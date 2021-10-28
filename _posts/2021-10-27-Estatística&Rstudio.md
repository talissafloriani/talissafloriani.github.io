---
title: "Estatística & Rstudio"
output: html_document
---

## **Homework - Experimental Statistics**  
*The homework will be write in portuguese*  

### Pressuposições do Modelo  

Em uma análise de variância (ANOVA), a qual testa se há diferenças significativas entre as médias testadas, é exigido **pressuposições** sobre os erros.  

- Mas o que são essas pressuposições?   

Sabe-se que os erros de um experimento são aleatórios, e os mesmos são conhecidos como resíduos. Logo, a análise desses reíduos permitirá dizer se a análise de variância é aceitável.  
Nesse caso irei utilizar o modelo de um delineamento inteiramente casualizado, o qual é representado por:  

$$
Y_{ij} = \mu + a_i  + \epsilon_{ij}
$$  

Sendo:  

$$Y_{ij}$$: O valor observado no i-ésimo nível do fator A, na j-ésima repetição;  
$$\mu$$: Constante inerente a todas as observações;  
$$a_i$$: O efeito do i-ésimo nível do fator A;  
$$\epsilon_{ij}$$: O erro experimental.  

**Pressuposições:**  

**1. Aditividade do modelo:** Nesse tipo de modelo não tem como "enxergar" a pressuposição de aditividade. Como o modelo não possui blocos, é considerado que não há interação entre tratamentos e blocos.  
Em delineamentos com o efeito de blocos no modelo, não pode haver a interação entre blocos e tratamentos, se houver, a pressuposição de aditividade não é atendida.  

**2. Normalidade dos erros:** A distribuição deve ser normal, ou seja, os erros devem ser normalmente distruibuídos, devem seguir a curva. São aceitas apenas pequenas violações da normalidade.  

**3. Independência dos erros:** Eles devem ser independentemente distruibuídos, ou seja,o erro de uma observação é apenas daquela observação, ele não pode estar correlacionado com erros de outra observação.    

**4. Homogeneidade de variâncias:** Os erros devem ter grandezas similares, a variância dos erros deve ser homogênea.    

Para o modelo em questão será considerado em maior parte as pressuposições de Normalidade e Homogeneidade. Se forem atendidas as pressuposições, então o teste F da análise de variância pode ser realizado.  
É importante mencionar que uma pressuposição não atendida, se vale a um ou mais dados atípicos. No entanto, dentro da pesquisa tais dados considerados atípicos (discrepantes) nem sempre estarão relacionados a erros, mas sim uma grande descoberta, por isso é necessário estar atento aos valores.  

- Testes de Normalidade: Shapiro-Wilk; Kolmorogov-Smirnov...  
- Teste de Homogeneidade de Variâncias: Hartley ou F máximo; Levene...  

Quando os testes de pressuposições não são atendidos? *Realizar a transformação dos dados.*

## Exercício

*Para dados no delineamento inteiramente casualizado: Verificar as pressuposições do modelo e interpretar os resultados.*  

Nesse exercício trabalharei com dados derivados de um delineamento inteiramente casualizado em feijão, o qual será testado a média de produtividade de 10 genótipos em Kg/Ha^-1^.Cada genótipo foi repetido 4 vezes em um sorteio dentro da área experimental.  

Os exemplos usam como base o Rmarkdown, então os códigos serão baseados em uma bibilioteca utilizando packages do Rstudio.   

### Visualização de banco de dados:

```R
#Anexando dados de um arquivo csv diretamente do excel
aula7 <- read.csv("aula7_v2.csv",header = T, sep = ";",dec = ",")
View(aula7)
names(aula7)
head(aula7,10)
```

### Análise Exploratória de Dados 
#### Gráficos pelo ggplot
```R
#Carregando biblioteca ggplot (para os melhores gráficos)
library(ggplot2)
ggplot(aula7) + 
  geom_point(mapping = aes(x = Gen, y = Rend), color = "hotpink1")
```

#### Gráfico de Caixa
```R
# O boxplot é muito utilizado na estatística experimental e também é anexado via ggplot
ggplot(aula7) +
  geom_boxplot(mapping = aes(group= Gen, x = Gen, y = Rend), color= "hotpink1")

```

### Estatísticas Descritivas
```R
n = with(aula7, tapply(Rend, Gen, length))
soma = with(aula7, tapply(Rend, Gen, sum))
media = with(aula7, tapply(Rend, Gen, mean))
variancia = with(aula7, tapply(Rend, Gen, var))
```

### Criando uma função para calcular a Amplitude  
```R
f1 = function(x) max(x) - min(x)
amplitude = with(aula7, tapply(Rend, Gen, f1))
resumo = rbind(n, soma, media, variancia, amplitude)
row.names(resumo) = c("n","soma","media","variancia","amplitude")
round(resumo, 2)

```
### Análise de Variância (ANOVA)

```R
#Carregar a biblioteca agricolae que facilita a vida quando trabalhando com a análise de variância
library(agricolae)
model1=aov(Rend~Gen, data = aula7)
anova(model1)
(tabela=HSD.test(model1,trt='Gen')) # Teste Tukey (alpha=5%)
```

### Teste de Tukey e Pressuposições

```R
#Anexando packages a análise e utilizando a biblioteca ExpDes.pt
library(ExpDes.pt)
with(aula7,
     dic (Gen, Rend, quali = TRUE, mcomp = "tukey",
          sigF = 0.05, sigT = 0.05))
```

Nesse caso, de acordo com os resultados obtidos com meus dados gerados, a normalidade e a homogeneidade estão de acordo com o modelo, logo, não será necessária a transformação dos dados. Os resultados podem variar de acordo com os dados trabalhados.   

ps: Rmarkdown com essa análise de estatística experimental salva no Blog, para nunca mais esquecer e para que eu (e você que está lendo) possa acessar quando necessário.  
xoxo:*





