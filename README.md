# Análisis NLP de normativas de inocuidad alimentaria + chatbot con LLM

![Python](https://img.shields.io/badge/Python-3.x-blue) ![NLP](https://img.shields.io/badge/NLP-RoBERTa%20%7C%20LDA-8A2BE2) ![Groq](https://img.shields.io/badge/LLM-Groq-F55036)

Pipeline de procesamiento de lenguaje natural sobre un corpus técnico-normativo de **7 estándares de inocuidad alimentaria** (casi 800 páginas): **ISO 22000, BRCGS v9, HACCP, Codex Alimentarius, Reglamento Sanitario de los Alimentos de Chile (RSA), IFS Food v8 y FSMA**.

El objetivo es identificar automáticamente la densidad de riesgos y las diferencias de enfoque entre normativas (por ejemplo, el enfoque preventivo de FSMA frente a IFS o BRCGS), y usar esos resultados como contexto de un **chatbot que asiste a supervisión y gerencia de planta durante auditorías**.

## Pipeline

| Etapa | Técnicas |
|---|---|
| 1. Ingesta y limpieza | Extracción de PDFs (`pypdf`), limpieza en 3 rondas, stopwords de dominio normativo y Document-Term Matrix |
| 2. EDA | Frecuencias, riqueza léxica por normativa, word cloud, treemap y lollipop charts |
| 3. Sentimiento | Línea base léxica (TextBlob) frente a modelo neuronal **RoBERTa** (`pysentimiento`) y evolución intratextual en 12 fragmentos |
| 4A. Modelado de temas | POS tagging, **LDA** (`gensim`) con exploración de hiperparámetros |
| 4B. Chatbot | *System prompt* dinámico que inyecta frecuencias, sentimiento y temas LDA en un LLM vía **Groq**, con interfaz `ipywidgets` |

## Estructura

```
notebooks/
└── food_safety_nlp_analysis.ipynb
```

## Cómo ejecutarlo

Diseñado para Google Colab. El chatbot requiere una API key de [Groq](https://console.groq.com/keys) definida como variable de entorno (en Colab, usa *Secrets*):

```bash
export GROQ_API_KEY="tu_clave"
pip install pypdf nltk gensim textblob pysentimiento groq wordcloud squarify plotly seaborn ipywidgets gdown
```

> Las normas ISO, BRCGS e IFS son documentos con derechos de autor y no se distribuyen en este repositorio.

**Stack:** Python · NLTK · gensim (LDA) · pysentimiento (RoBERTa) · TextBlob · scikit-learn · Groq LLM API · Plotly · ipywidgets
