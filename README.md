# Testing the Capacity of GPT-4o in Reading Math Papers:


## The Task
For my final project in the math class Machine Learning this semester I studied the famous result known as the Kolmogorov Arnold Representation Theorem. This theorem shows that all continuous multi-variable functions can be represented as a sum and composition of single variable function, specifically,
$$f(x_1,\dots,x_n) = \sum_{q=1}^{2n+1}\chi^q \left( \sum_{p=1}^n \phi^q(x_p) \right) $$
The proof of this result is very interesting and non-trivial. It happens to be a constructive proof, and the machinery that it uses is only dependent on some basic analysis knowledge. That being said, understanding the proof requires critical thinking about the underlying geometry and methods being used. Finally, literature on this proof is dense, and often not only analytical but highly abbreviated to the point that re-constructing the steps made by the authors of the proofs requires some real intelligence. For these reasons, I think that Chat-GPT is amply suited for helping aid someone in understanding of the proof, but also could struggle with understanding key steps. Bellow is my conversation with Chat-GPT4o, along with comments from me about the accuracy and value provided by Chat-GPT's responses. As a starting point, I first ask the model to try and summarize the paper at a high level. 

---

**User:**  
I need help understanding a math paper that I am reading. I will give you the paper, and first I want you to just tell me in simple but precise language what the goal of the paper is. I will then ask you clarifying questions about the steps taken in the paper and I want you to be able to explain in excruciating detail all algebraic and logical steps which the author makes. 

**ChatGPT:**  
The paper explores Hilbert’s 13th problem, which asks whether certain multivariable functions can be expressed as compositions of functions of fewer variables. Specifically, the paper focuses on a theorem by Kolmogorov and Arnold, which demonstrates that any continuous function of several variables can be expressed as compositions of continuous functions of two variables or even one variable.

The author aims to:
	1.	Provide background on Hilbert’s 13th problem and Kolmogorov-Arnold’s solution.
	2.	Present a detailed explanation and proof of the Kolmogorov representation theorem, emphasizing the construction of inner and outer functions necessary for the decomposition.

---

**My Analysis:**
This response is generally accurate, and summarizes the point of the paper well. I would have liked for the model to notice that their are two key ideas in the proof, one being to reduce the problem to a simpler one about two variable functions, and then to prove a construction for the simpler problem. If I was trying to explain the paper to someone, that fact would be a key detail to include. The model also says "or even one variable" when in fact the entire point of the proof is that it can always be decomposed to single variable functions. This highlights a slight lack of understanding on the models part. Now I want to push the model on its understanding of the math. I will do this first by asking the model to take a constructive part of the proof and make it more rigorous, testing its ability to come up with analytical though and testing its actually understanding of the problem itself. 

---

**User:**
On page 7 of the pdf in Lemma 3 the author states that for each fixed value $k$, any point $x$ in the unit interval will be contained in at least 4 of the $A_{k,1}^q$. The author presents the proof of this lemma as a wordy construction. Can you try to make this a more mathematical construction. Use common results from real analysis where necessary to justify your steps and make the construction as mathematically rigorous as possible. 

**ChatGPT:** (Some response omitted)
1.	**Divide the interval**  $[0, 1]$  into  $5k$  subintervals of equal length  $\frac{1}{5k}$:

\[
I_{i} = \left[\frac{i-1}{5k}, \frac{i}{5k}\right), \quad i = 1, 2, \dots, 5k-1, \quad \text{and } I_{5k} = \left[\frac{5k-1}{5k}, 1\right]
\]

2.	**Group the intervals cyclically** into five families  $A_{k,1}^q$ :
Assign each subinterval $ I_{i}$  to the family $ q = ((i-1) \mod 5) + 1 $.
Formally, for $q = 1, 2, \dots, 5$ , define:
\[
A_{k,1}^q = \bigcup_{\substack{i = q + 5j \\ 0 \leq j < k}} I_{i}, \quad \text{where } i = q, q+5, q+10, \dots, q+5(k-1).
\]
Each  $A_{k,1}^q $ is a union of $k$  non-overlapping subintervals, each of length  $\frac{1}{5k}$ .

3.	**Verify coverage:**
Observe that every interval  $I_{i}$  belongs to exactly one  $A_{k,1}^q$ , and thus:

