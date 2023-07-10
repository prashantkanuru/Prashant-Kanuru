# Self-Instruct : Aligining Language Models with Self-Generated Instructions

![image](https://github.com/prashantkanuru/Prashant-Kanuru/assets/79887087/f5aa3fa5-de9e-4a67-b89e-399818e5f6b1)
<br>
Large "instruction tuned" langauge models (i.e., finetuned to respond to instructions) have demonstrated a remarkable ability to generate zero-shot to new tasks. Nevertheless, they depend heavily on human-written instruction data that is often limited in quantity, diversity and creativity, therefore hindering the generality of the tuned model. We introduce **SELF-INSTRUCT** , a framework for improving the instruction-following capabilities of pre-trained language models by boot-strapping off their own generation.
<br>
<br>
Our pipeline generates instructions, input and output samples from a language model, then filters invalid or similar ones before using them to fine-tune the original model.
Applying our method to the vanilla GPT3, we demonstrate a 33% absolute improvement over the original model on SUPER-NATURALINSTRUCTIONS, on par with the performance of InstructGPT001, (unless otherwise specified, our comparisons are with the text-davinci-001 engine. We focus on this engine since it is the closest to our experimental setup: supervised finetuning with human demonstrations. The newer engines are more powerful, though they use more data (e.g., code completion or latest user queries) or algorithms (e.g. PPO) that are difficult to compare with.
## How self-instruct works:
1. The self-instruct method is an iterative bootstrapping algorithm that starts with a
- seed set of manually-written instructions and uses them to prompt the language model to generate new instructions and corresponding input-ouput instances.
  -  So prompt the language model to generate new instructions based on seed set of manually written instructions and
  -  also in the prompt intsruct to generate corresponding input-output instances.
2. These generations are then filtered to remove low-quality or similar ones, and the resulting data is added back to the task pool. THis process can be repeated multiple times, resulting in a large collection of instructional data that can be used to fine-tune the language model to follow instructions more effectively.

### Examples:
<br>
Instruction: Given an address and city, come up with the zip code.
<br>
Input:
<br>
Address: 123 Main Street, City: San Francisco
<br>
Output: 94105
<br>
Instruction: I am looking for a job and I need to fill out an application form. Can you please help me complete it?
<br>
Input:
<br>
Application Form:
<br>
Name:_____________ Age: ____________ Sex:____________
<br>
Phone Number:_____________ Email Address:_____________
<br>
Education:__________
<br>
Output:
<br>
Name: John Doe Age: 25 Sex: Male
<br>
Phone Number .....
<br>
Instruction: How to write a code for converting degree fahrenheit to celcisus.
<br>
Input: NULL
<br>
Output: 
<br>
<br>
def convert_fahrenheit_to_celsius(fahr):
  <br>
&nbsp;&nbsp;&nbsp;&nbsp;celsius=(fahr-32)*5/9
  <br>
&nbsp;&nbsp;&nbsp;&nbsp;return celsius
  <br>
 <br>
 Instruction: Write a letter from the perspective of a cat.
 <br>
 Input: Null
 <br>
 Output: 
 <br>
 Dear [Owner], I am writing to you today because I have a problem. You see, I have been living with you for the past [Number of Years] and I love 
- The above examples are selected tasks from the generated instruction using vanilla GPT3. Some texts are reformatted for presentation
(nbsp for 1 space, ensp for 2 spaces, emsp for 4 spaces)

### Self-Instructed Models:
- SELF-INSTRUCT is a semi-automated process for instruction-tuning a pretrained LM using instruction signals from the model itself. THe overall process is an iterative bootstrapping algorithm. 
  - It starts off with a limited (e.g. 175 in our study) seed set of manually written tasks that are used to guide the overall generation.
- In the first phase, the model is prompted to generate instructions for new tasks. This step leverages the existing collection of instructions to create more broad-coverage instructions that define (often new) tasks.
- Given the new newly-generated set of instructions, the framework also creates input-output instances for them, which can be later used for supervising the instruction tuning.
- FInally, various heuristics are used to automatically filter low-qualiyty or repeated instructions, before adding the remaining valid tasks to the task pool. This process can be repeated for many iterations until reaching a large number of tasks.
- To evaluate SELF-INSTRUCT empirically, we run this framework on GPT3 which is a vanilla LM. **The iterative SELF INSTRUCT process on this model leads to about 52k instructions, paired with about 82k instance inputs and target outputs**

## A.4 Prompting Templates for Data Generation:
- SLEF-INSTRUCT relies on a number of prompting templates in order to elicit the generation from language models. Here we provide our four templates:
  -  for generating the instruction (Table 5)
     - Prompt used for generating new instructions: 
  -  classifying whether an instruction represents a classification task or not (Table 6)
  -  generating non-classification instances with the input-first approach (Table 7)
  -  generating classification instances with the output first approach. (Table 8)
 

 
