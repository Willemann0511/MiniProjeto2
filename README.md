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



🔬 3. Análise Exploratória Clássica (OpenCV)Antes da etapa de aprendizado profundo, aplicamos uma sequência de pré-processamento clássico sobre uma amostra com defeito para compreender a assinatura física das falhas estruturais.Pipeline de Filtros Aplicados:Grayscale: Conversão da imagem de RGB para escala de cinza para reduzir a dimensionalidade de canais mantendo as variações de intensidade luminosa.Gaussian Blur: Aplicação de filtro gaussiano $5 \times 5$ para suavização de ruído de alta frequência e pequenos artefatos do ambiente industrial.Limiarização Otsu (Thresholding): Binarização automática da imagem para separar a peça metálica e os defeitos do fundo.Detecção de Bordas (Canny): Aplicação do algoritmo de Canny para realçar e isolar as descontinuidades e rachaduras na superfície da peça.Operações Morfológicas: Combinação de Dilatação e Erosão para conectar contornos fraturados e evidenciar visualmente a extensão da ranhura.O pipeline clássico provou ser essencial para confirmar que os defeitos possuem bordas bem definidas e padrões de iluminação distintos em relação às peças íntegras.

🧠 4. Arquitetura da IA & Data Augmentation (Keras)📥 Ingestão de Dados e AugmentationCarregamento em Lote: Ingestão automatizada das imagens via image_dataset_from_directory divididas em 80% para Treino e 20% para Validação (com imagens redimensionadas para $300 \times 300$ pixels).Data Augmentation: Para simular variações reais de posicionamento na esteira industrial, aplicamos transformações dinâmicas na entrada da rede:Inversões horizontais e verticais (RandomFlip)Rotações aleatórias (RandomRotation)Zoom ajustável (RandomZoom)Alterações de iluminação (RandomBrightness)🏗️ Arquitetura do Modelo CNNO modelo foi construído utilizando a API Sequential do Keras, intercalando blocos de extração de características e classificação binária:Camada de Entrada & Augmentation: Recebe a imagem $(300, 300, 3)$ e aplica os aumentos de dados.Rescaling: Normalização dos pixels da faixa $[0, 255]$ para $[0, 1]$.Blocos Convolucionais (3x):Conv2D com filtros crescentes (32, 64, 128) e ativação ReLU para extração de mapas de características.MaxPooling2D $(2 \times 2)$ para redução de dimensionalidade e garantia de invariância à tradução.Classificação (Head):Flatten para vetorização da matriz de características.Dense com 64 neurônios + Dropout(0.5) para prevenir o overfitting.Dense final com 1 neurônio e ativação Sigmoid para saída probabilística binária (0 = OK, 1 = Defeituoso).Compilação: Otimizador Adam e função de perda binary_crossentropy.

📊 5. Auditoria Gráfica do TreinamentoApós a execução do treinamento por 15 épocas, geramos a visualização analítica das curvas de desempenho:📈 Análise das Curvas de Loss e Acurácia:Comportamento da Loss: A queda contínua tanto da perda de treino (loss) quanto da perda de validação (val_loss) demonstra que o modelo convergiu de maneira estável.Generalização: O alinhamento próximo entre as curvas de treino e validação evidencia que as técnicas de Data Augmentation e Dropout foram eficazes para prevenir o overfitting, garantindo que a IA aprenda a generalizar o padrão das trincas para novas peças na fábrica.

🎥 6. Apresentação em VídeoA explicação técnica detalhada, demonstração do código em execução e a defesa da solução estão disponíveis no vídeo abaixo:🔗 Clique aqui para assistir à Apresentação do Projeto (Google Drive)Tópicos Abordados no Vídeo (Duração: < 5 min):Objetivo do sistema industrial e demonstração das células do Jupyter Notebook.Análise dos resultados obtidos com os filtros clássicos do OpenCV (Canny, Blur, Morfologia).Estruturação da arquitetura CNN e lógica por trás do Data Augmentation.Auditoria gráfica e discussão sobre Overfitting vs. Aprendizado saudável do modelo.


🚀 Como Executar o ProjetoClone o repositório:Bashgit clone [https://github.com/seu-usuario/seu-repositorio.git](https://github.com/seu-usuario/seu-repositorio.git)
cd seu-repositorio
Instale as dependências:Bashpip install -r requirements.txt
Execute o Notebook:
Abra o arquivo notebooks/mini_projeto_m2.ipynb no Jupyter Notebook, Google Colab ou VS Code e execute as células em ordem.