$$\bigcup_{q=1}^5 A_{k,1}^q = \bigcup_{i=1}^{5k} I_{i} = [0, 1]$$.

---

**My Analysis**
Asking ChatGPT to take something written in descriptive english and translate it into mathematical notation in some sense tests whether the model has a deep understanding of the structure of what is being described, and in this case the model has failed. I omitted the rest of ChatGPT's response, which was it trying to incorrectly justify it's idea. At first glance the notational choices the model makes look very reasonable, and in fact I quite like the idea of splitting up the unit interval into 5k sub intervals to then distribute between the classes of $q$-values. This method could be easily modified to work, but the model has unfortunately constructed the intervals in such a way that any point will fall in exactly 1 covering set $q$, and this is far from the goal of the lemma which is to construct a classes of covering sets such that any point is in at least 4. In some sense this is exactly what one might expect an LLM to do in this context, pick nice notation, understand what it should try to say, but fail to actually demonstrate understanding of the underlying geometry at play. Next, I want to test the model in the opposite direction, by asking it to take very analytical math language and translate it back into something more intuitive. 


---

**User:**
I would now like help understanding the construction of the inner functions $\phi$. I understand how we construct the first $\phi_1$ in the sequence, and then we carefully pick values $\epsilon_1$ and $\delta_1$. I will ask a series of questions about these two choices of values, but first, to make sure we are on the same page, just respond by stating what these values are. Keep your response short and just give me the definition of $\epsilon_1$ and $\delta_1$ as given in the paper. 

**ChatGPT**
In the paper:
	•	$\epsilon_1$: This is chosen as  $\epsilon_1 = \frac{1}{4} \min \big| \psi_1(S_{1,1i,2j}^q) - \psi_1(S_{1,1m,2n}^q) \big|$ , where $(i, j) \neq (m, n)$.
	•	$\delta_1$: This is the infimum of the lengths of intersections  $L \cap U_1$ , where  $L$  is a horizontal line intersecting the $\epsilon_1$-neighborhood  $U_1$  of the graph of  $\phi_1$ .


**User:**
Now that I know we are on the same page, can you tell me why we have chosen $\epsilon_1$ as such? Specifically, we have chosen it so that when we construct the next function $\phi_2$ in our sequence, it satisfies condition 1 of the lemma for $r=1$ and $r=2$. Why does this choice of epsilon help guarantee that?

**ChatGPT**
...*Some response omitted*...
3.	Gap Preservation with  $\epsilon_1$ :
By making  $\epsilon_1$  proportional to the smallest gap between mapped intervals of  $\psi_1(S_{1,1i,2j}^q)$, the construction guarantees that even after adjustments to  $\phi_2$ , the mapped intervals  $\psi_2(S_{2,1i,2j}^q)$  remain non-overlapping. This preservation occurs because the perturbation introduced in constructing  $\phi_2$  (to maintain continuity and refinement) is controlled to stay within the  $\epsilon_1$ -neighborhood.

**User**
Now I would like to investigate the definition of $\delta_1$. Can you try to explain intuitively why it was chosen in such a way. Specifically can you discuss what this choice means when constructing the next function $\phi_2$. Why does this choice also help guarantee that we satisfy condition 1 for $r=1$ and $r=2$?

**ChatGPT**
...*Some response omitted*...
Why $\delta_1$ Helps Guarantee Condition 1:

1.	Control Over Perturbations:
•	The size of  $A_{2,1}^q$  and  $A_{2,2}^q$  determines how much  $\phi_2$  can “wiggle” when mapped onto  $S_{2,1i,2j}^q$.
•	Ensuring that  $A_{2,1}^q$  and  $A_{2,2}^q$  have lengths smaller than  $\delta_1$ prevents perturbations from spanning multiple  $\epsilon_1$-neighborhoods of disjoint intervals in  $\psi_1(S_{1,1i,2j})^q$ . This ensures that the new mapped intervals  $\psi_2(S_{2,1i,2j}^q)$  remain non-overlapping.
2.	Maintaining Separation Across Iterations:
•	 $\phi_1(x_1)$  already separates the rectangles  $S_{1,1i,2j}^q$ into distinct intervals.  $\phi_2$  must refine this separation while respecting the constraints imposed by  $\epsilon_1$ . By using  $\delta_1$ , we ensure that  $\phi_2$  introduces finer intervals without disrupting the structure of the disjoint sets created by  $\phi_1$.
...*Some response omitted*...
---

