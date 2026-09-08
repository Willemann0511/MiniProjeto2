# MiniProjeto2

# 🏭 Inspeção de Qualidade Automática em Peças de Fundição (Indústria 4.0)

> **Mini-Projeto Avaliativo - Módulo 2 | Visão Computacional e Machine Learning**  
> **Curso:** SCTEC  
> **Data de Entrega:** 14/09/2026  

---

## 📌 1. Visão Geral do Projeto

Na Indústria 4.0, a automação do controle de qualidade em linhas de produção metálicas exige soluções ágeis e precisas. Este projeto implementa um pipeline híbrido em Python que combina **Processamento Digital de Imagens Clássico (OpenCV)** e **Deep Learning (TensorFlow/Keras)**.

### 🎯 Objetivos:
1. **Análise Exploratória Clássica:** Isolar e evidenciar ranhuras, trincas e defeitos estruturais em amostras de peças utilizando técnicas avançadas de Visão Computacional.
2. **Classificação Automatizada:** Treinar uma Rede Neural Convolucional (CNN) com *Data Augmentation* dinâmico para automatizar a triagem de peças metálicas entre as classes **"OK"** e **"Defeituosa"**.

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
