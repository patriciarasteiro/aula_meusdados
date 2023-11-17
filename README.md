---
title: "README"
output: github_document
---

# README

# Sobre o Projeto

Projeto em desenvolvimento do meu doutorado no Programa de Pós-graduação em Genética e Biologia Molecular da Universidade Federal de Goiás. Um dos objetivos e estudar a evolução das enzimas digestivas tripsina e quimotripsina das borboletas e mariposas (ordem lepidoptera).

## Organização das pastas

As pastas estão organizadas e numeradas de acordo com as etapas das análises e suas subpastas contêm os resultados das análises e scripts utilizados. Os dados brutos são colocados na pasta data.

## Data

Dados das espécies de lepidoptera selecionadas do NCBI e planilha do banco de dados das plantas hospedeiras - [HOSTS - a Database of the World's Lepidopteran Hostplants](https://data.nhm.ac.uk/dataset/hosts).

A espécie Limnephilus lunatis usamos o banco de dados de genomas de lepidoptera [lepbase.org](http://download.lepbase.org/archive/v3/sequence/), única espécie não incluida do banco do NCBI.

## 1_analise_qualidade

Etapa de analise da qualidade das sequências proteínas das espécies selecionadas do NCBI e testes para escolha do grupo externo da árvore filogenética.

### Isoformas

Para manter as isoformas mais longas foi utilizado o script AGAT:

```{bash}
for file in *gff; do agat_sp_keep_longest_isoform.pl -gff $file -o $file.longest; done
```

[Acesse a página do AGAT](https://github.com/NBISweden/AGAT/blob/master/bin/agat_sp_keep_longest_isoform.pl)


### Busco

Para verificar a qualidade dos genomas foi utilizado para analise o banco de lepidoptera e de endopterygota do busco:


```{bash}
for file in *_protein.longestisof.faa; do busco -m protein -i $file -o $file.busco -l lepidoptera_odb10; done
```

```{bash}
for file in *_protein.longestisof.faa; do busco -m protein -i $file -o $file.busco -l endopterygota_odb10; done
```

[Banco com as linhagens](https://busco.ezlab.org/list_of_lineages.html)

Após análises as espécies Limnephilus lunatis(Trichoptera) e Ctenocephalides felis(Siphonaptera), do grupo externo, foram retiradas das proximas análise devido a genes fragmentados e alta quantidade de duplicações nos resultados do busco.

## 2_filogenia_especies

Construção das ávores filogenética usando resultados do busco para endopterygota e do Orthofinder:

### arvore_Busco

Primeiro foi realizado o alinhamento com o mafft em seguida a filtragem com trimAL e por ultimo as sequencias foram  concatenadas usando o catfasta2phyml.pl e usamos o iqtree para construir a árvore:

```{bash}
iqtree -s concated-fasta.fasta -m JTT -bb 1000
```

### arvore_orthofinder

Para inferir uma árvore filogenética baseada em ortogrupos utilizamos o  [Orthofinder](https://github.com/davidemms/OrthoFinder):

```{bash}
orthofinder -f proteinas/
```

Com os resultados do Orthofinder foi realizado a mesmas etapas do busco e por ultimo a iqtree:

```{bash}
iqtree -s concated.ortho-fasta.fasta -m JTT -bb 1000
```

### Visualização das árvores

Para visualização das árvores foi utilizado o [iTol](https://itol.embl.de/) e o script modificado para inserir os nomes das famílias. O script está na pasta 2__filogenia_especies. A pasta com os resultados do iqtree estão 1_output na mesma pasta.


## Referências
Gaden S. Robinson; Phillip R. Ackery; Ian Kitching; George W Beccaloni; Luis M. Hernández (2023). HOSTS - a Database of the World's Lepidopteran Hostplants [Data set]. Natural History Museum. https://doi.org/10.5519/havt50xw

## Autores
Patricia Rasteiro