# Taller Causal Inference

## Preguntas causales.

Creo que empezaré mi taller comentando algo que aunque parezca evidente no se suele decir. 
Hay dos tipos de cuestiones causales. 
1- Efecto de las causas. El efecto de una intervención. 
2-  Causas de los efectos. Qué ha podido ser la causa de esto?

## 0. The whole game

Ejemplo completo aunque no se entienda de lo que se hace en inferencia causal. 
Explicar los puntos por los que ha de pasar la inferencia causal. 

1 Ejemplo de los mosquitos ? Sacado del libro r-causal.org 
2 Specify a causal question
3 Draw our assumptions using a causal diagram
4 Model our assumptions
5 Diagnose our models
6 Estimate the causal effect
7 Conduct sensitivity analysis on the effect estimate

## 1. Potential outcomes

Exponer el principal problema de la inferencia causal, que es la imposibilidad 
de tener contrafactuales a nivel individual

Ejemplo del libro ROS. hay imagen en carpeta fig. Texto en páginas 341 y siguientes. 
Útil el comentario de que la lógica bajo _pre-post_ experimentos puede no ser suficiente, porque
el valor previo de la presión arterial de un sujeto previo al experimento puede no ser una buena
medida de su contrafactual. 

### Notas del libro (ROS)

At
the design stage, we can use randomization to ensure that treatment and control groups are balanced
in expectation, and we can use blocking to reduce the variation in any imbalance. At the analysis stage,
we can adjust for pre-treatment variables to correct for differences between the two groups to reduce
bias in our estimate of the sample average treatment effect

- External validity: Difficulty of extrapolating to new individuals and situations
More
generally, causal inference can be viewed as a special case of prediction in which the goal is to predict
what would have happened under different treatment options. Causal interpretations of regression
coefficients can only be justified by relying on much stronger assumptions than are needed for
predictive inference.

- However,
in observational studies, treatment exposure is observed rather than manipulated (for example,
comparisons of smokers to nonsmokers), and it is not reasonable to consider the observed data as
reflecting a random allocation across treatment groups.Thus, in an observational study, there can be systematic differences between groups of units
that receive different treatments with respect to key covariates, x, that can affect the outcome, y.
Such covariates that are associated with the treatment and the potential outcomes are typically called
confounders or confounding covariates because if we observe differences in average outcomes across
these groups, we can’t separately attribute these differences to the treatment or the confounders—the
effect of the treatment is thus “confounded” by these variables.
-Matching refers to any of a variety of procedures that restructure the original sample in preparation
for a statistical analysis. The goal of this restructuring in a causal inference setting is to create an
analysis sample that looks like it was created from a randomized experiment. 
-Given this, how can we make decisions in a scenario where we are not convinced that all
confounders have been included? One strategy to reduce risk is to avoid covariates that are strongly
related to the treatment variable but not strongly related to the outcome. The classic example of a
covariate that should not just be included as an additional predictor is an instrumental variable, as
discussed in Section 21.1.

- Said another way, it is only necessary to have common support with respect to
confounders, not all covariates.

We distinguish between two broad classes of causal queries:
1. Effects of causes. What might happen if we do z? What is the effect of some manipulation, for
example, the effect of job training on poverty status, the effect of smoking on health, the effect of
schooling on earnings, the effect of campaigns on election outcomes, and so forth?
2. Causes of effects. What causes y? Why do more attractive people earn more money? Why does
per capita income vary so much by country? Why do many poor people vote for Republicans and
rich people vote for Democrats? Why do some economies collapse while others thrive?
When methodologists write about causal inference, they generally focus on the effects of causes.
We are taught to answer questions of the type “What is the effect of z?”, rather than “What caused
y?” As we have discussed in the preceding chapters, potential outcomes can be framed in terms of
manipulations: if z were changed by one unit, how much would y be expected to change? But “What
caused this?” questions are important too. They are a natural way to think, and in many ways, these
causal questions motivate the research, including experiments and observational studies, that we use
to estimate particular causal effects.
How can we incorporate “What caused this?” questions into a statistical framework that is centered
around “What is the effect of this?” causal inference? A potentially useful frame of this issue is as
follows: “What is the effect?” causal inference is about estimation; “What caused this?” questions are
more about model checking and hypothesis generation. Therefore we do not try to answer “What
caused this?” questions; rather, our exploration of these questions motivates “What is the effect of?”
questions that can be studied using statistical tools such as the ones we have discussed in these
chapters: experiments and observational studies.

