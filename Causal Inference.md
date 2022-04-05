# Causal Inference➡️

Created: January 23, 2022 9:46 PM
Property: https://www.bradyneal.com/causal-inference-course
Property 1: https://www.youtube.com/watch?v=5x_pPemAVxs&list=PLoazKTcS0RzZ1SUgeOgc6SWt51gfT80N0&index=2&t=91s
Property 2: https://web.archive.org/web/20170910225539/https://www.stats.ox.ac.uk/~lienart/gml15_causalinference.html
Property 3: https://medium.data4sci.com/causal-inference-part-xi-backdoor-criterion-e29627a1da0e
Updated: April 1, 2022 11:01 PM

## Lecture 1: Introduction

- **Definition of Causal inference:** Inferring the effects of one thing on the other thing.
- **Two different Theorem**
    - Potential Outcome
        
        $$
        \text{Causal effect}: Y_i(1)-Y_i(0)
        $$
        
        - Neyman: Randomized trial
        - Rubin: Observational research
    - Directed Acyclic Graph
        - Pearl:
            
            $$
            P(X)=\prod _{j=1}^n (X_j|pa_j)
            $$
            
            ![Untitled](Causal%20Inf%206c27c/Untitled.png)
            
        - Motivating Example**:** Simpson’s paradox
            - which one to choose?
                
                ![Untitled](Causal%20Inf%206c27c/Untitled%201.png)
                
            - scenario 1:
                
                C: condition   T: treatment    Y: outcome
                
                In this case, B is a better choice, because the higher total 19% mortality  came from severe conditions of patients. In this case we make our decision based on the subgroup’s data.
                
                ![Untitled](Causal%20Inf%206c27c/Untitled%202.png)
                
            - scenario 2:
                
                We look at total number because this would take the condition transition into account. We choose A.
                
                ![Untitled](Causal%20Inf%206c27c/Untitled%203.png)
                

## Lecture 2: Potential outcomes

- Definition: **Potential outcome and causal effects**
    
    $$
    \text{Causal effect}: Y_i(1)-Y_i(0)
    $$
    
    - Note that the definition of causal effects does not depend on the actual
    treatment or action taken！
    
    Some terminology and relationship:
    
    ***T***: observed treatment
    
    ***Y***: observed outcome
    
    i: stands for an individual or unit
    
    Y_i(1): potential outcome under treatment
    
    Y_i(0): potential outcome under no treatment
    
    $$
    Y_i = T(Y_i(1))+(1-T)(Y_i(0))
    $$
    
    - This equation linked the ‘observed outcome’ and the ‘potential outcome’
    - The potential outcomes exist in a hidden state prior to treatment receipt, and receiving treatment reveals one of them and leaves the other one hidden.
- Fundamental problem of causal inference: cannot observe outcome after treatment and no treatment at the same time
    - can also be intepreted as missing data problem
        
        ![Untitled](Causal%20Inf%206c27c/Untitled%204.png)
        
    - observed: factual; unobserved: counterfactual
    - So we introduce the **Average Treatment Effect(ATE)**:
        
        $$
        \begin{align}&E[Y_i(1)-Y_i(0)]\\&=E[Y(1)]-E[Y(0)]\\ &\neq E[Y|T=1]-E[Y|T=0]\end{align}
        $$
        
        Y(t): population-level potential outcome
        
        (2) doesn’t equal to (3) because we have **confounding association**. (3) is just a measure of association, and it mixed confounding association and causal association.
        
    - Confounding association
        
        The principle of confounding; the confounder makes the exposure more likely and in some way independently modifies the outcome, making it appear that there is an association between the exposure and the outcome when there is none, or masking a true association
        
        ![Untitled](Causal%20Inf%206c27c/Untitled%205.png)
        
