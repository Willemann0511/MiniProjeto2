# MiniProjeto2

# 🏭 Inspeção de Qualidade Automática em Peças de Fundição (Indústria 4.0)

> **Mini-Projeto Avaliativo - Módulo 2 | Visão Computacional e Machine Learning**  
> **Curso:** SCTEC  
> **Data de Entrega:** 14/09/2026  

---

## 📌 1. Visão Geral do Projeto

Na Indústria 4.0, a automação do controle de qualidade em linhas de produção metálicas exige soluções ágeis e precisas. Este projeto implementa um pipeline híbrido em Python que combina **Processamento Digital de Imagens Clássico (OpenCV)** e **Deep Learning (TensorFlow/Keras)**.

### 🎯 Objetivos:
* **Análise Exploratória Clássica:** Isolar e evidenciar ranhuras, trincas e defeitos estruturais em amostras de peças utilizando técnicas avançadas de Visão Computacional.
* **Classificação Automatizada:** Treinar uma Rede Neural Convolucional (CNN) com *Data Augmentation* dinâmico para automatizar a triagem de peças metálicas entre as classes **"OK"** e **"Defeituosa"**.

---

## 🛠️ 2. Estrutura do Repositório

O projeto foi desenvolvido seguindo boas práticas de versionamento com Git, utilizando *feature branches* dedicadas para cada Sprint do desenvolvimento.

```text
├── dataset/                     # Diretório com o dataset Casting Product
│   ├── def_front/               # Peças metálicas com defeito
│   └── ok_front/                # Peças metálicas sem defeito (OK)
├── notebooks/
│   └── mini_projeto_m2.ipynb    # Notebook com o código completo executado
├── images/                      # Capturas de tela e gráficos para o README
│   ├── opencv_exploratory.png   # Pipeline de filtros do OpenCV
│   └── training_history.png     # Gráficos de Loss e Acurácia
├── .gitignore
├── README.md                    # Relatório de apresentação do projeto
└── requirements.txt             # Dependências e bibliotecas do ambiente
```



🔬 3. Análise Exploratória Clássica (OpenCV)Antes da etapa de aprendizado profundo, aplicamos uma sequência de pré-processamento clássico sobre uma amostra com defeito para compreender a assinatura física das falhas estruturais.  Pipeline de Filtros Aplicados:Grayscale: Conversão da imagem de RGB para escala de cinza para reduzir a dimensionalidade mantendo variações de intensidade luminosa.  Gaussian Blur: Aplicação de filtro gaussiano $5 \times 5$ para suavização de ruído de alta frequência e pequenos artefatos.  Limiarização Otsu (Thresholding): Binarização automática da imagem para separar a peça metálica e os defeitos do fundo.  Detecção de Bordas (Canny): Aplicação do algoritmo de Canny para realçar e isolar as descontinuidades e rachaduras na superfície.  Operações Morfológicas: Combinação de Dilatação e Erosão para conectar contornos fraturados e evidenciar a extensão da ranhura.  

🧠 4. Arquitetura da IA & Data Augmentation (Keras)📥 Ingestão de Dados e AugmentationCarregamento em Lote: Ingestão automatizada das imagens via image_dataset_from_directory divididas em 80% para Treino e 20% para Validação.  Data Augmentation: Para simular variações reais na esteira industrial, aplicamos transformações dinâmicas na entrada da rede: rotações, zoom, inversões e alterações de brilho.  🏗️ Arquitetura do Modelo CNNCamada de Entrada & Augmentation: Recebe a imagem $(300, 300, 3)$ e aplica os aumentos de dados.  Rescaling: Normalização dos pixels da faixa $[0, 255]$ para $[0, 1]$.Blocos Convolucionais (3x): Intercalação de Conv2D com ativação ReLU e MaxPooling2D para extração de mapas de características.  Classificação (Head): Flatten para vetorização, Dense com Dropout(0.5) para prevenir overfitting, e camada final Dense com ativação Sigmoid para classificação binária.  

📊 5. Auditoria Gráfica do TreinamentoApós a execução do treinamento por 15 épocas, geramos a visualização analítica das curvas de desempenho[cite: 1]:Comportamento da Loss: A queda contínua da perda de treino (loss) e validação (val_loss) demonstra a convergência estável do modelo[cite: 1].Generalização: O alinhamento entre as curvas evidencia que o Data Augmentation e o Dropout preveniram o overfitting[cite: 1].

🎥 6. Apresentação em Vídeo
🚀 Como Executar o Projeto
Clone o repositório:

Bash
git clone https://github.com/seu-usuario/seu-repositorio.git
cd seu-repositorio
Instale as dependências:

Bash
pip install -r requirements.txt
Execute o Notebook:
Abra o arquivo notebooks/mini_projeto_m2.ipynb no Jupyter Notebook ou VS Code e execute as células em ordem.
