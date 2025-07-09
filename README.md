
# Classificação de Uso do Solo com Sentinel-2

Este projeto utiliza imagens multiespectrais do satélite Sentinel-2 para classificar automaticamente o uso do solo em quatro categorias:

- 🌿 Vegetação
- 🏜️ Não vegetação
- 💧 Água
- ❓ Não definida (ignorada no treinamento)

## 📂 Estrutura do Projeto

```
classificacao_uso_solo/
├── img_sentinel/         # Imagens .jp2 do Sentinel-2
├── scripts/              # Scripts de processamento e modelos
├── resultados/           # Saída dos classificadores
├── main.py               # Execução principal
├── requirements.txt      # Dependências
└── README.md             # Este arquivo
```

## 🚀 Como executar

```bash
# 1. Crie o ambiente virtual
python -m venv venv
source venv/bin/activate  # ou venv\Scripts\activate no Windows

# 2. Instale as dependências
pip install -r requirements.txt

# 3. Execute o script principal
python main.py
```

## 🧪 Pré-processamento

- Bandas utilizadas:
  - B01, B02, B03, B04, B05, B06, B07, B8A, B11, B12 (exceto B8, B9, B10)
- Operações aplicadas:
  - Normalização das bandas para o intervalo [0, 1]
  - Alinhamento espacial com a máscara SCL (Scene Classification Layer)
  - Extração de vetores espectrais por pixel (ignorando classe não definida)

## 📊 Dados

- Total de amostras: 29.594.170 pixels válidos
- Após amostragem para economia de memória:
  - Conjunto de treinamento: 80.000 pixels (~80%)
  - Conjunto de teste: 20.000 pixels (~20%)
- Distribuição por classe no teste (com base na matriz de confusão):
  - Vegetação: 17.593 pixels
  - Não vegetação: 1.175 pixels
  - Água: 1.232 pixels

## 🧠 Modelos Treinados

### 🎯 Random Forest

- Arquivo: `resultados/random_forest_model.pkl`
- Relatório: [`random_forest_relatorio.txt`](./resultados/random_forest_relatorio.txt)
- Matriz de Confusão:  
  ![Random Forest](./resultados/matriz_confusao_random_forest.png)

### 🎯 SVM

- Arquivo: `resultados/svm_model.pkl`
- Relatório: [`svm_relatorio.txt`](./resultados/svm_relatorio.txt)
- Matriz de Confusão:  
  ![SVM](./resultados/matriz_confusao_svm.png)

## 📈 Métricas Avaliadas

- **Acurácia**
- **Precisão**
- **Revocação**
- **F1-Score**
- **Matriz de Confusão (visual e textual)**

## 📚 Próximos Passos

- Testar classificadores baseados em redes neurais (CNN)
- Aplicar pós-processamento espacial
- Avaliar desempenho sobre diferentes cenas Sentinel-2

---

Desenvolvido para fins educacionais e experimentais 🌱
