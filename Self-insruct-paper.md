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