- Correlation does not imply causation - Why?
    - Ignorability - (2): Average effects equals to associational difference(outcome is independent to treatment assignment)
        
        $$
        (Y(1),Y(0))\perp T
        $$
        
        $$
        \begin{align}&E[Y(1)]-E[Y(0)]\\&=E[Y(1)|T=1]-E[Y(0)|T=0]\\ &= E[Y|T=1]-E[Y|T=0]\end{align}
        $$
        
        ![Untitled](Causal%20Inf%206c27c/Untitled%206.png)
        
    - Exchangeability(same as ignorability)
        
        We swap groups, get same expectation value:
        
        $$
        E[Y(1)|T=1]=E[Y(1)|T=0]=E[Y(1)]
        $$
        
        ![Untitled](Causal%20Inf%206c27c/Untitled%207.png)
        
    - Identifiability:  Causal quantities is identifiable if we can compute it from a purely statistical quantity.
    
    $$
    \begin{align}&E[Y(1)]-E[Y(0)] \text{ Causal Quantities}\\ &= E[Y|T=1]-E[Y|T=0] \text{ Statistical Quantities}\end{align}
    $$
    
- **RCT**
    
    RCT can give us exchangeability, thus identifiability. It’ll eliminate confounding association
    
    if don’t have any confounding association:
    
    - T cannot have any causal parents
    - groups are comparable
    - and when there is no confounding, causal effect is easy to measure:
        
        $$
        E[Y(1)]-E[Y(0)]= E[Y|T=1]-E[Y|T=0]
        $$
        
        ![Untitled](Causal%20Inf%206c27c/Untitled%208.png)
        
    - Conditional exchangeability from conditional independent:
        
        ![Untitled](Causal%20Inf%206c27c/Untitled%209.png)
        
        $$
        \begin{align}&E[Y(1)-Y(0)|X]\\&=E[Y(1)|X]-E[Y(0)|X]\\ &=E[Y(1)|T=1,X]-E[Y(0)|T=0,X]\\&= E[Y|T=1,X]-E[Y|T=0,X]\end{align}
        $$
        
        So it we’d like to calculate ATE, we can use:
        
        $$
        \begin{align}&E[Y(1)-Y(0)]\\&=E_XE[Y(1)|X]-E[Y(0)|X]\\&= E_X[E[Y|T=1,X]-E[Y|T=0,X]]\end{align}
        $$
        
        - To make this work, we have some assumptions:
            1. Positivity assumption:
                - The question is, if we have some x values, that all units with those values were treated or not treated, we are not able to evaluate causal effect in this way.
                - Or we can see it in the perspective of overlapping way:
                    
                    ![Untitled](Causal%20Inf%206c27c/Untitled%2010.png)
                    
                    and this suffers a lot from high dimensions
                    
                    ![Untitled](Causal%20Inf%206c27c/Untitled%2011.png)
                    
                    Extrapolation
                    
                    ![Untitled](Causal%20Inf%206c27c/Untitled%2012.png)
                    
            2. No interference assumption:
                - My potential outcome should only depend on my own treatment rather than influenced by other people’s treatment
                    
                    ![Untitled](Causal%20Inf%206c27c/Untitled%2013.png)
                    
            3. Consistency: 
                - No multiple versions of treatments
                    
                    ![Untitled](Causal%20Inf%206c27c/Untitled%2014.png)
                    
            - Finally, we wrap up to understand:
                
                ![Untitled](Causal%20Inf%206c27c/Untitled%2015.png)
                
- Example
    
    ![Untitled](Causal%20Inf%206c27c/Untitled%2016.png)
    
    ![Untitled](Causal%20Inf%206c27c/Untitled%2017.png)
    
- Observational studies to measure causal effects
    
    Control for the right variables ***W, the sufficient adjustment, (**here w is C in the graph**):***
    
    $$
    E[Y(t)|W=w]=E[Y|do(T=t),W=w]= E[Y|T,w]
    $$
    
    We use w to block the confounding association from C to T
    
    ![Untitled](Causal%20Inf%206c27c/Untitled%2018.png)
    
    If we want the total effect rather than the conditional effect above, we just marginize W, take expectation of W on the E[Y|t,w]:
    
    $$
    E[Y(t)]=E[Y|do(T=t)]= E_WE[Y|T,W]
    $$
    
    Other examples of sufficient adjustment:
    
    ![Untitled](Causal%20Inf%206c27c/Untitled%2019.png)
    
    ![Untitled](Causal%20Inf%206c27c/Untitled%2020.png)
    

