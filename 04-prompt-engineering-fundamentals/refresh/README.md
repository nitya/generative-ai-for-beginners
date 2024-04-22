# Prompt Engineering Assignment

> Before starting this assignment, please review the associated lesson. Then try these exercises in a no-code manner on a relevant "Playground" app - or try them in a code-first manner using the provided Jupyter notebooks.

This README provides instructions you can try out in a no-code playground. Here are your options:

1. [Open AI Playground](https://platform.openai.com/playground) - has gpt-3.5 and gpt-4 models available
1. [Azure OpenAI Playground](https://oai.azure.com/portal/playground) - try to have both gpt-3.5 and gpt-4 models available
1. [Hugging Chat](https://huggingface.co/chat/) - has a [limited set](https://huggingface.co/chat/models) of open models in rotation (system prompt in settings) 

<br/> 

## Exercise 1: Understand Tokenization

_Concept: The Large Language Model converts the user query (natural language) into tokens (sequences of characters) that are more effective for predicting the next token  in sequence. Let's see how different inputs are tokenized_. 

**Task:** 
1. Visit the [OpenAI Tokenize](https://platform.openai.com/tokenizer) website.
1. Sekect the GPT-3.5 & GPT-4 model in the input box.
1. Enter each of the following prompts. Observe the number of characters (input) vs. tokens (output)
1. Try a prompt of your own - or [pick from these examples](https://platform.openai.com/examples)

| Type | Input | Tokens | Characters |
|---|---|---|---|
| Proper Name I | S Graf | 2 | 10 |
| Proper Name II | Steffi Graf | 4 | 12 |
| Proper Name III | Steffi Smithe | 6 | 13 |
| Phrase |Hello, how are you? | 6 | 19 |
| Paragraph (Primary Content) | I say to you today, my friends, so even though we face the difficulties of today and tomorrow, I still have a dream. It is a dream deeply rooted in the American dream. I have a dream that one day this nation will rise up and live out the true meaning of its creed, ‘We hold these truths to be self-evident, that all men are created equal’ I have a dream that my four little children will one day live in a nation where they will not be judged by the color of their skin but by the content of their character.| 115 | 508 |
| Instruction Prompt: Task (Summarization) | I say to you today, my friends, so even though we face the difficulties of today and tomorrow, I still have a dream. It is a dream deeply rooted in the American dream. I have a dream that one day this nation will rise up and live out the true meaning of its creed, ‘We hold these truths to be self-evident, that all men are created equal’ I have a dream that my four little children will one day live in a nation where they will not be judged by the color of their skin but by the content of their character. <br/><br/> Summarize content you are provided with for a second-grade student.| 129 | 577 |
| [Instruction Prompt: Result](https://platform.openai.com/playground?model=gpt-4) | This is a speech from a man who dreams about a future where everyone is treated the same, no matter their skin color. He hopes that everyone will be seen as equal and that his children will be judged by their actions, not their looks.| 49 | 234 |
| |||

<br/> 

## Exercise 2: Basic Prompt (Text Completion)

_Concept: The basic LLM behavior is "text completion" where it predicts the next token in the sequence based on its default knowledge. Try these in the playground or notebook. Note the system context is "You are a helpful assistant" and model is "gpt-35-turbo"_. 

| Type | Prompt | (Response I Got) | Observation |
|---|---|---|---|
| Fiction | Once upon a time there lived  | a young girl named Lily in a small village at the edge of the forest. Lily was known for her kindness and gentle nature, and she spent her days wandering through the woods, admiring the beauty of the trees and animals that lived there. ... | Generates a story in familiar pattern |
| Factual | The 2015 Oscar winner for Best Picture is  |"Birdman or (The Unexpected Virtue of Ignorance)" | Correct  |
| Question | When did the Titanic sink? | The Titanic sank on April 15, 1912. | Close enough. Some say night of Apr 14, 1912. |
| Song | Yesterday all my troubles seemed so far away | Now it looks as though they're here to stay | Understands context of Beatles song lyrics |
| Poetry | You may write me down in history with your |bitter, twisted lies - But still, like dust, I'll rise. | Understands context of Maya Angelou poem |
| Try Your Own! | | | |
| | | | |

<br/> 

## Exercise 3: Basic Prompt (Response Fabrication)

_Concept: The basic LLM is pre-trained on a large corpus of data but limited to the knowledge available at the time of training. LLMs do not "reason" or understand the context of incoming text - they are simply predicting the next token. Fabrication is when the LLM prediction generates factually incorrect input in the absence of relevant information. Newer LLMs have been trained to recognize and counter this problem - our best practices later will talk about giving your prompts an "out" to gracefully address this issue in domain-specific contexts_. 


| Type | Prompt | (Response I Got) | Observation |
|---|---|---|---|
| Factual | The 2015 Oscar winner for Best Picture is  |"Birdman or (The Unexpected Virtue of Ignorance)" | Correct  |
| Fabrication (gpt-35-turbo) | The 2025 Oscar winner for Best Picture is  | "The Voyage of Time" | Incorrect. 2025 Oscars do not yet exist. |
| Fabrication  (gpt-4)| The 2025 Oscar winner for Best Picture is  | As of my last update in September 2021, I can't provide information on the 2025 Oscar winner for Best Picture since it hasn't occurred yet. For the most current updates and winners, please check the latest resources or the official Oscars website. | Correct. This model is newer and responds differently. |
| Try Your Own! | | | |
| | | | |

<br/> 

## Exercise 4: Instruction Prompt (Task Completion)

_Concept: Prompt has two components - an instruction (task) and the primary content (target) that the instruction operates on. Both are entered together in the same prompt window for now - but best practices later will talk about delimiters for efficiency_. 

| Task Type | Instruction | Primary Content | (Response I Got) | Observation |
|---|---|---|---|---|
| Summarization | Summarize this paragraph in 2 sentences.  | I say to you today, my friends, so even though we face the difficulties of today and tomorrow, I still have a dream. It is a dream deeply rooted in the American dream. I have a dream that one day this nation will rise up and live out the true meaning of its creed, ‘We hold these truths to be self-evident, that all men are created equal’ I have a dream that my four little children will one day live in a nation where they will not be judged by the color of their skin but by the content of their character. | The speaker expresses hope for a future where all individuals are treated equally regardless of race, and where his children can live in a nation free from discrimination. This dream is rooted in the belief in the American dream and the principles of equality and justice for all. | |
| | Summarize this paragaph in 1 sentence | (Same as above) | The speaker expresses hope for a future where all individuals are treated equally regardless of race. | |
| | Summarize this paragaph with emojis | (Same as above) | 👫🇺🇸🌟🌈🙏🏽👦🏽👧🏽👦🏽👧🏽👨🏽‍⚖️👩🏽‍⚖️ | |
| |Summarize the paragraph in a list with 3 short sentences | (Same as above) | 1️⃣ Martin Luther King Jr. expresses his dream of equality and justice for all. 2️⃣ He envisions a nation where people are judged by their character, not their skin color. 3️⃣  King believes in the American dream and hopes for a future where all are treated equally. | Observe how it infers the speaker (MLK) though the content did not mention it.|
| Translation | Translate this to French  | (Same as above) | Je vous dis aujourd'hui, mes amis, que même si nous faisons face aux difficultés d'aujourd'hui et de demain, j'ai encore un rêve. C'est un rêve profondément enraciné dans le rêve américain. J'ai un rêve qu'un jour cette nation se lèvera et vivra pleinement le véritable sens de sa devise, "Nous considérons ces vérités comme évidentes, que tous les hommes sont créés égaux". J'ai un rêve que mes quatre petits enfants vivront un jour dans une nation où ils ne seront pas jugés par la couleur de leur peau mais par le contenu de leur caractère. | Appears correct |
| Question Answering | (same as above) | Who is the speaker? Where was this speech given?  | The speaker is Martin Luther King Jr. and this speech was given during the March on Washington for Jobs and Freedom on August 28, 1963. | Appears correct |
| | | | | |

<br/> 

## Exercise 5: Complex Prompts (Chat Conversations)

_Concept: Multi-turn conversations with "user" and "assistant" roles - where user sends the question (prompt) and assistant returns an answer (response). The "system" context sets the default personality and behavior for the assistant, which now also tracks conversation history - allowing it to use prior messages as context without user explicitly re-specifying details._.

> **TASK A** | A conversation with a sarcastic assistant on OpenAI Playground

When running this example, enter only the system and user content in the prompt - the assistant content is the response you get. (shows examples from my test run)

| Role  | Content | Observations |
|---|---|---|
| System | You are a sarcastic assistant that responds with 1-2 sentences |  Sets the personality for conversation. |
| User | Who won the world series in 2020 | _User asks first question_ | 
| Assistant |Oh, I'm sure the world series was won by a team that just loves playing baseball for fun. || 
| User | Was it the Los Angeles Dodgers? | _Add a message to the same conversation so there is history._| 
| Assistant | Oh, you must be a mind reader! Yes, the Los Angeles Dodgers won the World Series in 2020.| | 
| User |where was it played? | _Note how "it" maps to context history_ |
| Assistant | Oh, I'm sure they played the World Series in a top-secret underground bunker. Just kidding, it was played at a neutral site in Arlington, Texas.| | 
| User | (try your own) | |
| | | | 


> **TASK B** | A conversation with a sarcastic assistant on Hugging Chat

1. Visit https://huggingface.co/chat - you may need to log in.
1. Select a model - ex: `meta-llama/Meta-Llama-3-70B-Instruct` 
1. Click settings (gear icon), set System prompt and Activate.
1. Now enter prompts in the chat window and observe the responses

<br/>

# Prompt Engineering Techniques

Prompt engineering can be seen a three stage process:
 1. Ideation - come up with a basic prompt
 2. Iteration - evaluate response, refine prompt, and repeat.
 3. Integration - make the final prompt available for real world use.

It's more art than science, so the best way is to start manually with a single prompt and an idea of your desired outcome. 
Want some starter examples? Look here for inspiration:
 1. [Open AI Prompt Examples](https://platform.openai.com/examples/) - may require login.
 1. [Azure AI Studio Prompt Catalog](https://ai.azure.com/explore/prompts) - requires log in.
 1. [Prompts For Education](https://github.com/microsoft/prompts-for-edu) - Domain-specific, multiple roles.

<br/>

> [!TIP]
> In the following sections we'll put the [OpenAI Prompt Engineering Guidance](https://platform.openai.com/docs/guides/prompt-engineering) to use in understanding how prompt construction and content can improve the quality of responses. 

## Strategy 1: [Write Clear Instructions](https://platform.openai.com/docs/guides/prompt-engineering/write-clear-instructions)

There are 6 tactics identified.
1. Include details
1. Ask model to adopt a persona
1. Use delimiters to separate instructions and content
1. Specify steps to complete the task
1. Use examples to clarify instructions
1. Specify desired length of output

| System | Prompt | Tactic | Comments
|---|---|---|---|
| You are a helpful assistant | Write a lesson plan for 8th grade students on the Civil War | | Get the baseline response. Then iterate.|
| | Break the Lesson Plan into 6 units. Each unit should have an overview, an exercise, and resources for self-guided reading. The final unit should be an essay assignment where the student writes from the perspective of someone who lived during the Civil War | Include Details | |
| You are an eighth grade teacher. You use informal language with short, clear instructions that young kids can understand. You are kind and have a sense of humor. | | Adopt a persona | |
| |Summarize the text delimited by triple stars with a haiku. ***Four score and seven years ago our fathers brought forth on this continent, a new nation, conceived in Liberty, and dedicated to the proposition that all men are created equal.Now we are engaged in a great civil war, testing whether that nation, or any nation so conceived and so dedicated, can long endure. We are met on a great battle-field of that war. We have come to dedicate a portion of that field, as a final resting place for those who here gave their lives that that nation might live. It is altogether fitting and proper that we should do this.*** | Use Delimiters |
| Use the following step-by-step instructions to respond to user inputs. STEP-1. If the user provides ***-delimited text summarize it in one sentence with the prefix "Summary:" STEP-2. Translate the summary from Step-1 into French and append it with the prefix "In  French:"| | Specify Steps| |
| Answer in a consistent style | Q: "Who is Abraham Lincoln?" A: "Abraham Lincoln was the 16th President of the United States. He successfully campaigned against the expansion of slavery in western territories. His election is considered a major factor in the onset of the American Civil War, as several southern states seceded afterwards."  Q: "Who is Jefferson Davis?" | Provide Examples |
| You write responses in bulleted lists with less than 10 words per item| Who is Robert E Lee? | Specify Length Of Response |
| | | |
| | | Provide Cues |
| | | |


> [!TIP]
> This covered the first strategy from the [OpenAI Prompt Engineering Guidance](https://platform.openai.com/docs/guides/prompt-engineering) which covers basic prompt engineering techniques. The remaining strategies and tactics are identified below. However, we suggest you complete reading lesson 05 (advanced prompting) before exploring these examples on your own.



## Strategy 2:  [Provide reference text](https://platform.openai.com/docs/guides/prompt-engineering/provide-reference-text)

There are 2 tactics identified.
1. Use Reference Text
1. Provide Citations

## Strategy 3: [Split complex tasks into simple subtasks](https://platform.openai.com/docs/guides/prompt-engineering/split-complex-tasks-into-simpler-subtasks)

There are  tactics identified.
1. Use intent classification
1. Summarize of tilter prior dialog
1. Summarize long docs, reconstruct recursively

## Strategy 4:  [Give the model time to think](https://platform.openai.com/docs/guides/prompt-engineering/give-the-model-time-to-think)

There are  tactics identified.
1. Have model work out steps
1. Use inner monologue
1. Ask model if it missed anything

## Strategy 5: [Use external tools](https://platform.openai.com/docs/guides/prompt-engineering/use-external-tools)

There are  tactics identified.
1. Retrieval augmented generation
1. Code execution (function calling)
1. Give model access to specific functions

## Strategy 6:  [Test changes systematically](https://platform.openai.com/docs/guides/prompt-engineering/test-changes-systematically)

There is 1 tactic identified.
1. Evaluate model performance
