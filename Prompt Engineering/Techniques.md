---
banner: https://statics-cls.vcdn.com.vn/vng_cloud_blog_what_are_large_language_models_cover_en_0ce8e6c899.png
---
# Prompting technique
## Zero-shot Prompting
- Các model hiện đại có thể thực hiện việc zero-shot 
- VD:
```python 
Classify the text into neutral, negative or positive. 

Text: I think the vacation is okay.
Sentiment:
```
## Few-shot prompting 
- Thêm ví dụ => in-context learning 
###### Limitation
- Trong các task về reasoning few-shot learning tỏ ra không hiệu quả 

## Chain-of-Though(CoT) Prompting
- Phương pháp này giúp LLM có khả năng reasoning bằng việc thông qua bước trung gian 
 ![[Pasted image 20240326041219.png]]
###### Zero-shot COT Prompting 
![[Pasted image 20240326041404.png]]
- Đơn giản là thêm "Let's think step by step" ở cuối 
###### Automatic Chain-of-Thought (Auto-CoT)
![[Pasted image 20240326041731.png|825]]
- Nói chung là dùng zero-shot để generate reasoning chain 
- Gồm 2 bước:
	- Question clustering: Từ dataset tạo một vài cluster để feed vào LLM 
	- Demonstration sampling: Sử dụng "Let's think step by step" cho các câu hỏi được sampling để generate ra reasoning chain

## Self-Consistency
- Sample những phần reasoning khác nhau từ few-shot CoT sau đó use generations để chọn ra answer consistent nhất 


## Generate Knowledge Prompting
![[Pasted image 20240326044251.png]]
- Tóm lại là cách thêm tri thức về thế giới trước khi generate ra câu hỏi 
- Paper: [2110.08387.pdf (arxiv.org)](https://arxiv.org/pdf/2110.08387.pdf)

## Prompt Chaining 
- Break task thành các subtasks (Chia nhỏ các prompt, transform thông tin từ prompt này để nhận output và feed vào prompt tiếp theo)
- Prompt 1:
```
You are a helpful assistant. Your task is to help answer a question given in a document. The first step is to extract quotes relevant to the question from the document, delimited by ####. Please output the list of quotes using <quotes></quotes>. Respond with "No relevant quotes found!" if no relevant quotes were found.


####
{{document}}
####
```
- Output 1:
```
<quotes>
- Chain-of-thought (CoT) prompting[27]
- Generated knowledge prompting[37]
- Least-to-most prompting[38]
- Self-consistency decoding[39]
- Complexity-based prompting[41]
- Self-refine[42]
- Tree-of-thought prompting[43]
- Maieutic prompting[45]
- Directional-stimulus prompting[46]
- Textual inversion and embeddings[59]
- Using gradient descent to search for prompts[61][62][63][64]
- Prompt injection[65][66][67]
</quotes>
```
- Prompt 2:
```
Given a set of relevant quotes (delimited by <quotes></quotes>) extracted from a document and the original document (delimited by ####), please compose an answer to the question. Ensure that the answer is accurate, has a friendly tone, and sounds helpful.

####
{{document}}
####

<quotes>
- Chain-of-thought (CoT) prompting[27]
- Generated knowledge prompting[37]
- Least-to-most prompting[38]
- Self-consistency decoding[39]
- Complexity-based prompting[41]
- Self-refine[42]
- Tree-of-thought prompting[43]
- Maieutic prompting[45]
- Directional-stimulus prompting[46]
- Textual inversion and embeddings[59]
- Using gradient descent to search for prompts[61][62][63][64]
- Prompt injection[65][66][67]
</quotes>
```
- Output 2:
```
The prompting techniques mentioned in the document include:

1. Chain-of-thought (CoT) prompting[27]
2. Generated knowledge prompting[37]
3. Least-to-most prompting[38]
4. Self-consistency decoding[39]
5. Complexity-based prompting[41]
6. Self-refine[42]
7. Tree-of-thought prompting[43]
8. Maieutic prompting[45]
9. Directional-stimulus prompting[46]
10. Textual inversion and embeddings[59]
11. Using gradient descent to search for prompts[61][62][63][64]
12. Prompt injection[65][66][67]

Each of these techniques employs unique strategies to enhance or specify the interactions with large language models to produce the desired outcomes.
```
## Tree of Thoughts (ToT)
![[Pasted image 20240326045903.png|800]]
- Giúp explore nhiều thoughts khác nhau
- Paper: [2305.10601.pdf (arxiv.org)](https://arxiv.org/pdf/2305.10601.pdf)
![[Pasted image 20240326051445.png]]
- To perform BFS on ToT: evaluate each thought candidate as "sure/maybe/impossible" with regard to reaching 24

## Retrieval Augmented Generation (RAG)
![[Pasted image 20240326051736.png]]
- Goals:
	- Complex and knowledge-intensive tasks, it's possible to build a language model-based system that accesses external knowledge sources to complete tasks
	- Giảm tình trạng "hallucination"
	- Adaptive for situations where facts could evolve over time

## Automatic Reasoning and Tool-use (ART)
- Flow of work:
	- Given task => select demonstrations of multi-step reasoning and tool use from a task library
	- At test time => pauses generation whenever external tools are called, and integrate their output before resuming generation
![[Pasted image 20240326052742.png]]

## Automatic Prompt Engineer (APE)
- APE discovers a better zero-shot CoT prompt than the human engineered "Let's think step by step" prompt
![[Pasted image 20240326053114.png]]
- Use as a black-box optimization problem using LLMs to generate and search over candidate solution 

## Active Prompt 
- Problems: Chain-of-thought (CoT) methods rely on a fixed set of human-annotated exemplars. The problem with this is that the exemplars might not be the most effective examples for the different tasks.
- Active Prompt is used to adapt LLMs to different task-specific
 ![[Pasted image 20240326053745.png]]


## Directional Stimulus Prompting 
- Goals: Guide LLM in generating a desired summary 
- ![[Pasted image 20240326054034.png]]
- Using stimulus/hint
## PAL(Program-Aided Language Models)
- Leveraging programmatic runtime such as a Python interpreter
![[Pasted image 20240326054321.png]]
## ReAct Prompting 
- ReAct = Reason + Action 
- 



## Reflexion 
![[Pasted image 20240326054717.png]]\
- Key steps in Reflexion:
	- define a task
	- generate a trajectory
	- evaluate
	- perform reflection
	- generate the next trajectory
-  Reflexion consists of three distinct models:
	- **An Actor**: Generates text and actions based on the state observations. The Actor takes an action in an environment and receives an observation which results in a trajectory. [Chain-of-Thought (CoT)(opens in a new tab)](https://www.promptingguide.ai/techniques/cot) and [ReAct(opens in a new tab)](https://www.promptingguide.ai/techniques/react) are used as Actor models. A memory component is also added to provide additional context to the agent.
	- **An Evaluator**: Scores outputs produced by the Actor. Concretely, it takes as input a generated trajectory (also denoted as short-term memory) and outputs a reward score. Different reward functions are used depending on the task (LLMs and rule-based heuristics are used for decision-making tasks).
	- **Self-Reflection**: Generates verbal reinforcement cues to assist the Actor in self-improvement. This role is achieved by an LLM and provides valuable feedback for future trials. To generate specific and relevant feedback, which is also stored in memory, the self-reflection model makes use of the reward signal, the current trajectory, and its persistent memory. These experiences (stored in long-term memory) are leveraged by the agent to rapidly improve decision-making.

## Multimodel CoT
![[Pasted image 20240326054104.png]]