ICSE 2026, Research TrackCycle-2-Rebuttal response deadline in 4 days·chunyoupeng@email.swu.edu.cn
#1864 From Generation to Reasoning: Chain-of-Thought Guided Merge Conflict Resolution
[Main] Main[Edit] Edit
Your submissions	
(All)
Search
Email notification
Select to receive email on updates to reviews and comments.
PC Conflicts
Jacques Klein
Other conflicts
All (Southwest University)
ICSE 2026, Research Track #1864
Review #1864A
Review #1864B
Review #1864C
Submitted

[PDF] Submission (726kB) Jul 18, 2025, 9:34:38 AM UTC ·  29cd9063

Abstract
Merge conflicts have become a critical bottleneck in version control systems that significantly affect development efficiency, typically relying on manual, time-consuming processing. In recent years, learning-based methods have transformed the solution of merge conflicts from a classification problem to a generative task, directly generating post-conflict code by sequentially generating code tokens. Although this approach overcomes certain limitations of classification methods (e.g., the inability to introduce new code tokens), we observe that relying solely on the conflicting code for direct generation makes it difficult to effectively handle complex conflict scenarios that require the integration of non-trivial semantics and distributed modifications. To address this, this paper redefines merge conflict resolution as a reasoning task and proposes MergeCoT, an automated resolution framework based on Chain-of-Thought (CoT) prompting with Large Language Models (LLMs). Specifically, we design a simple Domain-Specific Language (DSL), introducing an Edit Script (ES) to structurally represent conflict information and guide the reasoning process. We then automatically construct a training dataset with explicit reasoning traces through a two-stage data generation pipeline, leveraging both DSL and ES representations. Experimental results on this dataset show that MergeCoT significantly outperforms the current state-of-the-art (SOTA) techniques in terms of precision and accuracy. The accuracy on Java reached 72.3% (an absolute improvement of 4.6%). Furthermore, experiments on various programming languages demonstrate MergeCoT’s superior multilingual versatility and cross-language generalisation ability. Additional ablation studies validate the critical role of the ES and CoT mechanisms in enhancing performance.

Authors (anonymous)
C. Peng, Z. Zhang, S. Tyszberowicz, Z. Liu, B. Liu [details]
Topics and options
✓ Confirmation of Author List
Topics
AI for Software Engineering: AI-enabled recommender systems for automated SE (e.g., code generation, program repair, AIOps, software composition analysis, etc.)
AI for Software Engineering: Automating SE tasks with LLM and other foundation models (e.g., large vision model)
AI for Software Engineering: Prompt engineering for SE (e.g., novel prompt design)
Primary Area: AI for Software Engineering
Information about Artifact Availability
All related artifacts—including code, dataset, and trained checkpoints—are available at https://anonymous.4open.science/r/MergeCoT-AF6D/readme.md The repository includes a README with instructions for reproducing all experiments and results in the paper.

✓ Compliance with ACM and IEEE Policies
✓ Compliance with Double Anonymous, Formatting, and Other ICSE 2026 Specific Policies
ACM Open: The authors can afford to pay APC.
✓ Confirmation of Accuracy of Conflicts of Interest
✓ Confirmation of Other and Personal Conflicts of Interest
Is the Paper a Resubmission of an ICSE 2026 (Cycle 1) Rejected Paper?: No
OveMer	ArtAss
Review #1864A		2	
Review #1864B		2	3
Review #1864C		2	
You are an author of this submission.

[Edit] Edit submission[Add response] Add Cycle-2-Rebuttal response

[Text] Reviews in plain text

Review #1864A
Overall merit
2. 
Weak reject

Paper summary
This paper proposes a new approach based on chain of thought with LLMs to guide resolving merge conflicts, called MergeCoT.

It relies on two main steps. First, a simple DSL introducing an edit script between original and conflicting branches in the merge (in the form of add, replace, delete changes). Second, the authors construct a customized training dataset by generating reasoning traces using the edit scripts that contextualize more the merge conflicts.

MergeCoT is then evalaued on 10% of the test dataset. It shows that is outperformes other seletced baselines in case of java and other languages present in the training dataset. A further ablation study showed the benefit of the edit script in improvements brought by MergeCoT in resolving merge conflicts.

Strengths
Important topic on resolving merge conflicts
New approach based on reasoning and on structured description of the conflicts with edit scripts
Sound evaluation
Weaknesses
Lack of details about the traces of reasoning and it is unclear how the output CoT look like
The introduced DSL for the edit script seems limited, and it's unclear how moves are handled. It's also unclear why no SOTA edit script is used instead
Incomplete ablation study
Detailed comments for authors
The paper is well motivated, easy to read and follow, with a clear presentation. Resolving merge conflicts is a relevant topic and the paper proposes a new approach to tackle it. Overall, MergeCoT seems novel and shows improved results over several baselines. I have however, some comments and concerns, as follows.

