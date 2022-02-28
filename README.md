
The above exercise has been done to highlight the importance of test sampling and how Bayes probabilities go against our intuition.

# Main Question
What is the probability someone has SARS-CoV-2 (COVID-19) if he has one positive Rapid test and then only negatives?

## Scenario :syringe:
The subject runs the following Rapid Tests in a Point-of-Care **(Important: Give attention on that detail)**:
* Test 1: Positive (+)
* Test 2: Negative (-)
* Test 3: Negative (-)
* Test 4: Negative (-)

**Assumptions**
* All the tests take care in the same time.
* All the tests are from the same brand
    
---

### Rapid Test Performance Metrics
Let's assume the the Rapid test is the [VivaDiagTM Pro SARSCoV-2 Ag Rapid Test](https://www.mmbiotech.it/en/prodotto/vivadiag-pro-sars-cov-2-ag-rapid-test-tampone-antigene-covid-rapido-confezione-da-25-tamponi-rapidi/).
* Specificity = 99.99%
* Sensitivity = 97.06%

**Test Parameters: SARS-CoV-2 Ag**
* Test Principle: Immunochromatorgraphy
* Sample Type: Nasal swab / Nasopharyngeal swab / oropharyngeal swab
* Sample Volume: 60 μl
* Test Time: 15 min
* Operation Temperature: 15-30°C
* Storage Temperature: 2-30°C
* Shelf Life: 24 months

---

## Population Prevelence
Let's assume that the target country is Greece.
  * Daily Active Cases = 200.000 ([Source](https://www.worldometers.info/coronavirus/country/greece/))
  * Greece Population = 10.72M

The population prevelance is calculated with the following formula:
```
    Covid prevelence = Daily Active Cases / Greece Population = 200.000/ 10.720.000 = 0.0186 or 1.86%
```
---

## Propability estimation maths

### Notations

**---- Hypothesis ----**

**Ho**: Disease Free

**H1**: Have Disease (SARS-CoV-2)

**---- Outcomes ----**

**+** : Positive test outcome

**-** : Negative test outcome

---

### 1st Test: Estimate the probability of has SARS-CoV-2 (H1) given a positive test (+)
P(H1 | +) = P(+ | H1) * P(H1) / P(+) (Bayes Rule)

P(H1) = 0.0186
P(Ho) = 1 - P(H1)
P(+ | H1) = Sensitivity
P(+ | Ho) = 1-Specificity
P(+) = TruePositive + FalsePositive = P(+ | H1)*P(H1) + P(+ | Ho)*P(Ho)

Propability: **P(H1 | +) = 99.45%**

--- 

### 2nd Test: Estimate the probability of has SARS-CoV-2 (H1) given a negative test (-)
P(H1 | -) = P(- | H1) * P(H1) / P(-) (Bayes Rule)

P(H1) = 0.645 (Previous test probability)
P(Ho) = 1 - P(H1)
P(- | H1) = 1 - Sensitivity
P(- | Ho) = 1 - P(+ | Ho) = 1 - (1-Specificity) = Specificity
P(-) = TrueNegative + FalseNegative = P(- | Ho)*P(Ho) + P(- | H1)*P(H1)

Propability: **P(H1 | -) = 84.39%**

etc ...

Finally, we have the following probabilities for the four sequential tests:

![title](plots/ideal_probabilities.png)


xmm... the probability for having SARS-CoV-2 looks very low after 3 sequential negative tests! Yeah no infection!!
YES this will be the outcome if the experiments have take care by experts in a laboratory environment.

BUT in a Point-of-Care location (e.g. pharmacies, doctor offices, homes,  etc.) the probability of incorrect sampling is high.

## Re-estimate the probabilities in a Point of Care

In a Point of Care, you or the person who will do the sampling of the mucus and cells will not be so finicky as a medical professional in lab.
This will play significant role in SARS-CoV-2 (COVID-19) catching. In other words, the cases of not caching the virus will be higher (False Negatives).

In our case, the metric which will be affected is the test `Sensitivity`.
Sensitivity, is the metric which describes what proportion of the actual positives is correctly identified.
(`Sensitivity = TP / (TP + FN)`, where TP: True Positive, FN: False Negative)

Let's plot the correlation between the Sensitivity and the probability of actually having SARS-CoV-2.
Also add a cut of point (vertical dash line) with the estimated `Point-of-Care Sensitivity = 0.789`, [source](https://www.healthline.com/health/how-accurate-are-rapid-covid-tests).

![title](plots/sensitivity_vs_probability.png)


Finally, we re-estimate the probabilities of the four sequential tests by using the `Point-of-Care Sensitivity = 0.789` in our formulas:

![title](plots/point_of_care_probabilities.png)

Now the results are not so clear with the probability of infected from COVID-19 being higher!!

**NOTE: The code and the plots created from the Multiple Rapid Tests Probability Estimation.ipynb**


:beers: Cheers!