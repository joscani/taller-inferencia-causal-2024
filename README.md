# Taller Inferencia Causal desmitificada. Jornadas de R. Sevilla

Material para el taller de inferencia causal para las XIV Jornadas de R Hispano

Gran  parte del material viene del estupendo libro online [Causal inference in R](https://www.r-causal.org/). 

Yo comentaré a mi manera las cosas que allí se cuenta y aportaré en la medida de lo posible cómo sería de forma bayesiana


# Índice 

## 0. Qué es esto de la inferencia causal

Dos clases de preguntas causales

* Efecto de las causas. El efecto de una intervención. 
*  Causas de los efectos. Qué ha podido ser la causa de esto?

## 1. A jugar !!

Ejemplo completo aunque no se entienda de lo que se hace en inferencia causal. 

1. Ains, los mosquitos, que chungos son 
2. Especificar pregunta causal
3. Explicitar nuestras asunciones, por ejemplo con un diagrama causal
4. Modelar las asunciones
5. Diagnóstico del modelo 
6. Estimar el efecto causal
7. Análisis de sensibilidad. 

## 2. Potential outcomes

Exponer el principal problema de la inferencia causal, que es la imposibilidad  de tener contrafactuales a nivel individual


## 3. Supuestos para poder hacer estas cosas de la inferencia causal

* Alguno obvio. Causa ha de ser anterior al efecto
Cómo solventar parcialmente el problema fundamental? 

* Consistencia (igual que SUTVA)
* Intercambiabilidad _Exchangeability_
* Positividad
* SUTVA 
  * No interferencia
  * Valor único. No hay tratamiento A diferente para una observación y otro para otra
* Ignorabilidad. No hay variables de confusión no medidas. Laxo


## 4. RCT . ¿Se puede hacer siempre? 

* RCT es el gold standard, pero a veces no se puede

En el ejemplo de la red de mosquito no se puede, porque no puedo elegir gente al azar
y a unos obligarles a no tener red moquitera. Chiste negro no contar.  Quizá en la Alemania nazi deberían haber aprovechado
para hacer inferencia causal

Incluso si podemos hacer RCT, muchas de las técnicas mejoran la precisión de la estimación en ese caso

## 5. Pensemos en el DAG

Ciencia antes que estadística. 

* Uso del DAG para hacer explícitas las asunciones. 

* Nomenclatura, puede que nueva para algunos. 
    * Forks
    * Mediators
    * Colliders
    
* Causal quartet

* Reglas de Pearl, (backdoor, frontdoor, etc), que nos pueden servir para identificar
qué variables hemos de considerar, supuesto correcto el DAG. 


## 6. Técnicas.

Son sólo técnicas, lo importante es lo de antes

* Queremos acercarnos a lo que es un RCT, qué se puede hacer desde perspectiva clásica frecuentista.
 * Identificar variables con reglas de Pearl, uso de daggitty
 * Propensity Score Matching
 * Inverse Probability Weighting
 * Meta-learners
 * G-estimation ( esto nos sirve en frecuentista y en bayesiano)


## Apéndice . Oye, que yo soy bayesiano

Usando el DAG y técnicas bayesianas es todo más natural y sencillo. 
"La inferencia causal no es más que predecir el efecto de la intervención" (es lo que se hace con G-estimation)

Si el DAG es correcto, estímalo conjuntamente, nos podemos saltar reglas de Pearl 
Se puede "condicionar" por variables no observadas, o por colliders


## 7. Causal Forests y metalearners (Para otro taller)