The approach argues for the benefit of using an edit script. This is not novel per se, as it has been used in several other topics and even with LLMs as extra context. Maybe not in merge conflict resolution. Nevertheless, apart from using an edit script that results show benefits, I wonder why you have not used existing SOTA solutions for computing it, such as GumTree or others. Especially since it seems you handle basic edit scripts with only replacement, add, and delete changes without move changes. Is it feasible to change your edit script with the one of GumTree and observe the new results ?

The second concern I have is with the generation of the chain of thought and what you also refer to as the intermediate reasoning process (section 3.2). It is unclear what they look like. Do they have (or do you enforce) a specific structure in which they come from? This part is not detailed enough, and it would help to clarify it, even with an example if needed.

Also can you report on its results for each languages. You only mention it for Java that it gives 49.5% in stage 1 and then stage 2 increases it to 91.3%. What about other languages. Besides, I did not get how you ensure or check the correctness of stage 2. Can you elaborate on it further?

It surprised me a bit that the test set is only 10% of the dataset. Usually it is around 20% or more. Did you attempt a training only on 80% or less? Would it be feasaible to test on ratios of 70%/30% or 80%/20%?

RQ3 runs an ablation study for the edit script component. What about an ablation study for the reasoning and the generation of chain of thoughts? I would have also expected an ablation study for it. Can you run it or elaborate on why did not you perform it ? Also, in RQ3, you comment on "the significant contribution of ES to performance", while the improvement is only 1.7% in precision and 1.9% in accuracy. I would not say it is a significant improvement, but just a small yet clear improvement.

In RQ4, the discussion of the results seems to suggest that MergeCoT allows transferability or generalization to other languages with training on them. However, the original model used is already trained on those tested languages (JS and TS). Thus, one should be careful here when drawing a conclusion. Again, the improvements compared to direct generation from the original model are around 2%, which shows that the original model can already cope with those merge conflicts. It would help to have a more detailed and fair discussion of the results of RQ4.

Section 6.1 discusses the computational overhead introduced by the approach, which is non-negligible. It would be great if you can somehow quantify it or measure it.

Minor comments

Maybe you can add and discuss takeaways at the end of each RQ.
In tables 1,2,3,4, you could add the difference (x% -+ y) to MergeCoT compared with the other approaches.
Questions for authors’ response
Q1) Is it feasible to change your edit script with the one of GumTree and observe the new results ?

Q2) Can you detail the generation part of the chain of thought and how they look like ? Also, how do you check their correctness in the stage 2 of the generation ?

Q3) Why did not you run an ablation study for the second component of generation of the chain of thought ?

Q4) Would it be feasaible to test on a ratio of 70%/30% or 80%/20% for training/test sets ?

Q5) Can you quantify the computational overhead ?

Review #1864B
Overall merit
2. 
Weak reject

Paper summary
This work presents MergeCoT, an approach that combines edit scripts and Chain of Thought prompting to resolve merge conflicts. Given a merge conflict, an edit script is computed, and then given to an LLM to generate the conflict resolution as well as a reasoning trace. The authors construct a training dataset using a teacher model to generate a large number of reasoning/resolution pairs which they then use to fine-tune a smaller LLM (mergeCoT) for the task. They evaluate MergeCoT across four languages, showing strong language generalization and performance improvement over SoTA approaches.

Strengths
Well written, easy to follow
Clear and well defined research questions
Approach demonstrates substantial performance gains
Weaknesses
One of the core motivations of the work, the novel framing of the problem as a reasoning task as opposed to simple classification/generation, should be evaluated in more depth.

Overall weak technical contributions of the work. Both edit scripts and CoT for merge conflict resolution have been explored in prior work, though not combined.

The problem framing and technical contributions of the work are further weakened by the emergence of reasoning models, with implicit CoT traces that do not need to be explicitly prompted for, the work should compare to these models.

Shallow analysis of failure cases

Detailed comments for authors
One of the primary contributions of the work is the prompting approach, using edit scripts and chain of thought reasoning traces to fine-tune an LLM. However, with the emergence of reasoning models, it's unclear why the authors choose to explicitly prompt for CoT traces and not use an off the shelf reasoning model to extract traces that way.