**My Analysis**

I first ask the model to give me the definition of the two elements that I am interested in studying, which it unsurprisingly does a perfect job of. This helps ensure that if it makes mistakes later it is not because of a misinterpretation of what the elements at play are. I then ask the model to to explain the choice of $\epsilon_1$ made in the proof. What I wanted the model to understand that the range of values which a square in $r=1$ could be sent to is controlled within $\epsilon_1$ and thus still satisfied condition 1 for these squares. The model did a spot on job of saying this, and clearly understands why the value was chosen as such. I then wanted to probe it on what is arguably the harder value to understand $\delta_1$. In this case the model is also good at summarizing the choice of $\delta_1$. It states that the choice prevents intervals from spanning the gaps between tiles in $r=1$, but the model then says that this ensure new mapped intervals $\psi_2(S_{2,1i,2j}^q)$ remain non-overlapping. Instead, I believe it should have said $\psi_2(S_{1,1i,2j}^q)$ remain non-overlapping. This is a small detail, but it is not a mistake that someone who fundamentally understands why we have chosen the specific values would make. Overall, for this section I am impressed with the models ability to make the language of the paper more understandable. It might make more sense that LLM's would be good at taking mathematical language and making it natural and not good at doing the reverse. This is generally because intuitive explanations are more forgiving to small hallucinations and factual inaccuracies. For the final test of ChatGPT's reasoning capacity, I wanted to see how it would handle understanding a series of algebraic steps made in the final part of the proof. Specifically, the proof makes use of facts proven throughout the paper in a series of steps without justifying each step. I ask ChatGPT to restate this set of manipulations while carefully justifying each change using facts from the paper or from general real analysis. 


---
**User**
On the bottom of page 10 through page 11 the paper makes a series of algebraic manipulations to show that $||g_1|| = ||g_0-f_1||$ is bounded by $\frac{5}{6}M_0$. Can you re-write this exact set of steps but on each line adding a justification for the changes made. Make sure that the justification either references something proved above in the paper or a common fact from real analysis. 


**ChatGPT**
...*Some response omitted*...

Start with the definition of $||g_1||$ :

$$
||g_1|| = \sup_{(x_1, x_2) \in E^2} |g_1(x_1, x_2)| = \sup_{(x_1, x_2) \in E^2} |g_0(x_1, x_2) - f_1(x_1, x_2)|.
$$

Justification: This follows from the definition of the supremum norm of a continuous function $||g_1|| = \sup_{x \in \text{domain}} |g_1(x)|$, and $g_1 = g_0 - f_1$.

Substitute the definition of $f_1$ :

$$
||g_1|| = \sup_{(x_1, x_2) \in E^2} \left| g_0(x_1, x_2) - \sum_{q=1}^5 \chi_q^1(\psi_q(x_1, x_2)) \right|.
$$

Justification: Substitute $f_1(x_1, x_2) = \sum_{q=1}^5 \chi_q^1(\psi_q(x_1, x_2))$, as defined earlier in the paper.

Group the terms into two parts:

$$
||g_1|| \leq \sup_{(x_1, x_2) \in E^2} \left| g_0(x_1, x_2) - \sum_{q=1}^3 \chi_q^1(\psi_q(x_1, x_2)) \right| + \sup_{(x_1, x_2) \in E^2} \left| \sum_{q=4}^5 \chi_q^1(\psi_q(x_1, x_2)) \right|.
$$

Justification: Use the triangle inequality: $|a - (b + c)| \leq |a - b| + |c|$. Here, we split the summation into $q = 1, 2, 3$ and $q = 4, 5$.

For the first term, observe that $\chi_q^1(\psi_q(x_1, x_2))$ approximates $\frac{1}{3}g_0$ :

$$
\sup_{(x_1, x_2) \in E^2} \left| g_0(x_1, x_2) - \sum_{q=1}^3 \chi_q^1(\psi_q(x_1, x_2)) \right| \leq \sup_{(x_1, x_2) \in E^2} \left| g_0(x_1, x_2) - \frac{1}{3}g_0(x_1, x_2) \cdot 3 \right|.
$$

