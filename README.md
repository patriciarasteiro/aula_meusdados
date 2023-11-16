---
title: "README"
output: github_document
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```

# Sobre o Projeto

Projeto em desenvolvimento no meu doutorado no Programa de Genética e Biologia Molecular da Universidade Federal de Goiás. Um dos objetivos e estudar a evolução das enzimas digestivas tripsina e quimotripsina das borboletas e mariposas (ordem lepidoptera).

## Organização das pastas

As pastas estão organizadas e numeradas de acordo com as etapas das análises e suas subpastas contêm os resultados das análises e scripts utilizados. Os dados brutos são colocados na pasta data.

## Data

Dados das espécies de lepidoptera selecionadas do NCBI e planilha do banco de dados das plantas hospedeiras.

## 1_analise_qualidade

Etapa de analise da qualidade das sequências proteínas das espécies selecionadas do NCBI e testes para escolha do grupo externo da árvore filogenética. 

### Isoformas

Para manter as isoformas mais longas foi utilizado o script AGAT:

```{bash}
for file in *gff; do agat_sp_keep_longest_isoform.pl -gff $file -o $file.longest; done
```

Link script AGAT: [hiperlink](https://github.com/NBISweden/AGAT/blob/master/bin/agat_sp_keep_longest_isoform.pl)


### Busco




## 2_filogenia_especies




You can include R code in the document as follows:

```{r cars}
summary(cars)
```

## Including Plots

You can also embed plots, for example:

```{r pressure, echo=FALSE}
plot(pressure)
```

Note that the `echo = FALSE` parameter was added to the code chunk to prevent printing of the R code that generated the plot.
