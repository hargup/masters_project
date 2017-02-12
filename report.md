---
title: 'Legal Safeguards in Algorithmic Decision Making'
keywords: "law, algorithmic fairness, machine learning, constitution of India"
abstract: |
    From face recognition to hiring, recent years have a growth of use of
    machine learning in large areas of human endeavor. With the rise and
    ubiquity of algorithms, we are also seeing that algorithms are not living
    up to their promise. They are found to only reflect the existing bias and
    discrimination found in today's society but also exaggerate it. There is a
    growing literature which trying to classify, detect and rectify various
    kinds of discriminations which can be found in machine learning
    applications, who have developed various formalized notions of fairness. In
    this work we take one such formalization and try to adapt it in the context
    of equality and anti-discrimination provisions in Constitution of India so
    that it can be give force of law.
thanks: |
    I would like to thank **Dr. PVSN Murthy** and **Prof. Shreya Matilal** for
    their continued guidance, support and supervision. I thank Department of Mathematics
    and our faculty advisor **Dr. G P Raja Shekhar** for allowing me to carry out
    inter disciplinary research. I also thank Kumar Krishna Agarwal and Shivam Vats
    for insightful conversations.
author: Harsh Gupta
bibliography: fairness.bib
csl: ieee-with-url.csl
...

# Introduction


Recent year have seen an exponential rise in the use of machine learning and
algorithmic systems in almost all domains, including very "human" aspects of
human society. Now algorithmic systems suggests us which music should we listen
to, which movie to watch, which news article is worth reading, which resumes to
forward to the hiring manager, who should be given admission and even who
should be given a larger sentence for a crime. Historically some of these
areas, like employment, education and crime have seen a lot of contention
regarding bias and discrimination.

Often algorithmic systems are projected as something which is neutral and has
the ability to fix human bias. <!--[Citation]--> But recent experiences have been
shown that they can not only reflect human biases but also exaggeration it.
Large amount of literature is emerging which brings out more of these biases,
finds out why these biases occur and how to tackle them. These algorithms takes
decisions in real world, affecting people real people in real ways, therefore
we believe their behavior needs to regulated to prevent harm and the legal
notions of equality and anti-discrimination need to built into the machine
learning systems. In order to do so we need to frame these concepts in ways
such that machines can understand and enforce them.

The first step towards the goal is to formulate these notions as abstract
mathematical concepts so that machines can reason about them, the second step
is fit into the legal framework. Our work looks at a very recent formulation of
fairness in terms of mapping between metric spaces and tries to adapt it for
Article 14 and Article 15 of The Constitution of India.


# Motivating Examples

## Racial in Crime Risk Assessment


Some jurisdictions in the United States use a software system to assess the
risk of a re-offending by an offender. A study by ProPublica found that though
the accuracy of the system for whites and blacks was similar, the type of error
they make for different races are very different. Blacks are almost twice as
likely as whites to be labeled a higher risks but not actually re-offend. The
system made the opposite mistake for whites. [@angwin_machine_2016]

| Error type                                | White | Black |
| --                                        | --    | --    |
| Labeled Higher Risk, But Didn’t Re-Offend | 23.5% | 44.9% |
| Labeled Lower Risk, Yet Did Re-Offend     | 47.7% | 28.0% |

This particular reported has generated wide response, including rebuttal from
Northpoint, the company which makes the risk assessment software and
rebuttal of rebuttal from ProPublica. The main argument from Northpoint's
side is that rate of violent crimes is higher among blacks directly leads to
asymmetry in the two error rates and correcting for the disparity in error
rates will lead to fair treatment to white inmates [@_computer_2016]. Recent
literature, has suggested that it might be impossible to achieve certain notions
of fairness without compromising on others. [@kleinberg_inherent_2016]

## Blacks being tagged as Gorillas

Users found that in a Machine Learning based image tagging system in Google
Photos produced offensive labels, tagging black people in photos as "gorillas".
[@_google_2015] In a similar example, flickr was found to tag a black person
as 'Ape' [@_flickr_2015] and in 2009 it was seen that when HP's web cam wasn't
able to recognize black faces when it was easily able to track white ones
[@frucci_hp_2009] Though there are technical explanation for these behaviors of the
algorithms, Face recognition techniques are used widely to identify offenders
and error or bias in these systems can lead to loss of reputation and
livelihood of innocent people. [@kofman_how_2016]

## Occupational Gender stereotypes in Google Images