Justification: Recall that $\chi_q^1(\psi_q(x_1, x_2))$ was constructed as $\frac{1}{3}g_0(x_{c_q}^1, x_{c_q}^2)$, where $(x_{c_q}^1, x_{c_q}^2)$ are centers of rectangles. Since the rectangles approximate $g_0$ uniformly on $E^2$, we replace $\sum_{q=1}^3 \chi_q^1$ with $\frac{1}{3}g_0 \cdot 3$.

Simplify the first term:

$$
\sup_{(x_1, x_2) \in E^2} \left| g_0(x_1, x_2) - \frac{1}{3}g_0(x_1, x_2) \cdot 3 \right| = \sup_{(x_1, x_2) \in E^2} \left| g_0(x_1, x_2) - g_0(x_1, x_2) \right| = \frac{3}{18}M_0 = \frac{1}{6}M_0.
$$

Justification: Algebraically, $g_0 - g_0 = 0$, but the perturbations introduced by $\psi_q$ and $\chi_q^1$ limit the error to $\frac{1}{6}M_0$. This bound comes from the choice of $\epsilon_1$ and the uniform continuity of $g_0$.

For the second term, bound the remaining summation:

$$
\sup_{(x_1, x_2) \in E^2} \left| \sum_{q=4}^5 \chi_q^1(\psi_q(x_1, x_2)) \right| \leq \frac{2}{3}M_0.
$$

Justification: Since each $\chi_q^1$ contributes $\frac{1}{3}M_0$, summing over $q = 4, 5$ gives $\frac{1}{3}M_0 + \frac{1}{3}M_0 = \frac{2}{3}M_0$.

Combine the results:

$$
||g_1|| \leq \frac{1}{6}M_0 + \frac{2}{3}M_0 = \frac{5}{6}M_0.
$$

Justification: Add the bounds from the two terms. Both approximations and inequalities were shown to hold under the assumptions of the construction and the uniform continuity of $g_0$.
  
...*Some response omitted*...

---

**My Analysis**
This is the perfect problem to challenge ChatGPT because it is not a particularly hard series of steps to explain algebraically, but it requires a deep understanding of what each component in the paper is built to do. ChatGPT has unfortunately failed, but not catastrophically. First, ChatGPT does a good job with simple explanations of steps having to do with more general analysis tools. The model first explained why we could assume the norm $||g_1|| = ||g_0 - f_1||$, something I didn't even remember needed justifying as I sort of take it for granted. It then correctly spots the triangle inequality which is not surprising. In the next step it makes its first big mistake. It correctly explains how we defined $\chi$ but then it says that "Since the rectangles approximate $g_0$ uniformly on $E^2$", which would not be a very specific statement even if it was right, but also it is unfortunately incorrect. What it should have said here is that we can replace $\chi$ through direct equality by instead using $g_0$ evaluated at the center of the tile. This misunderstanding then has consequences on the next step when ChatGPT finds itself then taking $g_0(x_1,x_2)-g_0(x_1,x_2)$ which it correctly notices is algebraically 0. Had it understood the last step correctly, it would have gotten instead $g_0(x_1,x_2)-g_0(x_{c_q}^1, x_{c_q}^2)$, and it seems to realize that it was wrong, correcting for this by saying something about the perturbations introduced by $\psi_q$ limiting the error. This does allow it to work its way back to the correct answer, but in no way would help aid someone learning about this theorem in understanding it. After this it easily finishes the final substitutions and finishes the explanation. 

---

**Conclusions**

I'd like to conclude this first by writing about my opinion on ChatGPTs performance and whether it's advice would have been on balance beneficial to me learning this paper had I not understood it before, then I will ask ChatGPT itself to read this paper and tell me how it thought it did in terms of helping aid me. 

Math papers can often be some of the most verbose and dense academic literature to understand, and to often great ideas that are intuitive and not incredibly complicated are hidden behind notation that prioritizes concision and accuracy (which is not a bad thing). For this reason I would hope that ChatGPT could be a powerful tool in translating this into more intuitive language that focuses less on precision and more on intuition. In some respects ChatGPT has nailed it with it's responses, and had I understood nothing about the paper beforehand, using ChatGPT to understand it would have gained me a slight amount of intuition. That being said, it still would have required substantial mathematical effort for me to correct its errors, and understand certain steps which it failed to explain (and unfortunately the hardest steps for me to understand were often the ones where it failed).  I think there is still some ways to go before we can trust an LLM on everything it says about a paper, but for now they are certainly a slight benefit to the informed reader.