Overall the contributions of the work are weak. The authors call out the edit script, prompting approach, and dataset construction method as some of the contributions. However all three of these have been explored in prior work: ES in MergeBert and ChatMerge, chain of thought prompting in ConGra [1], and the STaR work for the dataset construction approach. Though combining all three methods together is certainly a novel contribution, it's worth noting.

[1] Zhang, Qingyu, et al. "CONGRA: Benchmarking Automatic Conflict Resolution." arXiv preprint arXiv:2409.14121 (2024).

One of the core hypotheses of this work is that the reasoning traces extract via CoT should improve merge outcomes. However, there is no analysis on the validity of these extracted traces. Similar to RQ3, the paper should include an ablation on the effectiveness of the CoT approach. And with the emergence of reasoning models, this should be compared to the native reasoning traces. The takeaways to practitioners are not clear: should tool creators explicitly prompt for CoT reasoning? How much does it contribute to the performance? And would a reasoning model demonstrate the same performance?

( Section 5.1 ) One of the main arguments in the paper is that the framing of merge conflict resolution as a classification or simple generative problem is not sufficient. This hypothesis should be validated in RQ1. The authors are missing a clear opportunity to analyze examples where MergeCoT outperforms classification baselines (MergeBert) and show empirical evidence that the failure of the baseline is related to the framing of the problem. For example, what percentage of these cases have to do with missing context that a classification model is critically missing?

I appreciate the section on failure cases however it is quite shallow. The section should be updated with concrete numbers, for example, the actual distribution of the kinds of failures identified.

Minor Comments:

Consider renaming K in section 3.2 …. 2K (l607) calls means something else at first glance.
Questions for authors’ response
Why use explicit CoT prompting instead of reasoning models?
How do CoT reasoning traces contribute to the performance of MergeCoT?
Artifact assessment
3. 
Satisfactory, i.e., the artifacts are in line with what is declared in the submission form or the paper [OR] the authors explained why the artifacts are not provided and I find the explanation to be reasonable.

Review #1864C
Overall merit
2. 
Weak reject

Paper summary
The proposed approach, called MergeCoT, follows a line of research on utilizing deep learning for merge conflict resolution. More precisely, it follows an LLM-based generative approach, but differs from previous work in two aspects:

Instead of using conflicting chunks of text as input, MergeCoT describes the differences in conflicting branches wrt. to the common base version in terms of token-level edit scripts (i.e., inserted, deleted and replaced tokens).
Instead of working on pairs of conflicts and their historical resolution, MergeCoT utilizes a so-called teacher model that generates a chain of thoughts supposed to explain the rationale behind the generated conflict resolution. Therefore, it uses an adaptation of the STaR (Self Taught Reasoner) method proposed by Zelikman et al. [31].
Experiments have been conducted on a dataset originally constructed for training and evaluation of MergeBERT [25], evaluating (i) MergeCoT's overall performance on Java conflicts compared to selected baseline approaches, and (ii) its multilingual generality compared to the most closest competitors. Moreover, an ablation study has been conducted evaluating (iii) the effectiveness of the edit script representation in a mono-lingual setting, and (iv) the edit script (ES) and chain of thoughts (CoT) effectiveness in a cross-language setting. The results show that MergeCoT outperforms competitors wrt. (i) and (ii), and the effectiveness of the ES and CoT components have been confirmed in (iii) and (iv).

Strengths
The two-stage learning via the teacher model is a great idea to construct a mostly trustworthy corpus of merge cases with explanations.
Overall well written, and easy to follow paper.
If the numbers could be trusted, the authors present a major improvement over the status quo on the important task of merge conflict resolutions.
Weaknesses
Too many significant details are not explained, or unsound in the current paper version.
For a fair comparison with the competitors (folds, choice of competition), the authors have to adapt their experiment setup.
The authors' explanation of their edit script could have been cut down to half a line, instead of wasting a complete page.
Detailed comments for authors
Novelty
Technical novelty lies in the components 1. and 2. Though neither edit script generation nor the STaR method are new by themselves, integrating them in a deep-learning based merge conflict resolution is indeed the first attempt of its kind.

As for the edit script, I was actually wondering why the paper makes a big deal out its generation, framing the representation even as a novel DSL. There are dozens of different approaches for calculating and representing edit scripts proposed in the literature. I understand that they often work on a line-level, but could be easily adapted to token level, as this is rather a tooling question, isn't it? One whole page of the manuscript could have been saved to clarify other parts. Furthermore, in your edit scripts, if a token X is part of the conflict more than once, how can the model differentiate between the instances of X?

Significance
MergeCoT outperforms its strongest competitor in terms of accuracy by 4.6 percent in the conducted Java experiments, which decreases down to 1,5 percent for JavaScript for the generalization study.