The current society has large amount of gender bias with regards to
occupations. It was found that Google Image search results exaggerate the
existing gender bias in occupation. This is important because representation of
gender in image search results shifts people's perception about real world
distribution. [@kay_unequal_2015]


## Staples Dynamic Pricing

An online shopping store in US, Staples dynamically price items for customers
on the basis of their browsing history, location from the nearest competitor store
and other parameters. A study by The Wall Street Journal found that the pricing
scheme worked negatively for low-income households as they are more likely to
live outside the core of the city. This considered as an unintended side effect
of the pricing scheme. [@valentino-devries_websites_2012]

<!-- Find out about price discrimination laws in India -->

## Job Advertisements

A study on effects of web tracking on advertisements by Google found that
setting the gender to female resulted in fewer instances of advertisements
related to high paying jobs. [@datta_automated_2015]


# Overview of reasons of Biases


## Poorly Collected or Poorly Selected Data

Good algorithms require good data to work on it. The source of data can have
inherent biases, for example the typical editor of Wikipedia is someone who is
White, college educated, western and male [@_wikipedia_2010] [@lam_wp:_2011].
The content of wikipedia also under represents non western population of the
world. [@graham_digital_2015]

The data get corrupted while handing and transformation, or though bugs in
software [@hrala_excel_2016].

The process of collecting data can also introduce certain bias in the data, for
example if certain data is collected through online form, people with low
access to the internet are likely to missing from the data, and these people
are also more likely to be low income, less educated, non english speaking and
from depressed race and caste. The errors introduced through selection process
can be very subtle, such disparities which are often under appreciated.


## Poor Algorithm

Even if the underlying data is of good quality and represents the population
well, the design of the algorithm might introduce certain biases in the result.
One example such effects is called uncertainty bias.

The uncertainty associated with a subpopulation in data has inverse relation
with the sample. In cases the algorithmic system takes decisions
conservatively, uncertainty bias can lead to inferior result for population
with lower sample, even if everything else remains same.

