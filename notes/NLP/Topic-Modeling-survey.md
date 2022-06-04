# Topic Modelling Meets Deep Neural Networks: A Survey

**Definition:** A topic model is applied to a collection of
documents and aims to discover a set of latent topics, each of which describes an interpretable semantic concept. 


## Previous works

+ **Bayesian probabilistic topic models (BPTMs)** have been the most popular and successful series f models. However it has some disadvantages: 
  + its inference process usually needs to be customised accordingly and the inference complexity may grow significantly as the model complexity grows. Unfortunately 
    $\to$ it is also hard to automate the design of the inference processes
  + Hard to scale efficiently on large text collection or to leverage parallel computing facilities like GPUS
  + It is usually inconvenient to integrate BPTMs with other deep neural networks (DNNs) for joint training
## Background 
*The most important idea of a topic model is the modelling of the three key entities: **document**, **word**, and **topic**.*
+ The task for a topic model is to learn the latent variables of $T$ and $Z$ from the observed data $D$. More formally, a topic model learns a projection parameterised by $\theta$ from a document’s data to its topic distribution: $Z = \theta(b)$ and a set of global variables for the word distributions of the topics: $T$.

## Evaluation
**1. Predictive accuracy**: the
log-likelihood of a model on held-out test documents. ex: calculate perplexity,  which captures how surprised a model is of new (test) data and is inversely proportional to average log-likelihood per word.
+ Problems: 
  + As *topic models are not for
predicting unseen data but learning interpretable topics and
representations of seen data* , predictive accuracy does not reflect the main use of topic models.
  + Predictive accuracy does not capture topic quality. Predictive accuracy and human judgement on topic quality are often not correlated, and even sometimes slightly anti-correlated
  + The estimation of the predictive probability is usually intractable for Bayesian models and different papers may apply different sampling or approximation techniques
**2. Topic Coherence**: Evaluate the coherence between a topic's most representative words 
  + advantages: inline with human evaluation of topic interpretability. 
  + Disadvantages: various formulation $\to$ hard to compare methods.
**3. Topic Diversity**: measures how diverse the discovered topics are. $\to$ It is preferable that the topics discovered by a model describe different semantic topical meanings.
**4. Downstream Application Performance**: The topic distribution $z$ of a document learned by a topic model can be used as the semantic representation of the document, which can be used in document classification, clustering, retrieval visualization, and elsewhere. 
## Recent Methods
+ Auto-encoder (VAE - NTMs): need answer 2 key questions:
  + Different from other applications $\to$ How to deal with such data 
  + 

