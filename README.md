# Beating ChatGPT o1, 4o and DeepSeek R1 with smaller LLMs & GraphRAG
This project briefly showcases how smaller LLMs combined with knowledge graphs can outperform much larger and more capable LLMs in complex multi-hop question answering of Wikipedia data. 
## Comparison
Complex multi-hop questions are presented to ChatGPT o1, 4o and DeepSeek R1 against Mistral Large querying a public Knowledge Graph sourced from Wikipedia (DBpedia)
## KG of Nelson Mandela (Simplified)
![Nelson Mandela Knowledge Graph](https://github.com/Champagne-paki/GraphRAG-Comparison/blob/main/Nelson%20Mandela%20Knowledge%20Graph.png)
## 4-hop Question 
Q: Who are the spouses of the current chancellors from where Nelson Mandela got his alma mater from and when were they born?

A: The spouse is Zanele Dlamini Mbeki and her birthdate is 1938-11-18

As we can see below, both ChatGPT models failed to answer this question with DeepSeek R1 only reaching up to the chancellor's name. However, my architecture provided the necessary context for the LLM to guide its answer to this complex question.

```Text
// SYSTEM: You are a helpful assistant

USER: Who are the spouses of the current chancellors from where Nelson Mandela got his alma mater and when were they born.

ASSISTANT: I’m not aware of any publicly available, authoritative source that lists the spouses of all chancellors of each institution Mandela attended—let alone their birth dates. Nelson Mandela studied at several universities (Fort Hare, the University of the Witwatersrand, and later the University of South Africa), and the offices of chancellor at these institutions have often been largely ceremonial. Details about chancellors’ private lives—especially spouses’ names and birth dates—are not comprehensively documented in standard historical or university archives available to the public.

If you need this information for a historical or scholarly project, you might consider:

• Checking each university’s official archival collections or contacting their administrative or alumni offices to see if they catalog such personal details (though many do not, as it is private information).  
• Consulting credible biographical dictionaries, local historical societies, or specialized academic works that might discuss key figures in the universities’ histories.  

However, this level of personal data (particularly birth dates of spouses) is often either altogether unrecorded publicly or is protected to respect individual privacy. If a specific chancellor or spouse was a prominent public figure in their own right (for example, well-known politicians or activists), you may find biographical details in reliable news archives or official government or NGO websites. Otherwise, it may simply not be a matter of public record.

Settings used
model-name: OpenAI o1 (External)
model: openai-o1
temperature: 0.5
top_p: 0.5
```

```Text
// SYSTEM: Answer in one line

USER: Who are the spouses of the current chancellors from where Nelson Mandela got his alma mater and when were they born

ASSISTANT: <think>
Okay, let's try to figure out this question. The user is asking about the spouses of the current chancellors from the university where Nelson Mandela got his alma mater, and their birth dates.

First, I need to determine where Nelson Mandela studied. I recall that Mandela attended the University of Fort Hare in South Africa. So his alma mater is the University of Fort Hare. Now, the question is about the current chancellors of that university. Wait, but universities usually have one chancellor, not multiple. Maybe the user is confused or there's a misunderstanding here. Let me confirm: the University of Fort Hare's current chancellor. Let me check that. 

Looking it up, the current chancellor of the University of Fort Hare as of recent information is Dr. Vuyo Mahlati. She was appointed in 2021. However, I should verify if she is still the current chancellor. Wait, there might have been changes. Alternatively, maybe the user is referring to multiple chancellors from different institutions Mandela attended? But Mandela's main alma mater is Fort Hare. He also studied law at the University of the Witwatersrand but didn't complete his degree there. So the primary alma mater is Fort Hare.

Now, the user is asking for the spouses of the current chancellors (plural) from that university. But Fort Hare has one chancellor. Unless there are multiple chancellors in different roles, but typically a university has one chancellor. Maybe the user is referring to vice-chancellors or other officials? Wait, the chancellor is a ceremonial role, while the vice-chancellor is the administrative head. But the question specifically mentions chancellors. So perhaps the user made a mistake, but I should proceed with the current chancellor of Fort Hare.

Assuming the current chancellor is Dr. Vuyo Mahlati, I need to find out her spouse and their birth date. However, upon checking, Dr. Vuyo Mahlati passed away in 2021. Wait, that complicates things. If she was appointed in 2021 but passed away the same year, then the current chancellor might be someone else now. Let me check the latest information. 

As of 2023, the University of Fort Hare's chancellor is Dr. Mvuyo Tom. He was appointed after Dr. Mahlati's passing. So Dr. Mvuyo Tom is the current chancellor. Now, I need to find out his spouse's name and birth date. However, information about the personal lives of university chancellors, especially their spouses' birth dates, might not be publicly available. Public figures often keep such details private. 

Alternatively, maybe the user is referring to the chancellor's spouse in general terms. If I can't find the spouse's name, I might have to state that the information isn't publicly disclosed. Additionally, the birth dates of spouses might not be readily available unless they are public figures themselves. 

So, putting it all together: Nelson Mandela's alma mater is the University of Fort Hare. The current chancellor is Dr. Mvuyo Tom. Information about his spouse and their birth date isn't publicly available. Therefore, the answer would address that the spouse's details aren't disclosed, and confirm the current chancellor's name.
</think>

Nelson Mandela's alma mater is the University of Fort Hare in South Africa. As of the latest available information, the current chancellor of the university is **Dr. Mvuyo Tom** (appointed in 2022). Details about the spouses of chancellors, including their names or birth dates, are not typically publicly disclosed unless the individuals themselves are public figures. There is no readily accessible information about Dr. Tom's spouse or their birth date. 

For accuracy, always verify with the university’s official communications or recent reputable sources, as leadership roles and personal details can change or remain private.

Settings used
model-name: DeepSeek R1
model: deepseek-r1
temperature: 0.5
top_p: 0.5
```

```Text
// SYSTEM: You are a helpful assistant

USER: Who are the spouses of the current chancellors from where Nelson Mandela got his alma mater and when were they born.

ASSISTANT: Nelson Mandela attended the University of Fort Hare, which was one of his alma maters. However, I don't have current information about the personal details of spouses of university chancellors or their birthdays, as this typically falls under private information and isn't publicly disclosed in a detailed manner. If you are looking for specific biographical details about public figures, it may be best to consult official university websites or press releases.

Settings used
model-name: OpenAI GPT-4o (External)
model: openai-gpt4o
temperature: 0.5
top_p: 0.5
```
<img width="439" alt="image" src="https://github.com/user-attachments/assets/97233906-f243-4dfd-961e-75fee2dac394" />

## 2-hop Question
Q: Who are the current chancellors from where Nelson Mandela got his alma mater from?

A: University of Fort Hare Current Chancellor: Dumisa Ntsebeza, 
University of London Current Chancellor: Anne, Princess Royal,
University of South Africa Current Chancellor: Thabo Mbeki,
University of the Witwatersrand Current Chancellor: Judy Dlamin

Even on a relatively simpler complex question, we can see ChatGPT o1 returns the correct Universities and chancellors of only 3 universities. DeepSeek R1 also performs similarly except it provides the wrong Chancellor for the University of Fort Hare and ChatGPT 4o returns 1 correct chancellor and 2 correct universities. Meanwhile, my architecture returns all 4 University-Chancellor pairs correctly.

```Text
SYSTEM: You are a helpful assistant

USER: Who are the current chancellors from where Nelson Mandela got his alma mater from and what are the alma maters

ASSISTANT: Nelson Mandela pursued his studies at several South African universities, but the two institutions from which he formally received degrees were:

• The University of Fort Hare (he received his B.A.)  
• The University of South Africa (UNISA; he eventually completed his LL.B. there)

He also studied law at the University of the Witwatersrand (often called “Wits”)—although he did not finish his degree there, it is still closely associated with his early legal training. Below are the current chancellors of each university:

1) University of Fort Hare  
   – Current Chancellor: Dumisa Buhle Ntsebeza SC  

2) University of the Witwatersrand  
   – Current Chancellor: Dr. Judy Dlamini  

3) University of South Africa (UNISA)  
   – Current Chancellor: Thabo Mbeki  

Those three institutions are generally cited as Mandela’s most significant alma maters, with Fort Hare and UNISA being the ones from which he graduated.

Settings used
model-name: OpenAI o1 (External)
model: openai-o1
temperature: 0.5
top_p: 0.5
```

```Text
SYSTEM: You are a helpful assistant

USER: Who are the current chancellors from where Nelson Mandela got his alma mater from and what are the alma maters

ASSISTANT: <think>
Okay, let's tackle this question. The user is asking about the current chancellors from the institutions where Nelson Mandela got his alma mater, and also what those alma maters are. 

First, I need to confirm Nelson Mandela's alma maters. From what I remember, Mandela attended the University of Fort Hare and the University of South Africa (UNISA). Let me double-check that. Yes, he studied at Fort Hare but didn't complete his degree there due to political activism. He later completed his BA through UNISA while in prison. He also studied law at the University of the Witwatersrand but didn't graduate there. So his main alma maters are Fort Hare and UNISA.

Next, the user wants the current chancellors of these universities. For the University of Fort Hare, I need to find out who the current chancellor is. I recall that in South African universities, the chancellor is a ceremonial role, often held by notable figures. Let me check recent sources. As of 2023, the chancellor of the University of Fort Hare is Ms. Baleka Mbete, a former Speaker of the National Assembly and Deputy President of South Africa. 

For UNISA, the University of South Africa, the current chancellor is former President Thabo Mbeki. He was appointed in 2021, I believe. Let me verify that. Yes, Thabo Mbeki became chancellor of UNISA in December 2021, succeeding Dr. Matamela Cyril Ramaphosa, who is now the President of South Africa.

So putting it all together: Mandela's alma maters are the University of Fort Hare and UNISA. Their current chancellors are Baleka Mbete and Thabo Mbeki respectively. I should also mention that Mandela's time at Fort Hare was significant in shaping his political views, even though he didn't graduate there initially. At UNISA, he completed his degree via correspondence, which is notable given his circumstances at the time.
</think>

Nelson Mandela's primary alma maters are the **University of Fort Hare** and the **University of South Africa (UNISA)**. Here are the current chancellors of these institutions as of the latest available information:

### 1. **University of Fort Hare**  
   - **Current Chancellor**: **Ms. Baleka Mbete** (appointed in 2019).  
     She is a prominent South African politician, former Speaker of the National Assembly, and former Deputy President of South Africa.  
   - **Mandela's Connection**: Mandela studied at Fort Hare in the early 1940s but left without completing his degree due to political activism. He later completed his BA through UNISA.

### 2. **University of South Africa (UNISA)**  
   - **Current Chancellor**: **Former President Thabo Mbeki** (appointed in 2021).  
     He served as President of South Africa from 1999 to 2008.  
   - **Mandela's Connection**: Mandela earned his **Bachelor of Laws (LLB)** degree through UNISA via correspondence while imprisoned on Robben Island (1989).  

### Additional Note:  
Mandela also attended the **University of the Witwatersrand (Wits)** to study law in the 1940s but did not graduate there. The current chancellor of Wits is **Dr. Judy Dlamini**, a businesswoman and academic (appointed in 2022). However, since Mandela did not graduate from Wits, it is not typically listed as his alma mater.  

Let me know if you'd like further details!

Settings used
model-name: DeepSeek R1
model: deepseek-r1
temperature: 0.5
top_p: 0.5
```

```Text
SYSTEM: You are a helpful assistant

USER:  Who are the current chancellors from where Nelson Mandela got his alma mater from and what are the alma maters

ASSISTANT: Nelson Mandela attended the University of Fort Hare and later, the University of South Africa (UNISA), among other institutions. As of the latest information available up to 2023:

1. **University of Fort Hare**: The chancellor of the University of Fort Hare is generally a ceremonial position, and the current details might change over time. It's recommended to check the university's official website or contact them directly for the most current information.

2. **University of South Africa (UNISA)**: The Chancellor of UNISA as of the latest available information is Thabo Mbeki, former President of South Africa. To get updated or verify this information, you can visit UNISA's official website or contact them directly.

For the most accurate and current details, checking the respective university websites or official announcements would be the best approach.

Settings used
model-name: OpenAI GPT-4o (External)
model: openai-gpt4o
temperature: 0.5
top_p: 0.5
```
<img width="428" alt="image" src="https://github.com/user-attachments/assets/1b3b0d92-33a2-408a-99ea-caa19e42e7e3" />


