# Dados descompactados do INMET

Baixe os arquivos anuais de 2002 a 2025 em:

https://portal.inmet.gov.br/dadoshistoricos

Descompacte os arquivos anuais. A organização recomendada é:

```text
2002/INMET_..._A705_BAURU_...2002....CSV
2003/INMET_..._A705_BAURU_...2003....CSV
...
2025/INMET_..._A705_BAURU_...2025....CSV
```

O notebook procura recursivamente arquivos `.csv` que contenham `A705_BAURU` no nome. Portanto, a organização exata das subpastas pode variar. Basta existir um CSV da estação para cada ano entre 2002 e 2025.

Os dados brutos não são versionados por causa do tamanho. Se as pastas descompactadas estiverem em outro local, defina a variável de ambiente `INMET_DADOS_DIR` antes de abrir o VS Code ou iniciar o Jupyter.