To illustrate this consider you have a sample 1000 people, 900 white and 100
black and all of them have same likelihood of defaulting on a loan 5 %, and you
give loan to any with a default rate of less 10%. Now if you give loans
conservatively (if you think chances of someone defaulting is between 3 to 8 %
then you'll consider defaulting rate to be 8%) you won't give loans to any of
the black folks and to every white folk and that because their sample size
is smaller the uncertainty associated with black sample is higher than the
white sample. [@goodman_european_2016]


# Formalizing Notions of Fairness and Non Discrimination

In the literature of discrimination aware machine learning, researchers have
used various definitions of fairness which mutually exclusive at times. For
analysis of anti-discrimination provisions in The Constitution of India we
adapt a framework developed by Friedler et. al. [@friedler_im_2016]

Because their framework is central to our discussion on Formalization of Article
14 and 15 of Constitution of India we reproduce a large section of their paper
here.

For the purpose of this report we will call the framework as framework of
construct space.

## Construct Space, Observed Space and Decision Space

In framework of construct space we view the task of producing a decision
algorithm as finding a map from the true characterises of a person at a given
time, called construct space, to a decision variable in the space of possible
decisions called decision space. Formally,

Construct space represents the true features of the individuals which we would
like to use these features might contain attributes like intelligence,
skills in the area, ability to work in team, communication ability etc. But
because these attributes aren't always well defined, and very hard or
impossible to observe directly we see a manifestation of these attributes in
form of observable characteristics like GPA, scores on standardized tests,
degrees obtained, etc. This space of observable attributes is called observe
space. Formally

**Definition** _The construct space is a metric space $CS = (P, d_p)$
consisting of individuals and a distance between them. It is assumed that the
distance $d_p$ correctly captures closeness with respect to the task._

**Definition** _The observed space with respect to the task at hand, is a metric space $OS
= ( \hat{P}, \hat{d})$. We assume an observation process $g:P \rightarrow \hat{P}$ that generates an entity
$\hat{p} = g(p)$ from a person $p \in CS$_

And
**Definition** _A decision space is a metric space $DS = (O, d_O)$, where $O$
is a space of outcomes and $d_O$ is a metric defined on $O$. A task $T$ can be viewed
as the process of finding a map from $P$ or $\hat{P}$ to $O$._


<!-- Clarify the examples -->
Then they take the informal understanding of fairness that similarly situation
people should be treated similarly. In terms present framework, it means that
two persons who are close in the construct space should be close in decision
space. Defined formally as


**Definition** _A mapping $f : CS \rightarrow DS$ is said to be fair if objects that are close in $CS$ are
also close in $DS$. Specifically, fix two thresholds $\epsilon, \epsilon'$. Then $f$ is defined as_
($\epsilon, \epsilon$)- fair if for any $x, y \in P$,
$$
dP(x, y) \leq \epsilon \implies d_O(f(x), f(y)) \leq \epsilon'
$$


Because, the mapping from Construct Space which is largely unknown. We need to
make assumptions about the mapping from Construct Space to Observation Space.
One such

Hence, assumptions is introduced about mapping from Construct Space to
Observation Space. One such assumption is that Observation space is a good
proxy for Construct Space, in other words two people who are close in construct
space are also close in observation space. Friedler et. al. call this _what you
see is what you get (WYSIWYG)_ axiom.

**Axiom** (WYSIWYG) There exists a mapping $f : CS \rightarrow OS$ such that the distortion $\rho_f$
is at most $\epsilon$ for some small $\epsilon > 0$. Or equivalently, the
distortion $\rho_f$ between $CS$ and $OS$ is at most $\epsilon$.

Distortion $\rho_f$ of $f: X \rightarrow Y$ for metric spaces $(X, d_X)$ and
$(Y, d_Y)$ is defined as the smallest value such that for all $p, q \in X$
$$
|d_X(p, q) - d_Y(f(p), f(q))| \leq \epsilon
$$.

Under this axiom, Friedler et. al. defines Individual fairness mechanism as

**Definition** Fix a tolerance $\epsilon$. A mechanism $IFM_{\epsilon}$ is a
mapping $f : OS \rightarrow DS$ such that for all $\rho_f \leq \epsilon$

Unfortunately in many real world applications WYSIWYG axiom doesn't hold true.
Due to historical, cultural and other reasons the mapping of $CS$ to $OS$ is
more distorted for individuals belonging to certain groups than other
individuals.

This dispositional skew is called structural bias


**Definition** _(Group fairness mechanism (GFM)). Let X be partitioned into groups $X_1, X_2,
\dots$
as before. A rich mapping $f : OS \rightarrow DS$ is said to be a valid group fairness
mechanism if all groups are treated equally. Specifically, fix $\epsilon$. Then $f$ is
said to be a $GFM_{\epsilon}$ if for any $i, j$ and a group distance function $W$, $W_{d_O} (Xi,Xj) \leq \epsilon$_

As an interesting result, Friedler et. al. showed that if systemic bias is
present it is impossible to achieve both Individual fairness mechanism and
Group fairness mechanism.

Another important result form Friedler et. al. is that Individual Fairness
Mechanism is impossible if the decision space is discreet. To understand the
result intuitively, consider a test where passing marks are 30 out of 100, there
is one student who gets 31 marks and is passed and there is another student who
got 29 marks and is failed. In terms of marks both the students are similarly
situated in observation space but are far away in decision space. So wherever
there is a decision where everyone is not given the same treatment, there will
exist two people who are similarly situated but gets very different results,
one just inside the decision boundary and another just outside it.

Numerous real world decisions are discreet and binary, to hire or not
to hire, to give admission or not to give admission, to give loan or not to
give loan. A definition of fairness where it is impossible to fair in so many
application areas isn't a very useful definition. Hence, we slightly modify the
Individual Fairness Mechanism for binary decisions by considering decision
scores instead of actual decisions. Decision Score is real number assigned to
every individual who is considered for a particular decision and then the
actual decision is done on the basis of a cut off in the decision score space.
Sometimes the decision score is explicitly part of the decision making process.
For example Indian Institute of Technology conduct a Nationwide test called
Joint Entrance Exam and students are admitted only on the basis of the rank
they obtain in the test. In cases such score is not explicitly part of the
system we consider decision score to the probability that a certain decision
will be made for the individual.


<!-- If we know the algorithm and if it is not a random process, it doesn't
make sense to talk in terms of probabilities -->

**Definition** _Decision Score Space $DSS = ([a, b], d)$ where $a, b \in R, b \textgreater{} a$ and $d$
is Euclidean distance._


**Definition** Binary Individual Fairness Mechanism: $f(g(.))$ where $DS = (\{0,
1\}, d_O)$, $g: OS \rightarrow DSS$ such that $\rho_f \textgreater{} \epsilon$
and $f: DSS \rightarrow DS$ where for all $x \in DSS$ $f(x) = 0, x \leq z$ and
$f(x) = 1, x \textgreater{}  z,  a \leq z \leq b$


# Fairness and anti-discrimination in The Constitution of India

<!-- I can talk about the historical context of the fairness provisions -->

Part of III of The Constitution of India specifies the Fundamental Rights given
to every citizen of India. Of then Article 14 describes right to equality,
Article 15 formulates the anti-discrimination provisions and Article 16 talks
about anti-discrimination in terms of public employment by the government.
Though these provisions apply only to actions by State, these cover a large
portion real world issues which can occur though machine discrimination.

Corporations largely owned and funded by the Government are also covered under
these provisions.

## Article 14

Article 14 of The Constitution gives every citizen right to equal treatment
before law and it says:

\begin{shaded*}
The State shall not deny to any person equality before law or equal
protection of the laws withing the territory of India.
\end{shaded*}

Here law is understood as any action by the State and not just statutory law.
One of the widely used test to determine equality under 14 is called test of
reasonable classification.

Equality here doesn't mean that every citizen should be treated in the exact
same matter but is understood as similarly situated persons should be treated
similarly. This notion if equality is similar to the one used by Friedler et.
al. To determine when State can make different treatment, the Courts have
formulated what is called the test of

reasonable classification. The State can
treat two persons differently only if:

1. There is an intelligible differential between the two persons

2. There is an objective for the different treatment and the different treatment satisfies the objective.

This is not to say only the test of reasonable classification determines
equality in context of Article 14. Court have used various legal and
philosophical principles to determine when a particular action of State is to
considered equal. But test of reasonable classification is to understood as a
minimum criterion for equality.

We believe that Individual Fairness Mechanism along with Binary Individual
Fairness Mechanism described above captures the test of reasonable
classification well.
The Case of Subramanyan Swami v. Raju illustrates the importance
of using Decision Score Space instead of Decision Space. In this Subramanyan
Swami contested the age at which a person attains the status of major, which is
18 years in India. The Court said even though the age 18 is arbitrary, it is not
unreasonable, hence it does not violate Article 14.

## Article 15(1)

Article 15(1) says:

\begin{shaded*}
The State shall not discriminate against any citizen only on the grounds of
religion, race, caste, sex, place of birth or any of them.
\end{shaded*}

The word "only" is important here, Article 15(1) doesn't guarantee equality of
outcome of these different groups but says that while considering whether two
people are similarly or situated or not sex, religion, race, caste or place of
birth.

In terms of the formalization we did above, Article 15(1) says that the
distance function in $OS$ should be invariant of these groups.

As it has been widely studied in the context of racial bias in United States,
ignoring the race doesn't eliminate racial discrimination as wide array of
useful information, from someone's pin code to the name is correlated with
race. What is not clear is that to extent is Article 15(1) forces one to
normalize these parameters in terms of race.


Both Article 14 and Article 15(1) works towards ensuring individual fairness
mechanism but as we have discussed in the section above doing so disallows us
to work towards group level fairness. To resolve this conflict provisions to
Article 15(1) and 15(2), that is
15(3),15(4) and 15(5) allows state to override individual fairness mechanism to
ensure group level fairness. They read as follows:

\begin{shaded*}
(3) Nothing in this article shall prevent the State from making any special
provision for women and children.

(4) Nothing in this article or in clause (2) of article 29 shall prevent the
State from making any special provision for the advancement of any socially or
educationally backward classes of citizens or for the Scheduled Castes and the
Scheduled Tribes.

(5) Nothing in this article or in sub-clause (g) of clause (1) of article 19
shall prevent the State from making any special provision, by law, for the
advancement of any socially and educationally backward classes of citizens or
for the Scheduled Castes or the Scheduled Tribes in so far as such provisions
relate to their admission to educational institutions including private
educational institutions, whether aided or unaided by the State, other than the
minority educational institutions referred to in clause (1) of article 30.

\end{shaded*}



# Summary and Conclusion

In Summary we state that our modified Binary Individual Fairness Mechanism along
with Individual Fairness Mechanism captures the essence of test of reasonable
classification under article 14 and anti-discrimination under Article 15(1).

# Discussion and Further Research

Future studies should look take up a deeper study of the case laws and analyze
how the formal notions of fairness and anti-discrimination applies in these
circumstances.

# References
