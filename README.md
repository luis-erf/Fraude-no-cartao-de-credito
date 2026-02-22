# Detecção de Fraude em Cartões de Crédito — Reproduzir exclusivamente no Google Colab

Este README descreve o fluxo específico para **reproduzir os notebooks Jupyter no Google Colab** usando os arquivos obtidos diretamente do repositório GitHub (baixando/clonando o repositório no seu computador) e, **adicionalmente**, como **utilizar um modelo** já treinado sem necessidade de re-treinamento.

Todas as instruções abaixo são pensadas apenas para execução no Google Colab.

---

## Fluxo geral resumido

1. Baixe o repositório do GitHub no seu computador.  
2. No Google Colab, faça upload do notebook (.ipynb) que deseja executar.  
3. No Colab, faça download dos arquivos de dataset a partir dos links do Google Drive (fornecidos abaixo).  
4. Execute os notebooks na ordem indicada.  
5. (Opcional) Utilize o modelo treinado para gerar previsões em novos dados, sem re-treinamento.

---

## 1) Baixar o repositório (no seu computador)

Opções:

* Clonar via git:
```bash
git clone https://github.com/luis-erf/Fraude-no-cartao-de-credito.git
```

Ou baixar ZIP:
Acesse a página do repositório e clique em Code → Download ZIP.
Extraia o ZIP em uma pasta local.
Após baixar, você terá a estrutura com os notebooks e arquivos auxiliares.

---

## 2) Abrir notebooks no Google Colab (a partir dos arquivos baixados)
Opções para abrir um notebook do seu computador no Colab:

No Colab: File → Open notebook → Upload → selecione o arquivo .ipynb baixado.

Alternativa via upload por código (menos comum para notebooks):

```python
from google.colab import files
uploaded = files.upload()
```

> Observação: para notebooks, a opção **Open notebook → Upload** é a mais simples.

---

## 3) Acessar os arquivos de dataset via Google Drive
Os datasets usados neste projeto serão disponibilizados via links do Google Drive. Os nomes dos arquivos e seu uso são:

train.csv — usado na EDA e no tratamento de dados.
train_prep.csv — usado na etapa de modelagem (dados pré-processados / preparados).

Links de Download (Google Drive): https://drive.google.com/drive/folders/1rpGo0vziNC4EPXl0hZyKuE28PBov0wv3?usp=drive_link
Método alternativo — download automático via código (no Colab)

---

## 4) Ordem de execução recomendada dos notebooks
Abra cada notebook no Colab, faça o download dos datasets indicados e execute as células na ordem.

## 4.1) EDA (Ex.: EDA.ipynb)
* Dataset: `train.csv`
* Objetivo: análise exploratória, estatísticas descritivas, distribuições, análise de classes (fraude vs legítimo), correlações e visualizações iniciais.
## 4.2) Tratamento de Dados (Ex.: Tratamento_de_dados.ipynb)
* Dataset: `train.csv`
* Objetivo: limpeza, tratamento de valores ausentes.
## 4.3) Modelagem (Ex.: Modelagem_final.ipynb)
* Dataset: `train_prep.csv`
* Objetivo: treinamento, validação e avaliação de modelos de classificação, busca por hiperparâmetros, geração do modelo final e salvamento.

---

## 5) Utilizar o modelo já treinado (sem re-treinar)
Esta etapa demonstra como **carregar o modelo** pronto e aplicá-lo diretamente em novos dados, apenas para inferência.

5.1) Upload dos arquivos necessários
No Google Colab, faça upload (ou baixe do Drive) dos seguintes arquivos, caso estejam no repositório ou em Drive:

* `modelo_final.pkl` → modelo treinado
Você pode fazer upload manual via Files → Upload, ou usar gdown se os arquivos estiverem no Drive.

5.2) Carregar os dados de teste/exemplos
Exemplo de carregamento de um CSV de exemplo:

```python
import pandas as pd

# Carregar exemplo (pode ser train.csv ou outro arquivo de amostra)
df = pd.read_csv('train.csv')  # ou path para seu arquivo de teste

print("Primeiros 5 registros:")
print(df.head())
```

5.3) Carregar o modelo e o scaler
```python
import joblib

model = joblib.load("modelo_final.pkl")
```
5.4) Pré-processamento (exemplo genérico)
Ajuste esta etapa conforme as transformações aplicadas no pipeline de treino (mesmas colunas, mesma ordem e mesmas operações).

```python
# Transformar o dataset para o mesmo formato usado no modelo
df.drop_duplicates(inplace=True)
X = df.drop(columns=['id])

#Realize a previsão
y_proba = model['model'].predict_proba(X)
print("Probabilidades (primeiras linhas):")
print(y_proba[:5])
```