## 2. Supuestos para poder hacer estas cosas de la inferencia causal

* Los obvios: Causa ha de ser anterior al efecto
Cómo solventar parcialmente el problema fundamental? 

* Exchangeability (El solapamiento)
* Positivity
* Consistency
* Ignorability (no confounding)
* Stable unit treatment value assumption (SUTVA)

TODO (revisar)
* ¿Qué pasa si no se cumplen? 
    * Si no se cumple ignorability, tenemos confounding
    * Si no se cumple SUTVA, tenemos interferencia
    * Si no se cumple exchangeability, tenemos selection bias
    * Si no se cumple positivity, tenemos extrapolación
    * Si no se cumple consistency, tenemos measurement error

### Asunciones según r-causal.org (me gustan más )

1. Consistencia:  Qué realmente el análisis conteste a la pregunta causal 
 1.1 Buena definición del tratamiento. Que no haya múltiples versiones del mismo
 1.2 No interferencia. Que la variable respuesta de un individuo no dependa de la asignación de 
 tratmiento de otro.
A la consistencia también se le conoce como SUTVA.

2. Intercambiabilidad: Se asume que dentro de los niveles de las covariables (variables de confusión)
los individuos expuestos al tratamiento y no tratamiento tengan igual likelihood . A veces se dice
que no hay variables de confusión no medidas. 

3. Positividad: Que dentro de cada nivel y combinación de covariables, haya 
expuestos y no expuestos. O de otra manera,  que cada individuo tenga alguna probabildidad de
recibir o no el tratamiento. Básicamente positividad es que haya 0 < p < 1  

Se podría resumir  como "peras con peras" y "manzanas con manzanas". 
Suppose that there were in fact two containers of chocolate ice cream, one of which was spoiled

Violación de consistencia 1: El ejemplo que viene es bueno. 3 recipientes de helado. 2 tienen chocolate
y 1 vainilla. Pero hay uno de chocolate en mal estado, que hace que la variable y (te gusta del 0 al 10) 
sea 0 para todo aquel que prueba ese chocolate. Pero no se les dice a la gente cual es cual. 
Entonces hay diferentes versiones de chocolate (normal y en mal estado) y si mezclas los 
outcomes para ver el efecto causal estás jodido. 
Violación de inconsistancia 2. interferencia. Si que un individuo reciba el tratamiento afecta a otro
por ejemplo que en una ciudad se asignen precios bajos y altos de cabify ( y la gente se de cuenta)
y lo diga a sus amigos, afecta a la probabilidad de que los amigos cojan cabify.. Solución => 
aleatorizar para dar tratamiento barato en una ciudad o barrio y caro en otro. 

Violación de intercambialidad: In that example, participants were able to choose the ice cream that they wanted to eat,
so people who were more likely to have a positive effect from eating chocolate chose that, and those more likely to have
a positive effect from eating vanilla chose that.In that example, participants were able to choose the ice cream that
they wanted to eat, so people who were more likely to have a positive effect from eating chocolate chose that, and those
more likely to have a positive effect from eating vanilla chose that.
Básicamente, significa que si a los más propensos a elegir chocolate les dejo elegir , elegirán 
chocolate y hay un sesgo con respecto a los que eligen vainilla.. 

```
data <- data.frame(
  id = 1:10,
  y_chocolate = c(4, 4, 6, 5, 6, 5, 6, 7, 5, 6),
  y_vanilla = c(1, 3, 4, 5, 5, 6, 8, 6, 3, 5)
)
data_observed <- data |>
  mutate(
    exposure = case_when(
      # people who like chocolate more chose that
      y_chocolate > y_vanilla ~ "chocolate",
      # people who like vanilla more chose that
      y_vanilla >= y_chocolate ~ "vanilla"
    ),
    observed_outcome = case_when(
      exposure == "chocolate" ~ y_chocolate,
      exposure == "vanilla" ~ y_vanilla
    )
  ) |>
  select(id, exposure, observed_outcome)

data_observed |>
  group_by(exposure) |>
  summarise(avg_outcome = mean(observed_outcome))
```

