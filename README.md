# DS-Projeto-Final-EDA

Entrega do T2 para a matéria de Ciência de Dados

Gabriel Uemura Naka - 241024773
Thiago Toreto Damaceno de Souza - 241026164

-------------------------------------------------------

# Mudança climática em Bauru — estação INMET A705

Projeto de ciência de dados que investiga se a temperatura e o padrão de chuvas da estação automática A705, em Bauru (SP), apresentaram tendência entre 2002 e 2025.

## Pergunta

Há tendência estatisticamente relevante de aumento da temperatura ou mudança no padrão de chuvas na série histórica da estação A705?

## Dados e critérios

- Estação: A705 — Bauru (SP).
- Período analisado: 2002–2025.
- Importação esperada: 210.384 registros horários.
- Um dia é válido quando possui pelo menos 22 observações horárias válidas para a variável.
- Um ano é incluído na análise principal quando possui pelo menos 90% de dias válidos; 80% é usado como sensibilidade.
- Valores ausentes não são imputados nem convertidos em zero.
- Para chuva, são usados precipitação média por dia válido e proporção de dias com precipitação maior ou igual a 1 mm. O total anual bruto não é usado como indicador formal quando há lacunas.

## Estrutura

```text
tema-4-clima/
├── data/
│   ├── raw/                 # pastas e CSVs descompactados
│   └── processed/           # bases diária, mensal, anual e resultados OLS
├── figures/                 # gráficos PNG
├── notebooks/
│   └── analise_climatica.ipynb
├── requirements.txt
└── README.md
```

## Como reproduzir

1. Baixe os arquivos anuais de 2002 a 2025 no portal do INMET.
2. Descompacte cada arquivo em uma pasta dentro de `data/raw/`. A organização recomendada é `data/raw/2002/`, `data/raw/2003/`, até `data/raw/2025/`.
3. Em cada pasta anual, mantenha ao menos o CSV cujo nome contém `A705_BAURU`. Os demais arquivos de estações brasileiras podem ser removidos para economizar espaço.
4. Instale uma versão compatível do Python. O projeto foi validado com Python 3.13.
5. Crie e ative um ambiente virtual, a partir da raiz do projeto:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
python -m ipykernel install --user --name tema-4-clima --display-name "Python (tema-4-clima)"
```

6. Abra a pasta `tema-4-clima` no VS Code. Depois abra `notebooks/analise_climatica.ipynb`, selecione o kernel criado e execute `Restart Kernel` → `Run All`.

O notebook procura recursivamente os CSVs da estação A705 dentro de `data/raw`, normaliza as colunas de diferentes anos, aplica o controle de qualidade e recria os CSVs e figuras.

### Dados descompactados armazenados fora do projeto

Opcionalmente, os arquivos podem permanecer em outra pasta. Nesse caso, defina a variável de ambiente antes de iniciar o VS Code ou o Jupyter.

Windows PowerShell:

```powershell
$env:INMET_DADOS_DIR = "D:\dados\INMET_descompactado"
code .
```

Linux ou macOS:

```bash
export INMET_DADOS_DIR="/home/usuario/dados/INMET_descompactado"
code .
```

O notebook não grava esse caminho nos arquivos do projeto. Se a variável não estiver definida, `data/raw/` será usada automaticamente.

## Compilação do relatório

O relatório está em `relatorio/sn-article.tex` e utiliza o modelo Springer Nature.

### Requisitos no Windows

- [MiKTeX](https://miktex.org/download)
- [Strawberry Perl](https://download.cnet.com/strawberry-perl-64-bit/3000-2212_4-75808033.html)
- Extensão LaTeX Workshop no VS Code

Após instalar, feche e abra novamente o VS Code. Verifique no terminal:

```powershell
pdflatex --version
bibtex --version
perl --version
latexmk --version