## Lecture 3: Causal Graph

- Motivation
    - From potential outcomes, we find the causal effect is difficult to be identified from association. We need the ignorability assumption
        - the potential outcomes, Y1 and Y0, must be jointly independent (“⊥”) of
        treatment assignment. Ignorability holds in an ideal experiment.
        - In observational studies, ignorability seldom holds on its own (i.e., without any adjustments). But it may hold within groups defined by some other variables, X. That is, (Y1,Y0) ⊥ T|X
    - But **ignorability gives little guidance as to what variables should be in X** to make T and {Y T} conditionally independent.How would we know whether ignorability holds?
- Origins
    1. Structural equation models (1930s+)
    2. Social science path models (1960s+)
    3. Bayesian networks (1980s+)
    - DAGs are seen as nonparametric structural equation models (NPSEM), which gives them a causal interpretation.
    - It is **Compatible with the potential outcomes** (Neyman-Rubin) framework.
- Elements of DAGs
    - What is DAG?:
        - DAGs are visual representations of the joint distribution of a set of variables.
    - Elements
        - **Nodes**: variables
        - **Directed arrows**: represent direct causal effects
            
            ![Untitled](Causal%20Inf%206c27c/Untitled%2021.png)
            
        - **directed acyclic graph:** no directed path can form a closed loop. In other words, the future can’t predict the past
        - **Path**: from a node to another, can be directed or undirected. Directed Path is causal path.
    - Terminology
        - **Chain fork and inverted fork**
            
            All DAGs can be constructed from just three elements—causal chains, forks, and inverted forks.
            
            ![Untitled](Causal%20Inf%206c27c/Untitled%2022.png)
            
        - **Parent and child**: nodes that have outgoing edges are parent nodes, have incoming edges are their corresponding child nodes);
        - **Ancestor and descendant**: from one onde, follow directed paths, the nodes that can be reached are its descendant
        - **Adjacency**: the nodes that are connected by edges are adjacent.
        - I**mmorality**: has two parents to a child node but the **parents are not connected.**
        - **Collider:** a vertex on a path with two incoming arrows
- Assumptions for DAG
    - Local Markov assumption:
        - Given its parents in DAG, a node X is independent of all its non-descendants
            - For example, for this graph, we have
                
                 P联合=P(x1)P(x2|x1)P(x3|x1 x2)P(x4| x1 x2 x3)
                
                $$
                P(x_1,x_2,x_3,x_4)=P(x_1)P(x_2|x_1)P(x_3|x_2,x_1)P(x_4|x_3)
                $$
                
                ![Untitled](Causal%20Inf%206c27c/Untitled%2023.png)
                
        - generalization: Bayesian network factorization:
        
        $$
        P(x_1,x_2,...,x_n) = \prod P(x_i|pa_i)
        $$
        
    - Minimality assumption
        - Adjacent nodes in DAG are dependent
    - Causal edges assumption
        
        X is said to be a cause of Y if Y can change in response to changes in X
        
        In a directed graph, every parent is a direct cause of all its children
        
    
    The minimality is already included in local markov and causal edges assumption
    
    ![Untitled](Causal%20Inf%206c27c/Untitled%2024.png)
    
