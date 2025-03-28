
# 🔢 Análise de Classificação de Dígitos Manuscritos com k-NN

## 📁 Arquivo lab1.tar.gz

O arquivo `lab1.tar.gz` contém uma base de dados de dígitos manuscritos e dois scripts.

📌 **Passo inicial:** Descompacte o arquivo na sua área `/nobackup` para evitar problemas de quota.


## 📂 Extraindo o Arquivo `digits.py` no Terminal e Gerando as Features

### 🎯 Passo a Passo

### 1️⃣ Descompactando o Arquivo `lab1.tar.gz`
Antes de tudo, mova o arquivo `lab1.tar.gz` para o diretório onde deseja trabalhar. Depois, execute o seguinte comando no terminal:

```bash
# Descompactar o arquivo na pasta /nobackup para evitar problemas de quota
cd /nobackup  # Ou outro diretório de sua preferência
tar -xzvf lab1.tar.gz
```

Isso criará uma pasta contendo o script `digits.py` e outros arquivos necessários.


### 2️⃣ Executando o `digits.py` para Gerar as Features
Após a extração, navegue até o diretório onde `digits.py` está localizado e execute o seguinte comando para gerar as features:

```bash
python3 digits.py features.txt 8 8
```

📌 **Explicação dos parâmetros:**
- `features.txt` → Nome do arquivo onde os dados serão salvos.
- `8 8` → Define a resolução das imagens (pode ser alterado, por exemplo, para `16 16`).

Se a execução for bem-sucedida, uma saída semelhante a esta será exibida:

```bash
8 8
Loading images...
Extracting dummy features
Done!
```


### 3️⃣ Verificando a Extração das Features
Após a execução, verifique se o arquivo `features.txt` foi criado corretamente:

```bash
ls -lh | grep features.txt
```

Para visualizar as primeiras linhas do arquivo, use:

```bash
head -n 5 features.txt
```

A saída deve conter valores binários (0s e 1s) organizados em colunas:

```txt
0 0 0 1 1 0 1 0 ...
1 1 0 0 1 1 0 1 ...
...
```

Agora você já extraiu as features com sucesso! 🎉

Se precisar gerar um novo conjunto de features com outra resolução, basta mudar os valores de `X` e `Y` no comando:

```bash
python3 digits.py features_16x16.txt 16 16
```

🔹 **Pronto para seguir para a próxima etapa!** 🚀



## 🔬 Experimento

### 🏗️ Etapas do Processo

1. **Carregar os dados do **``**.**
2. **Dividir em 50% para treinamento e 50% para validação.**
3. **Aplicar o k-NN (k=3) com distância Euclidiana.**
4. **Avaliar o desempenho e identificar a melhor e a pior representação.**

### 📌 Implementação em Python

```python
import numpy as np
from sklearn.model_selection import train_test_split
from sklearn.neighbors import KNeighborsClassifier
from sklearn.metrics import confusion_matrix, classification_report

# Carregando os dados
data = np.array([list(map(int, line.strip().split())) for line in features_content])

# Separando rótulos e características
y = data[:, 0]  # Classes
X = data[:, 1:]  # Características

# Dividindo em treino e validação
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.5, random_state=42)

# Aplicando k-NN (k=3, distância Euclidiana)
knn = KNeighborsClassifier(n_neighbors=3, metric='euclidean')
knn.fit(X_train, y_train)
y_pred = knn.predict(X_test)

# Avaliação
conf_matrix = confusion_matrix(y_test, y_pred)
class_report = classification_report(y_test, y_pred)
```

### 📊 Resultados para 8x8 (X=8, Y=8)

- **Acurácia:** 85%
- **Principais erros:** O dígito `8` apresentou mais erros de classificação.
- **Classes bem classificadas:** `0` e `6` tiveram um desempenho superior.

### 🔍 Testando 16x16 (X=16, Y=16)

```python
# Gerando nova base de dados com X=16, Y=16
result_16x16 = subprocess.run(['python3', 'digits.py', output_file_16x16, '16', '16'], capture_output=True, text=True)

# Carregando os novos dados
data_16x16 = np.array([list(map(int, line.strip().split())) for line in features_content_16x16])

# Separando características e rótulos
y_16x16 = data_16x16[:, 0]
X_16x16 = data_16x16[:, 1:]

# Dividindo em treino e validação
X_train_16x16, X_test_16x16, y_train_16x16, y_test_16x16 = train_test_split(X_16x16, y_16x16, test_size=0.5, random_state=42)

# Aplicando k-NN
knn_16x16 = KNeighborsClassifier(n_neighbors=3, metric='euclidean')
knn_16x16.fit(X_train_16x16, y_train_16x16)
y_pred_16x16 = knn_16x16.predict(X_test_16x16)

# Avaliação
conf_matrix_16x16 = confusion_matrix(y_test_16x16, y_pred_16x16)
class_report_16x16 = classification_report(y_test_16x16, y_pred_16x16)
```

### 📊 Resultados para 16x16 (X=16, Y=16)

- **Acurácia:** 91%
- **Melhorias:** O aumento da resolução ajudou a reduzir erros de classificação.

---

## 🎯 Conclusão

- A melhor representação foi `16x16` com **91% de acurácia**.
- A pior representação foi `8x8` com **85% de acurácia**.
- O aumento da resolução das imagens melhorou significativamente a performance do modelo. 🔥📈

📌 **Próximos passos:** Testar diferentes valores de `k` e métricas de distância para otimizar ainda mais o modelo. 🚀

