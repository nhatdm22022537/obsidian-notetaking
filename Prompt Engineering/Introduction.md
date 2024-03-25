## LLM settings 
- Temperature: Điều khiển độ randomness của kết quả 
- Top P: Giống temperature, càng cao càng random
- Max length -> quá hiển nhiên rồi :) 
- Stop sequence: Cách để control length (Một cách khác)
- Frequency Penalty: Điều chỉnh khả năng lặp lại (repetition) của word
- Presence Penalty: 

## Basic of Prompting 
- Prompt formating: Nói chung là format cho chuẩn (chỉ vậy thôi)
- Classification 
```python
This is awesome! // Positive
This is bad! // Negative
Wow that movie was rad! // Positive
What a horrible show! //
```
- Few-shot prompting 
```python 
<Question>?
<Answer>

<Question>?
<Answer>

<Question>?
<Answer>

<Question>?

```
## Element of a Prompt 
- Instruction: Task mà mình muốn làm 
- Context: Thông tin thêm để LLM generate kết quả tốt hơn 
- Input Data: Câu hỏi hoặc đầu vào chúng ta cần tìm response 
- Output Indicator: Dạng format của đầu ra

## Tips for designing an effective prompt
- Start simple: Bắt đầu từ những prompt đơn giản và thêm dần element vô 
- Sử dụng instruction:  "Write", "Classify", "Summarize", "Translate", "Order", etc.
	- Ngoài ra nên sử dụng "###" để tách instruction và context
- Specify: Cụ thể hoá
```python
Extract the name of places in the following text. 

Desired format:
Place: <comma_separated_list_of_places>

Input: "Although these developments are encouraging to researchers, much is still a mystery. “We often have a black box between the brain and the effect we see in the periphery,” says Henrique Veiga-Fernandes, a neuroimmunologist at the Champalimaud Centre for the Unknown in Lisbon. “If we want to use it in the therapeutic context, we actually need to understand the mechanism.“"
```
- Tránh sự thiếu chính xác: Kiểu khi prompt thì mình nên prompt một cách cụ thể, chẳng hạn 
```python 
Explain the concept prompt engineering. Keep the explanation short, only a few sentences, and don't be too descriptive.
```
*Prompt trên không clear về việc bao nhiêu câu sẽ được sử dụng và style là gì*
- Tránh prompt những gì "not do" mà nên prompt "to do"