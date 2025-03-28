
# 🔢 Análise de Classificação de Dígitos Manuscritos com k-NN

## 📁 Arquivo lab1.tar.gz

O arquivo `lab1.tar.gz` contém uma base de dados de dígitos manuscritos e dois scripts.

📌 **Passo inicial:** Descompacte o arquivo na sua área `/nobackup` para evitar problemas de quota.

---

## 📝 Extração de Características

O script `digits.py` extrai a representação mais simples possível de uma base de dados de dígitos manuscritos:

- Para cada posição da imagem, verifica-se a intensidade do pixel.
- Se o valor for > 128, a característica é igual a 1; caso contrário, 0.
- Como os classificadores precisam de um vetor de tamanho fixo, as imagens são normalizadas utilizando as variáveis `X` e `Y` dentro da função `rawpixel`.
- Após a execução do programa, um arquivo chamado `features.txt` é criado, contendo 2000 linhas no formato:
  ```
  0 0 0 1 1
  ```
  O primeiro número indica o rótulo da classe, seguido pelos valores das características.

---

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

