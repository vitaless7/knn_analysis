
# 🔍 Análise de Classificação com kNN em Dígitos Manuscritos

## 📌 Introdução
O arquivo `lab1.tar.gz` contém uma base de dados de dígitos manuscritos e dois scripts. Descompacte o arquivo na sua área `/nobackup` para evitar problemas de quota.

## 🖼️ Extração de Características
O script `digits.py` extrai a representação mais simples possível de uma base de dados de dígitos manuscritos. O processo consiste em:
- 📌 Para cada posição da imagem, verifica-se o valor de intensidade do pixel.
- 🔲 Se o valor for maior que 128, a característica recebe valor `1`, caso contrário, `0`.
- 📏 As imagens possuem tamanho variável e, para que os classificadores funcionem corretamente, são normalizadas utilizando as variáveis `X` e `Y` dentro da função `rawpixel`.

Após a execução do programa, um arquivo chamado `features.txt` é criado no diretório corrente. Esse arquivo contém **2000 linhas** no formato:

```
0 0 0 1 1 
```

- 🔹 O primeiro número indica o **rótulo da classe**.
- 🔸 A sequência contém os valores das características.
- 📝 Exemplo: as características 0, 1, 2 e 3 possuem valores `0`, `0`, `1` e `1`, respectivamente.

## 🎯 Tarefa
Sua tarefa consiste em:
1. **Gerar diferentes vetores de características** variando os valores de `X` e `Y`.
2. **Utilizar um kNN** (k=3 e distância Euclidiana) para encontrar:
   - ❌ O conjunto de características que produziu os **piores** resultados de classificação.
   - ✅ O conjunto de características que produziu os **melhores** resultados de classificação.
3. **Dividir a base de dados**:
   - 📊 50% para treinamento.
   - 📈 50% para validação.
4. **Comparar as matrizes de confusão** nos dois casos e relatar:
   - 🔄 Quais foram as confusões resolvidas pela melhor representação.

## 🚀 Otimização do Modelo
Para a sua **melhor solução**, investigue se é possível **melhorar os resultados** ajustando:
- 🔢 O valor de `k`.
- 📏 A métrica de distância utilizada.

## 🏁 Conclusão
Ao final, compare os resultados e discuta as melhorias alcançadas com os ajustes realizados. 📊✨