How could we correct this? If we had some people who preferred chocolate ice cream but ended up taking vanilla instead,
we could adjust for the preference, and the effect conditioned on this would no longer have an exchangeability issue

Violación de positividad.En el ejemplo anterior, sólo si hay gente que elige vainilla 
en vez de chocolate aunque prefiera el chocolate, entonces se puede hacer algo. Tiene que ver
con el solapamiento, etc. si entre la gente que prefiere el chocolate no hay nadie que haya 
elegido vainilla no se puede construir el contrafactuaal.  Si hay al menos alguien que si
entonces se puede intentar ajustando por esa variable. 


```r
data <- data.frame(
  id = 1:10,
  y_chocolate = c(4, 4, 6, 5, 6, 5, 6, 7, 5, 6),
  y_vanilla = c(1, 3, 4, 5, 5, 6, 8, 6, 3, 5)
)

set.seed(11)
data_observed <- data |>
  mutate(
    prefer_chocolate = y_chocolate > y_vanilla,
    exposure = case_when(
      # people who like chocolate more chose that 80% of the time
      prefer_chocolate ~ ifelse(rbinom(n(), 1, 0.8), "chocolate", "vanilla"),
      # people who like vanilla more chose that 80% of the time
      !prefer_chocolate ~ ifelse(rbinom(n(), 1, 0.8), "vanilla", "chocolate")
    ),
    observed_outcome = case_when(
      exposure == "chocolate" ~ y_chocolate,
      exposure == "vanilla" ~ y_vanilla
    )
  ) |>
  select(id, prefer_chocolate, exposure, observed_outcome)


lm(
  observed_outcome ~ I(exposure == "chocolate") + prefer_chocolate,
  data_observed
)

```


## 3. RCT . ¿Se puede hacer siempre? 

* RCT es el gold standard, pero a veces no se puede

En el ejemplo de la red de mosquito no se puede, porque no puedo elegir gente al azar
y a unos obligarles a no tener red moquitera. Chiste negro no contar.  Quizá en la Alemania nazi deberían haber aprovechado
para hacer inferencia causal

Incluso si podemos hacer RCT, muchas de las técnicas mejoran la precisión de la estimación en ese caso

## 4. Pensemos en el DAG

Ciencia antes que estadística. 

* Uso del DAG para hacer explícitas las asunciones. library(tidyverse)
library(causalworkshop)
net_data |>
  ggplot(aes(malaria_risk, fill = net)) +
  geom_density(color = NA, alpha = .8)library(tidyverse)
library(causalworkshop)
net_data |>
  ggplot(aes(malaria_risk, fill = net)) +
  geom_density(color = NA, alpha = .8)

* Nomenclatura, puede que nueva para algunos. 
    * Forks
    * Mediators
    * Colliders

* Reglas de Pearl, (backdoor, frontdoor, etc), que nos pueden servir para identificar
qué variables hemos de considerar, supuesto correcto el DAG. 

* ¿nos podemos saltar algunas reglas de Pearl? Si, si ajustamos el sistema causal entero. Full-luxury

## 5. Técnicas.

Son sólo técnicas, lo importante es lo de antes

* Queremos acercarnos a lo que es un RCT, qué se puede hacer desde perspectiva clásica frecuentista.
 * Identificar variables con reglas de Pearl, uso de daggitty
 * Propensity Score Matching
 * Inverse Probability Weighting
 * Meta-learners
 * G-estimation ( esto nos sirve en frecuentista y en bayesiano)


## 6. Oye, que yo soy bayesiano

Usando el DAG y técnicas bayesianas es todo más natural y sencillo. 
"La inferencia causal no es más que predecir el efecto de la intervención" (es lo que se hace con G-estimation)

Si el DAG es correcto, estímalo conjuntamente, nos podemos saltar reglas de Pearl 
Se puede "condicionar" por variables no observadas, o por colliders


## 7. Causal Forests (fuera de tiempo)