If I understand correctly, the experiments have not been repeated for competitors such as MergeGen, but the paper simply reports their results, which may have been achieved on different train/validation/test splits. According to our experience in similar experiments, the train/validation/test split may have a significant impact on the overall performance. Thus, before being able to judge about the significance of the results, I would like to know whether train/validation/test have been chosen identical or different from the competitor experiments. In the latter case, the performance boost is quite limited and might be caused by more fortunate splits. Even if ablation shows the effectiveness of the novel components to some extent, it does not yet convince me about the stability of the effectiveness. In the former case, I'd be more relaxed, but I would still like to see the results for different splits to be fully convinced by the approach.

I was not sure if the CoT is supposed to be shown to developers as additional explanation for the generated merge conflict resolution. This would clearly add another dimension of contribution to the paper, but I do not see anything in this direction. Neither qualitative examples how this would look like, nor is there an evaluation attempt going into that direction.

Rigor / soundness
While accuracy is clear in terms of exact match with ground truth, I wonder about the definition of precision, that is defined as the portion of "syntactically valid resolutions that correctly resolve the conflict". However, this definition seems to be adopted from previous works, so I think it's fine.

Baseline selection is fine wrt. the competitors in ML-based merge conflict resolution. However, I was struggling with the selection of diff3 and JDIME, both of which are different methods for conflict detection but none of them performs conflict resolution in the first place. Given the latter, I was wondering how the evaluation determined accuracy and precision of conflict resolution for diff3 and JDIME. I mean, Git diff3 does some silent auto-merges of non-conflicting parts, but I can hardly assume that these are even considered in the evaluation, are they? If so, I am even more confused, as this raises the fundamental question of what a conflict actually is (a structured merge tool typically reports conflicts different from those reported by a textual merge tool). Following my intuition, diff3 can only ever have a precision of 0% (conflict markers are always part of diff3 output and thus never syntactically correct), while its accuracy might be a bit higher (if a ground truth merge contains these conflict markers). Please explain.

How can MergeBERT and ChatMerge have a higher accuracy than precision? This also only makes sense, if there are many syntactically incorrect results in the dataset. It seems you took these numbers uncritically from the original paper. If you used a subset (see question below) of their dataset (not their whole set), you have to repeat their experiments.

Looking at the experiments conducted for RQ3 and RQ4, I was wondering why RQ3 leaves out only ES, whereas the direct generation approach in RQ4 leaves out ES and CoT. Wouldn't it be interesting to do comparable ablations here to see the effect of ES and CoT in both the single-language and cross-language setting? Even more important, wouldn't it be straightforward to assess the effect of both components individually in both settings? I only see limited value in the current setup and results.

What does your 'dataset is based on on MergeBERT's' mean? Did you take a subset? Please give a table/summary of your/their dataset: how many conflicts did you train on? How many per language?

Your argumentation in lines 951-954 (i.e. GPT-4 does not produce explanations unless explicitly prompted) is too simplistic. Just adding a "explain yourself step by step" or activate CoT modes is easier (and possibly cheaper) than your approach. I feel, a better argument is needed to waive the comparison.

Presentation
Besides my questions that demand clarification, see rigor and significance, I found the paper generally well written and easy to follow. I particularly like the motivation of the approach and its positioning within the related work of ML-based merge conflict resolution, though I am not (yet) convinced by the results.

Is RQ2 really needed, given RQ1? I'd unite them.

Minor presentation issues:

l. 204-205, 248: cite your claims
l. 212: "tentative merge result"
l. 213: "||||||||" at end of line
l. 302: what is "highly generalised"?
l. 315-316: A->1, B->2?
l. 351: Conflict
l. 353, 358: leave out, first line of your example has no conflict!
l. 505: is this "X" defined?
l. 567: is this r_i defined? -- in 576?
l. 621: -"about", what about the other CoTs for the other languages?
l. 660: not necessesarily "human"-written, could be a tool that chose "OURS" for all conflicting chunks
l. 944: -"large"
Questions for authors’ response
Q1: Did you conduct your experiments on the exact same dataset and folds as MergeBERT and ChatMerge?

Q2: Why did you choose diff3 and JDIME as competitors; how do they resolve conflicts? How should one interpret accuracy and precision >0% for these tools?

Q3: It seems to be the case you give your model the input as shown in Figure 1, i.e., a conflict without wider context of its surrounding lines from its file or even the whole project, or other conflicts. Can you clarify this please?

Q4: In your edit script: if a token X is part of the conflict more than once, how can the model differentiate between the instances of X?

Add Cycle-2-Rebuttal response
HotCRP