- Tell Association from DAG
    
    ![Untitled](Causal%20Inf%206c27c/Untitled%2025.png)
    
    - DAGs help appreciate the **different ways statistical association** may exist between two variables X and Y:
        1. X caused Y
        2. Y caused X
        3. X and Y share a common cause
        4. The statistical association was induced by **conditioning on a common effect** of X and Y (one formal definition of selection bias)
            
            When there are multiple independent causes for an effect (i.e. a common effect), conditioning on this common effect, in other words choosing only a subset of this common effect, leads to a spurious association between those causes.
            
            - Example 1:
                
                ![Untitled](Causal%20Inf%206c27c/Untitled%2026.png)
                
            - Example 2:
                
                ![Untitled](Causal%20Inf%206c27c/Untitled%2027.png)
                
                without the observation of Grade, we cannot really say anything about the Intelligence of the student given the Difficulty of the course. When Grade is observed, Difficulty and Intelligence are not independent.(Why? if we observe Grade = C and Difficulty = Low, we tend to believe Intelligence = Low
                
- Any ways to block the associations?
    - Chain and fork
        
        ![Untitled](Causal%20Inf%206c27c/Untitled%2028.png)
        
        Independence: blocked path (condition on X_2)
        
        ![Untitled](Causal%20Inf%206c27c/Untitled%2029.png)
        
        - Proof for chain:
            
            $$
             \text{From bayesian network factorization:     } \\P(x_1,x_2,x_3)=P(x_1)P(x_2|x_1)P(x_3|x_2)\\ \text{need to prove: }P(x_1,x_3|x_2)=P(x_1|x_2)P(x_3|x_2)\\P(x_1,x_3|x_2) = \frac{P(x_1,x_2,x_3)}{P(x_2)}=\frac{P(x_1)P(x_2|x_1)P(x_3|x_2)}{P(x_2)}\\=\frac{P(x_1|x_2)P(x_2)P(x_3|x_2)}{P(x_2)}=P(x_1|x_2)P(x_3|x_2)
            $$
            
        - Proof for fork:
            
            $$
            \text{From bayesian network factorization:     } \quad \quad \quad \quad \\P(x_1,x_2,x_3)=P(x_2)P(x_1|x_2)P(x_3|x_2)\\\text{need to prove: }P(x_1,x_3|x_2)=P(x_1|x_2)P(x_3|x_2)\\P(x_1,x_3|x_2)=\frac{P(x_2)P(x_1|x_2)P(x_3|x_2)}{P(x_2)}=P(x_1|x_2)P(x_3|x_2)
            $$
            
    - Inverted Fork
        
        ![Untitled](Causal%20Inf%206c27c/Untitled%2030.png)
        
        - Conditioning on X_2 brings unblocked path,and brings X_1 and X_3 association
        - Proof:
            
            $$
            \text{Need to prove: }P(x_1,x_3|x_2)\neq P(x_1|x_2)P(x_3|x_2)\\P(x_1,x_3|x_2)=\frac{P(x_1,x_3,x_2)}{P(x_2)}\\=\frac{P(x_1)P(x_3)P(x_2|x_1,x_3)}{P(x_2)}\\=\frac{P(x_1|x_2)P(x_2)}{P(x_2|x_1)}\frac{P(x_3|x_2)P(x_2)}{P(x_2|x_3)}\frac{P(x_2|x_1,x_3)}{P(x_2)}\\=P(x_1|x_2)P(x_3|x_2)\frac{P(x_2)P(x_2|x_1,x_3)}{P(x_2|x_1)P(x_2|x_3)}
            $$
            
            ![Untitled](Causal%20Inf%206c27c/Untitled%2031.png)
            
            ![Untitled](Causal%20Inf%206c27c/Untitled%2032.png)
            
    - Extension: What is Conditioning?
        
        Conditioning may occur in the data analysis stage or in the data collection stage
        
        - Controlling (e.g. in regression)
        - Stratification (e.g. crosstabs, survival analysis, loglinear models)
        - Subgroup analysis (e.g. restrict analysis to employed women)
        - Sample selection (e.g. only collect data on poor whites)
        - Attrition, censoring, nonresponse (e.g., analyze only respondents or survivors)
- Put all the things together we got: **d-separation**
    - Let A, B, C be three sets of nodes in G. We say that A and B are d-separated given C If A ⊥ B | C holds; If A and B are d-connected (i.e., not d-separated), A not ⊥ B | C in at least one distribution compatible with DAG
        - **Probabilistic Implications:**
            
            Two variables that are d-separated along all paths given {C} are conditionally independent given {C}.
            
        - **How to check?**
            1. Identify all paths(directed and non-directed) from any vertex in A to any vertex in B
            2. Check if each path is blocked
            3. If all paths are blocked, then A is d-separated from B by C
        - **When Path is blocked?**
            1. There is a chain ...→W→..., or there is a fork ...←W→..., condition on W brings blocked path
            2. There is an Immorality, all the collider and collider’s descendants are not conditioned
        
        - Examples
            
            ![Untitled](Causal%20Inf%206c27c/Untitled%2033.png)
            
            - B ⊥ C | A?
                
                Yes
                
            - A ⊥ F | E?
                
                Yes
                
            - C ⊥ D | F?
                
                No
                
    

- References——>
    - [https://bookdown.org/jbrophy115/bookdown-clinepi/causal.html#dag](https://bookdown.org/jbrophy115/bookdown-clinepi/causal.html#dag)
    - [https://imai.fas.harvard.edu/teaching/files/DAG.pdf](https://imai.fas.harvard.edu/teaching/files/DAG.pdf)
    - [d-separation.pdf](http://web.mit.edu/jmn/www/6.034/d-separation.pdf)
    - [D-separation](https://www.andrew.cmu.edu/user/scheines/tutor/d-sep.html)
    - [https://www.stat.cmu.edu/~cshalizi/350/lectures/31/lecture-31.pdf](https://www.stat.cmu.edu/~cshalizi/350/lectures/31/lecture-31.pdf)
    - [http://bayes.cs.ucla.edu/BOOK-2K/ch3-3.pdf](http://bayes.cs.ucla.edu/BOOK-2K/ch3-3.pdf)
    - [https://www.ssc.wisc.edu/~felwert/causality/wp-content/uploads/2013/06/2-elwert_dags.pdf](https://www.ssc.wisc.edu/~felwert/causality/wp-content/uploads/2013/06/2-elwert_dags.pdf)
    - [https://www.ssc.wisc.edu/~felwert/causality/wp-content/uploads/2013/06/1-Elwert_Causal_Intro.pdf](https://www.ssc.wisc.edu/~felwert/causality/wp-content/uploads/2013/06/1-Elwert_Causal_Intro.pdf)
    - [https://business.baylor.edu//scott_cunningham/teaching/causalinf.pdf](https://business.baylor.edu//scott_cunningham/teaching/causalinf.pdf)
    - [https://scholar.princeton.edu/sites/default/files/bstewart/files/fd_princeton.pdf](https://scholar.princeton.edu/sites/default/files/bstewart/files/fd_princeton.pdf)

## Lecture 4: Causal Model

- Causal effect terminology&representation in DAG
    - do-operator and Identifiability
        - **Conditioning vs. Intervening**
            
            ![Untitled](Causal%20Inf%206c27c/Untitled%2034.png)
            
            $$
            P(Y(t)=y)==P(Y=y|do(Y=t))==P(y|do(t))\\\text{ATE: } E[Y|do(T=1)]-E[Y|do(T=0)]\\\text{Observational: } P(Y,T,X), P(Y|T=t)\\\text{    Inverventional: } P(Y|do(T=t)), P(Y|do(T=t),X=x)
            $$
            
        - Identifiability: same as we’ve discussed in potential outcome, identifiability indicates we could access causal estimand by statistical estimand
    - Modularity assumption and Truncated Factorization
        - If we intervene on a node X_i, only the mechanism P(x_i|pa_i) changes. Other mechanisms such as P(x_j|pa_j) remain unchanged.
        - Based on modularity, we can rewrite the Bayesian network factorization with intervening:
            
            $$
            P(x_1,x_2,...,x_n|do(S=s))=\prod_{i\notin S} P(x_i|pa_i)
            $$
            
    - A simple example for causal effect estimation
        - Here we’d like to identify the causal quantity:
            
            $$
            P(y|do(t))
            $$
            
        - Let’s say we have a simple DAG structure here:
            
            ![Untitled](Causal%20Inf%206c27c/Untitled%2035.png)
            
            Bayesian network factorization:
            
            $$
            P(y,t,x)=P(x)P(t|x)P(y|t,x)
            $$
            
            If we intervene on the treatment:
            
            $$
            P(y,x|do(t))=P(x)P(y|t,x)
            $$
            
            So we marginalize out x to get the causal quantity:
            
            $$
            P(y|do(t))=\sum_xP(y|t,x)P(x)
            $$
            
            If x is independent to t, we can find the above formula be arranged into:
            
            $$
            P(y|do(t))=\sum_xP(y|t,x)P(x|t)\\=\sum_xP(y,x|t)=P(y|t)
            $$
            
        - ATE: (here we assume T is a binary random variable:
            
            $$
            E[Y(1)-Y(0)]=\sum_y yP(y|do(T=1))-\sum_y yP(y|do(T=0))
            $$
            
- Backdoor Criterion
    - Backdoor paths
        - Paths that are non-causal association paths from T to Y and not blocked
    - Backdoor criterion
        - A set of variables X satisfies the backdoor criterion relative to T and Y if the following are true:
            1. X blocks all backdoor paths from T to Y
            2. X does not contain any descendants of T (exp: collider)
        - Satisfying the backdoor criterion makes X a sufficient adjustment set
    - Causal Effect
        
        if the backdoor criterion is satisfied, then the causal effect of T on Y is given by:
        
        $$
        P(Y|do(T))=\sum_xP(Y|T,X)P(X)
        $$
        
        - Proof:
            
            $$
            P(y|do(t))=\sum_xP(y|do(t),x)P(x|do(t))\\P(y|do(t))=\sum_xP(y|t,x)P(x|do(t))\text{ <- Blocked path}\\P(y|do(t))=\sum_xP(y|t,x)P(x) \text{ <- Backdoor criterion}
            $$
            
    - Relationship with Potential outcome
        - From Potential outcome:
            
            ![Untitled](Causal%20Inf%206c27c/Untitled%2015.png)
            
        - For DAG:
            
            $$
            E(Y|do(t))=E[P(y|do(t))]=\sum_xE[y|t,x]P(x)=E_xE[y|t,x]\\E[Y|do(T=1)]-E[Y|do(T=0)]=E[Y(1)-Y(0)]
            $$
            
        
        Note: This is the same as Potential outcome, but in DAGs we have more information about what variables need to be conditioned on.
        
- M-Structure and M-Bias
    - Motivation: People believe: there’s no reason not to adjust(condition) for a co-variable, and the more conditional we have the more reliable the assumption is.————- But this is not the case at least to some statisticians. They brought up a structure as follows, and aimed to prove: In some cases, adjusting on co-variate might introduce new bias into our estimation.
    - Let’s see: in this following DAG, Should we condition on X or not?
    
    ![Untitled](Causal%20Inf%206c27c/Untitled%2036.png)
    

---

---

---

- Frontdoor Criterion
    
    
    ![Untitled](Causal%20Inf%206c27c/Untitled%2037.png)
    
    Here U=unobserved confounders, M = mediator
    
    - Frontdoor criterion for M:
        1. M intercepts all directed paths from T to Y
        2. No backdoor path from T to M 
        3. All backdoor paths from M to Y are blocked by T
- Instrumental Variable
- Nonparametric Structural Equation Models
    
    Equivalence to the nonparametric structural equation models
    

## Lecture 4 - con’t: Frontdoor adjustment

- Causality recap
    
    in potential outcome, the causality (for a unit) is defined as :
    
    $$
    \text{Causal effect}: Y_i(1)-Y_i(0)
    $$
    
    in causal graph , the causality is defined as:
    
    $$
    P(y|do(t))
    $$
    
    - understand the relationship between do-operator and probability:
        
        for a graph: $A  \rightarrow B$ :
        
        $$
        P(B|do(A)) = P(B|A)\\P(A|do(B)) = P(A)
        $$
        
        An example:
        
        $$
        A: \text{Covid Cases}\\B: \text{Google Searches on "Covid"}
        $$
        
    
    they are actually talking about the same thing, the relationship is:
    
    $$
    E[Y(1)-Y(0)]\\=E[Y|do(T=1)]-E[Y|do(T=0)]\\=\sum_y yP(y|do(T=1))-\sum_y yP(y|do(T=0))
    $$
    
- Backdoor adjustment recap
    - What is this for?: **to determine what variables to adjust/condition on**
    - a simple example:
        
        ![Untitled](Causal%20Inf%206c27c/Untitled%2038.png)
        
        Here we’d like to calculate the causal effect from 4 to 5. 
        
        if we directly use the observed probability of $P(Node5 | Node4)$, we cannot truly get the $P(Node5 | do(Node4))$**.** Because the two nodes have one confounding node: Node2. Node2 will affect Node4 and Node5 simultanously.
        
        Here, the undirected path: 4→2→3→5 is called **backdoor path.** Let’s define this with a more mathematical way:
        
    - Backdoor criterion:
        
        finds out the set of variables C that allows us to do this computation
        
        ![Untitled](Causal%20Inf%206c27c/Untitled%2039.png)
        
        ![Untitled](Causal%20Inf%206c27c/Untitled%2040.png)
        
        $$
        P(Y|do(X))=\sum_ZP(Y|do(X),Z)P(Z|do(X))\\P(Y|do(X))=\sum_ZP(Y|X,Z)P(Z|do(X))\text{ <- Blocked path}\\P(Y|do(X))=\sum_ZP(Y|X,Z)P(Z) \text{ <- Backdoor criterion}
        $$
        
- Frontdoor adjustment
    
    > Backdoor adjustment is to blocks all the non-causal information that X could possibly pick up
    > 
    
    > Frontdoor adjustment is to exploit the **outgoing information from X** to derive a causal estimator.
    > 
    
    Why we need frontdoor?: **when we are unable to identify any sets of variables that obey the [Backdoor Criterion](https://medium.com/data-for-science/causal-inference-part-xi-backdoor-criterion-e29627a1da0e)** 
    
    - one example:
        
        Here, U satisfy backdoor criterion, but it is an unobserved variable, we cannot use it to calculate causal effect. We’d like to utilize the variable Z to calculate causal effect(why? because the confounder U doesn’t affect Z.)
        
        ![Untitled](Causal%20Inf%206c27c/Untitled%2041.png)
        
        Looking at the causal path, we can write:
        
        $$
        P(Y=y|do(Z=z))\\P(Z=z|do(X=x))
        $$
        
        We chain them together:
        
        $$
        P(Y|do(X))=\sum_Z P(Y|Z,do(X))*P(Z|do(X))
        $$
        
        We can find X(smoking) blocks all the back-door paths from Z(tar) into Y(cancer):
        
        $$
        P(Y|Z,do(X)) = P(Y|do(Z),do(X)) = P(Y|do(Z)) 
        $$
        
        $$
        P(Y|do(Z)) = \sum_X P(Y|Z,X)P(X)
        $$
        
        Let’s plug this back to $P(Y|do(x))$:
        
        $$
        P(Y|do(X))= \sum_Z\sum_{X'} P(Y|Z,X')P(X')*P(Z|do(X))\\=\sum_Z[\sum_{X'} P(Y|Z,X')P(X')]P(Z|X)
        $$
        
        Let’s try calculate!:
        
        ![Untitled](Causal%20Inf%206c27c/Untitled%2042.png)
        
        $$
        P(Cancer|do(X=smoker))\\=[P(Cancer|Tar,Smoker)*P(Smoker)+P(Cancer|Tar,Non Smoker)*P(Non Smoker)]*P(Tar|Smoker)+[P(Cancer|No Tar,Smoker)*P(Smoker)+P(Cancer|No Tar,Non Smoker)*P(Non Smoker)]*P(No Tar|Smoker)\\=[0.15*0.5+0.95*0.5]*0.95+[0.1*0.5+0.9*0.5]*0.05 \\= 0.5475
        $$
        
        $$
        P(Cancer|do(X=Non Smoker) = P(Cancer|Tar,Smoker)*P(Smoker)+P(Cancer|Tar,Non Smoker)*P(Non Smoker)]*P(Tar|Non Smoker)+[P(Cancer|No Tar,Smoker)*P(Smoker)+P(Cancer|No Tar,Non Smoker)*P(Non Smoker)]*P(No Tar|Non Smoker)\\= [0.15*0.5+0.95*0.5]*0.05+[0.1*0.5+0.9*0.5]*0.95 \\= 0.5025
        $$
        
        ![Untitled](Causal%20Inf%206c27c/Untitled%2043.png)
        
    - Frontdoor criterion
        
        determine which variables (like Tar in the example above) allow for this kind of computation
        
        ![Untitled](Causal%20Inf%206c27c/Untitled%2044.png)
        
        Frontdoor adjustment
        
        ![Untitled](Causal%20Inf%206c27c/Untitled%2045.png)
        

## Lecture ?: Causal Inference in Economics

[DID(2) copy.pdf](Causal%20Inf%206c27c/DID(2)_copy.pdf)

- Identification Strategies
    - RCT
    - PSM(Propensity Score Matching)
    - IV(Instrumental Variable)
    - DID(Difference in Differences)
    - SC(Synthstic Control)
    - RDD(Regression Discontinuity Design)
- **DID**
    - Basic setup
        
        ![Untitled](Causal%20Inf%206c27c/Untitled%2046.png)
        
        ![Untitled](Causal%20Inf%206c27c/Untitled%2047.png)
        
    - DID estimator
        
        $$
        \tau_{DID} = \bar Y_{1,1} - \bar Y_{1,0}-(\bar Y_{0,1}-\bar Y_{0,0})
        $$
        
        and this is the same as estimating beta3:
        
        ![Untitled](Causal%20Inf%206c27c/Untitled%2048.png)
        
    - Assumption
        - Common Trend Assumption
            
            It is actually untestable. But as a robustness check we often examine the
            parallel of pre-treatment trends.
            
            $$
            E(Y_{i1}(0)-Y_{i0}(0)|W_{it}=1)=E(Y_{i1}(0)-Y_{i0}(0)|W_{it}=0)
            $$
            
            When treatment is more of a “self-selection” process, it would be very hard to satisfy this assumption.
            
- TWFE (DID extension)
    - two-way fixed effects basic model:
        
        The DID estimator would be beta
        
        $$
        Y_{it} = \alpha+\beta D_{it}+\mu_i+\delta_t+\epsilon_{it}
        $$
        
        ![Untitled](Causal%20Inf%206c27c/Untitled%2049.png)
        
    
- DID Decomposition Theorem
    
    *The OLS estimate in a two-way fixed-effects regression is a weighted average of all
    possible two-by-two DID estimators:*
    
    ![Untitled](Causal%20Inf%206c27c/Untitled%2050.png)
    
    1. When treatment effects are homogeneous, DID estimator is ATT.
    2.  When treatment effects are heterogeneous across units, DID estimator is a variance-weighted treatment effect that is not ATT.
    3.  When treatment effects change over time, DID estimator is biased and stacked DID/event study may be more appropriate.
    
- Event Study
    
    ![Untitled](Causal%20Inf%206c27c/Untitled%2051.png)
    
- DDD
    
    The difference between two biased DID estimators will be unbiased as long as the bias is the same in both estimators, which is the common difference-in-trends assumption.
    
- Stack DID