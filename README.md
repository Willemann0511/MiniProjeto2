# ⚙️ Sistema Híbrido de Inspeção de Defeitos Industriais
> **Machine Learning & Visão Computacional na Indústria 4.0**  
> *Pipeline automatizado para detecção de falhas em peças metálicas de fundição (Casting Products).*

---

## 📌 Visão Geral do Projeto
Este projeto apresenta uma solução automatizada de visão computacional voltada para o controle de qualidade industrial. A arquitetura combina **técnicas clássicas de Processamento Digital de Imagens (OpenCV)** para análise exploratória e isolamento de características com uma **Rede Neural Convolucional (CNN via TensorFlow/Keras)** para classificação binária em larga escala nas classes `def_front` (peça com defeito) e `ok_front` (peça aprovada).

---

## 🛠️ Tecnologias e Bibliotecas Utilizadas
* **Linguagem & Ambiente:** Python 3.x, Google Colab (Aceleração por GPU T4).
* **Processamento Digital de Imagens:** OpenCV (`cv2` - Grayscale, Gaussian Blur, Median Blur, Sobel, Canny, Operações Morfológicas).
* **Deep Learning & Data Augmentation:** TensorFlow 2.x / Keras (`Sequential`, `Conv2D`, `MaxPooling2D`, `Dropout`, `Adam`, `Binary Crossentropy`).
* **Análise & Auditoria:** Matplotlib, Seaborn, Scikit-Learn (Matriz de Confusão e *Classification Report*).

---

## 🚀 Estrutura dos Sprints Industriais

### 🔹 Sprint 1 & 2: Preparação de Ambiente e Suavização Inicial
* Montagem do Google Drive no ambiente Google Colab e organização do dataset.
* Conversão de espaço de cor BGR para **Grayscale** para redução de dimensionalidade.
* Aplicação de filtros **Gaussian Blur (5x5)** e **Median Blur (k=5)** para remoção de ruídos de granulação metálica sem apagar as bordas reais dos defeitos.

### 🔹 Sprint 3: Destaque de Características (OpenCV)
Isolamento visual dos defeitos estruturais através de um pipeline clássico:
1. **Limiarização de Otsu:** Segmentação binária automática baseada no histograma de iluminação da peça.
2. **Detecção de Bordas (Canny & Sobel):** Extração de gradientes de alto contraste característicos de trincas e ranhuras.
3. **Morfologia Matemática:** Aplicação de *Dilatação* (fechamento de contornos desconectados) seguida de *Erosão* (eliminação de ruídos periféricos).

### 🔹 Sprint 4: Ingestão em Lote e Data Augmentation
* Carregamento automatizado das pastas `def_front` e `ok_front` via `image_dataset_from_directory` na proporção **80% Treino / 20% Validação** (resolução 300x300, batch size 32, seed 123).
* Otimização de alta velocidade I/O com `cache()` e `prefetch(AUTOTUNE)`.
* Implementação da camada sequencial de **Data Augmentation** para simular imprecisões da esteira industrial:
  * Inversões horizontais e verticais (`RandomFlip`)
  * Rotações aleatórias de até 20% (`RandomRotation`)
  * Ajustes de Zoom de até 10% (`RandomZoom`)
  * Variação de brilho de até 20% (`RandomBrightness`)

### 🔹 Sprint 5: Arquitetura CNN e Treinamento
Construção de um modelo sequencial convolucional focado no aprendizado hierárquico de características:
* **Entrada:** `(300, 300, 3)` + Camada de Reescalonamento (`Rescaling(1./255)`).
* **Extração de Feições:** 3 Blocos convolucionais (`Conv2D` com 32, 64 e 128 filtros + ativação `ReLU` intercalados com `MaxPooling2D(2,2)`).
* **Classificação Binária:** Achatamento via `Flatten`, camada oculta `Dense(64)`, camada de regularização **`Dropout(0.5)`** (prevenção ativa de memorização) e saída `Dense(1)` com função **Sigmoid**.
* **Compilação:** Otimizador **Adam** e função de perda **Binary Crossentropy** ao longo de 15 épocas.

### 🔹 Sprint 6: Auditoria Gráfica e Desempenho
Geração das curvas analíticas de aprendizado (*Loss* e *Accuracy*) e avaliação formal no conjunto de validação (260 imagens).

---

## 📊 Auditoria de Resultados e Diagnóstico do Modelo

### 📑 Tabela de Desempenho (Conjunto de Validação)

| Métrica | Classe `def_front` (Com Defeito) | Classe `ok_front` (Aprovada) | Geral (Macro Avg / Accuracy) |
| :--- | :---: | :---: | :---: |
| **Precision** | **0.93 (93%)** | 0.60 (60%) | 0.76 (76%) |
| **Recall** | 0.62 (62%) | **0.92 (92%)** | 0.77 (77%) |
| **F1-Score** | 0.74 (74%) | 0.73 (73%) | 0.73 (73%) |
| **Acurácia Total** | - | - | **73%** (Picos de até **81%**) |

### 💡 Diagnóstico de Overfitting
* As curvas de perda de treino (`train_loss`) e validação (`val_loss`) decresceram de forma contínua ao longo das 15 épocas.
* A curva de `val_loss` manteve-se consistentemente **abaixo** da curva de treino, e a acurácia de validação permaneceu superior à de treino.
* **Conclusão:** **NÃO ocorreu overfitting e o modelo aprendeu de forma saudável**. Esse comportamento é o efeito esperado da combinação do *Data Augmentation* com o *Dropout(0.5)*, que tornam o treinamento artificialmente mais complexo enquanto a validação avalia imagens limpas.

---

## 🔍 Análise da Matriz de Confusão

* **Verdadeiros Positivos (`def_front`):** 100 peças defeituosas identificadas corretamente.
* **Verdadeiros Negativos (`ok_front`):** 91 peças perfeitas aprovadas corretamente.
* **Falsos Positivos (Alarme Falso):** apenas 8 peças boas classificadas como defeituosas (Precisão da classe defeituosa de 93%).
* **Falsos Negativos (Erro Crítico Industrial):** 61 peças com falhas sutis classificadas como boas (Recall de 62%).
* **Recomendação Industrial:** Em futuras iterações na fábrica, recomenda-se calibrar o limiar de decisão (*threshold* da Sigmoid) de `0.5` para `0.3` para priorizar a retenção preventiva de qualquer peça suspeita.

---

## 📹 Vídeo de Apresentação Técnica
O vídeo demonstrativo com defesa do código e análise dos questionamentos acadêmicos (duração de até 5 minutos) está acessível pelo link:

🔗 **[Clique aqui para assistir ao Vídeo no Google Drive] https://drive.google.com/file/d/1yUH02JDaEynx18lSpRIR9E8XyQ7WA35W/view?usp=sharing*
