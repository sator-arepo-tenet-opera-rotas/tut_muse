==Mathematical formulation==
The mathematical formulation of traces allows for a model of memory as an ever-growing matrix that is continuously receiving and incorporating information in the form of a vectors of attributes. Multiple trace theory states that every item ever encoded, from birth to death, will exist in this matrix as multiple traces. This is done by giving every possible attribute some numerical value to classify it as it is encoded, so each encoded memory will have a unique set of numerical attributes.

===Matrix definition of traces===
By assigning numerical values to all possible attributes, it is convenient to construct a [[column vector]] representation of each encoded item. This vector representation can also be fed into computational models of the brain like [[neural networks]], which take as inputs vectorial "memories" and simulate their biological encoding through neurons.

Formally, one can denote an encoded memory by numerical assignments to all of its possible attributes. If two items are perceived to have the same color or experienced in the same context, the numbers denoting their color and contextual attributes, respectively, will be relatively close. Suppose we encode a total of ''L'' attributes anytime we see an object. Then, when a memory is encoded, it can be written as '''m<sub>1</sub>''' with ''L'' total numerical entries in a column vector:

::<math>\mathbf{m_1} = \begin{bmatrix} m_{1}(1) \\ m_{1}(2) \\ m_{1}(3) \\ \vdots \\m_{1}(L) \end{bmatrix} </math>.

A subset of the ''L'' attributes will be devoted to contextual attributes, a subset to physical attributes, and so on. One underlying assumption of multiple trace theory is that, when we construct multiple memories, we organize the attributes in the same order. Thus, we can similarly define vectors '''m<sub>2</sub>''', '''m<sub>3</sub>''', ..., '''m<sub>n</sub>''' to account for ''n'' total encoded memories. Multiple trace theory states that these memories come together in our brain to form a memory matrix from the simple concatenation of the individual memories:

::<math>\mathbf{M} = \begin{bmatrix} \mathbf{m_1} & \mathbf{m_2} & \mathbf{m_3} & \cdots & \mathbf{m_n} \end{bmatrix} 
= \begin{bmatrix} m_{1}(1) & m_{2}(1) & m_{3}(1) & \cdots & m_{n}(1) \\ m_{1}(2) & m_{2}(2) & m_{3}(2) & \cdots & m_{n}(2) \\ \vdots & \vdots & \vdots & \vdots & \vdots \\m_{1}(L) & m_{2}(L) & m_{3}(L) & \cdots & m_{n}(L)\end{bmatrix} </math>.

For ''L'' total attributes and ''n'' total memories, '''M''' will have ''L'' rows and ''n'' columns. Note that, although the ''n'' traces are combined into a large memory matrix, each trace is individually accessible as a column in this matrix.

In this formulation, the ''n'' different memories are made to be more or less independent of each other. However, items presented in some setting together will become tangentially associated by the similarity of their context vectors. If multiple items are made associated with each other and intentionally encoded in that manner, say an item '''a''' and an item '''b''', then the memory for these two can be constructed, with each having ''k'' attributes as follows:

::<math>\mathbf{m_{ab}} = \begin{bmatrix} a(1) \\a(2) \\ \vdots \\a(k) \\b(1) \\b(2) \\ \vdots \\b(k) \end{bmatrix} = \begin{bmatrix} \mathbf{a} \\ \mathbf{b} \end{bmatrix} </math>.

===Context as a stochastic vector===
When items are learned one after another, it is tempting to say that they are learned in the same temporal context. However, in reality, there are subtle variations in context. Hence, contextual attributes are often considered to be changing over time as modeled by a [[stochastic process]].<ref name=Estes>{{cite book| vauthors = Estes WK |title=Component and pattern models with markovian interpretations. studies in mathematical learning theory|year=1959|publisher=Stanford University Press|location=Stanford, CA}}</ref> Considering a vector of only ''r'' total context attributes '''t<sub>i</sub>''' that represents the context of memory '''m<sub>i</sub>''', the context of the next-encoded memory is given by '''t<sub>i+1</sub>''':

::<math>\mathbf{t_{i+1}(j)} = \mathbf{t_{i}(j) + \epsilon(j)}</math>

so, 

::<math>\mathbf{t_{i+1}} = \begin{bmatrix} t_i(1)+\epsilon(1) \\t_i(2)+\epsilon(2) \\ \vdots \\ t_i(r)+\epsilon(r) \end{bmatrix}</math>

Here, '''ε(j)''' is a random number sampled from a [[Gaussian distribution]].

===Summed similarity===
As explained in the subsequent section, the hallmark of multiple trace theory is an ability to compare some probe item to the pre-existing matrix of encoded memories. This simulates the memory search process, whereby we can determine whether we have ever seen the probe before as in recognition tasks or whether the probe gives rise to another previously encoded memory as in cued recall.

First, the probe '''p''' is encoded as an attribute vector. Continuing with the preceding example of the memory matrix '''M''', the probe will have ''L'' entries:

::<math>\mathbf{p} = \begin{bmatrix} p(1) \\ p(2) \\ \vdots \\p(L) \end{bmatrix}</math>.

This '''p''' is then compared one by one to all pre-existing memories (trace) in '''M''' by determining the [[Euclidean distance]] between '''p''' and each '''m<sub>i</sub>''':

::<math>\left \Vert \mathbf{p-m_i} \right \| = \sqrt{\sum_{j=1}^L (p(j)-m_i(j))^2}</math>.

Due to the stochastic nature of context, it is almost never the case in multiple trace theory that a probe item exactly matches an encoded memory. Still, high similarity between '''p''' and '''m<sub>i</sub>''' is indicated by a small Euclidean distance. Hence, another operation must be performed on the distance that leads to very low similarity for great distance and very high similarity for small distance. A linear operation does not eliminate low-similarity items harshly enough. Intuitively, an [[exponential decay]] model seems most suitable:

::<math>similarity(\mathbf{p,m_i}) = e^{-\tau \left \Vert \mathbf{p-m_i} \right \|} </math>

where '''τ''' is a decay parameter that can be experimentally assigned. We can go on to then define similarity to the entire memory matrix by a summed similarity '''SS(p,M)''' between the probe '''p''' and the memory matrix '''M''':

::<math>\mathbf{SS(p,M)} = \sum_{i=1}^n e^{-\tau \left \Vert \mathbf{p-m_i} \right \|} = \sum_{i=1}^n e^{-\tau \sqrt{\sum_{j=1}^L (p(j)-m_i(j))^2}}</math>.

If the probe item is very similar to even one of the encoded memories, '''SS''' receives a large boost. For example, given '''m<sub>1</sub>''' as a probe item, we will get a near 0 distance (not exactly due to context) for i=1, which will add nearly the maximal boost possible to '''SS'''.  To differentiate from background similarity (there will always be some low similarity to context or a few attributes for example), '''SS''' is often compared to some arbitrary criterion. If it is higher than the criterion, then the probe is considered among those encoded. The criterion can be varied based on the nature of the task and the desire to prevent [[false alarms]]. Thus, multiple trace theory predicts that, given some cue, the brain can compare that cue to a criterion to answer questions like "has this cue been experienced before?" (recognition) or "what memory does this cue elicit?" (cued recall), which are applications of summed similarity described below.
