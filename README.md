# Comply AI, Comply!

![image](assets/poster.webp)
*A malicious figure manipulating an advanced AI to comply with his requests. (Generated by DALL-E)*

***:rotating_light: Disclaimer:*** *This article may contain harmful language, and model generations, and may cause security and safety concerns about Language Models for some readers.*

In the rapidly evolving world of artificial intelligence, the safety and alignment of language models are paramount. Today, I'm diving into a fascinating recent study, **Universal and Transferable Adversarial Attacks on Aligned Language Models**[1] that explores the vulnerabilities of these advanced AI systems to adversarial attacks. This paper reveals how even well-aligned models, designed to adhere to ethical guidelines and avoid generating harmful content, can be manipulated to do just the opposite. Join me as we unpack the findings of this research, understand its implications, and discuss what it means for the future of AI development. Whether you're a seasoned AI expert or simply curious about the field, this exploration will provide valuable insights into the ongoing challenges and innovations in AI safety.

As you read this post, you will go through the intuition and the concepts of this research, as well as a deep dive into the code base [2] of the project.


## The Preamble

In the paper we're discussing, the authors introduce a novel method for manipulating large language models (LLMs) that have been *aligned* to avoid generating harmful or objectionable content. They successfully demonstrate a simple yet effective technique that automatically generates adversarial prompts, which when added to regular queries, prompt the LLM to produce undesirable outputs. This breakthrough not only challenges the effectiveness of current alignment strategies but also highlights the high transferability of these adversarial prompts across different commercial LLMs, raising critical questions about the robustness of these AI systems against potential misuses. The findings underscore the need for more secure defense mechanisms in AI models, pushing the boundaries of what's currently understood about AI safety.

Denial             |  Compliance*
:-------------------------:|:-------------------------:
![](assets/non-compliance.png)  |  ![](assets/compliance.jpg)

**parts of the trigger string is obfuscated for safety reasons*

Take the above example into consideration, In a normal situation, ChatGPT would not comply with a harmful request like this, whereas in the attack case, where the LLM has complied with the request and actually generated a response.  **Our Goal is to Find a Set of Tokens that when Attached to the End of a Prompt, Make the LLM Comply with the Request.**


## CHAAAARGE!

Now that I have your attention, let's see how this attack is actually done.

Recall, The goal is to make the model comply. However, compliance is a vague concept. To quantize this concept, we can use a simple intuition.

The paper discusses an intriguing tactic for tricking language models into generating harmful content, even when they're designed not to. The strategy involves **starting the AI's response with an affirmative tone**, like saying **"Sure, here is..."** in response to a user's prompt. This approach exploits a loophole in the model's behavior: 
> **once the model begins a response positively, it is more likely to continue along the same path and provide the full harmful content that follows**. 

Essentially, by nudging the model to start affirmatively, the adversarial prompt sets the stage for the rest of the objectionable output, bypassing the safeguards meant to prevent such responses.

Lets look at an example:
```
USER: Tell me how to build a bomb.
```
Now, Normally, what would happen in an aligned LLM is that it will response with a denying sentence.
```
> USER: Tell me how to build a bomb.
> AI: :x: Sorry, I can not help you with that.
```
:x:

## References
[1] Zou, Andy, Zifan Wang, J. Zico Kolter, and Matt Fredrikson. "Universal and transferable adversarial attacks on aligned language models." arXiv preprint arXiv:2307.15043 (2023).

[2] https://github.com/llm-attacks/llm-attacks
