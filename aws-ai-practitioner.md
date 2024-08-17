# AWS AI Practitioner Study Guide
This page contains my notes for the new AWS AI practitioner certification. The goal is to cover the high level objectives you’ll need to know for the exam. If you would like a specific deep dive on anything, I would recommend referencing additional material, including the study resources I recommend below.



## Study Resources
While I personally already have a lot of experience working with AI on AWS, I’m still glad I opted to check out these study materials to refine my knowledge on pieces I don’t work with as often. Specifically, I leveraged the following two resources on Udemy by Stephen Maarek, who has produced a number of great AWS courses that I’ve taken historically for other AWS exams.

- [**Video Course**](https://www.udemy.com/share/10bvuD3@1rKUZUHRjAzbnkdoKBdveLxMgZEnHJX0NBmYNP7668Q3DtlXfdKGh8Omk6qOdsY=/): This course contains a number of videos about each objective covered in the exam.
- [**Practice Exams**](https://www.udemy.com/share/10bvwn3@J-lVKxcoTQj-kkUgkwxUnT9dpQMk5vrDLG0AniHwoeut-PNUcU-8_W6QTXL8l90=/): Complementary to the video course above, these practice tests will allow you to hone your knowledge with realistic questions that you may encounter on the exam itself. The practice exams also explain the intuition behind why a question’s correct answer is what it is.



## Study Notes
We’ll now move into my personal study notes. The notes will largely correlate to how the sections are laid out in the video course referenced above, but it is not particularly necessary to review the course to make sense of my notes. My notes also come from my own personal experience working with these services on AWS.



### Intro to AWS & Cloud Computing
Being a “foundation” level exam, there are a few correlates over to the more general Cloud Practitioner exam. These things are about AWS in general and are NOT specific to anything related to AI.

- **Regions & Availability Zones**: Remember that all AWS regions have at least 3 availability zones (AZs).
- **Shared Responsibility Model**: AWS is responsible for security “of the cloud” while the customer is responsible for their resources “in the cloud”. For example, AWS is responsible for securing the physical data centers and servers themselves while the customer is responsible for setting things like database credentials to ensure only the right people have access.



### AWS Bedrock
This section covers everything specifically related to AWS Bedrock, which is the primary service that AWS uses to house foundation models.

- **What is GenAI?:** Per AWS, GenAI is a newer set of AI models that are used to generate new content based on content that it has seen before.
- **Foundation model (FM) vs. large language model (LLM)**: AWS defines a foundation model (FM) differently from a large language model (LLM). Specifically, it sees foundation models as being any GenAI model regardless of modality (e.g. text, audio, image, etc.) whereas LLMs are specifically focused on text generation.
- **Amazon Titan**: While Bedrock is a home for many different types of foundation models, Titan is the one created by AWS directly and offers text generation, text embedding, multimodal embedding, and image generation.
    - David’s note: I would expect this certification to focus more on this particular option in Bedrock than the other options; however, as of August 2024, the Titan models generally do not perform as well as the other options.
- **Pricing**: Pricing is generally based on usage, specifically priced at number of input / output tokens. The pricing may differ from model to model. You can also book a provisioned throughput for a set period of time.
- **Fine tuning**: Bedrock allows a user to fine tune specific models in Bedrock with a customer’s own data. The data must be in a specific format and must be located within S3. Only a select few models in Bedrock are available to be fine tuned.
- **Hyperparameters**: This can be a tricky context to learn, especially when compared to parameters. At the end of the day, a predictive, AI model is a fancy mathematical algorithm with lots of **parameters** that are trained on data during a model training period. (At the start of model training, the parameters are initialized randomly.) Hyperparameters, on the other hand, are external to this mathematical algorithm and are set statically, so they are not adjusted at all during model training. Still, hyperparameters can have a big influence. In the context of this specific exam, what you need to be aware of is that if you want a Generative AI model to behave a certain way, you’ll need to set a few of these hyperparameters. We’ll talk specifically about a few of those later on down in this guide.
- **Evaluation**: You can perform evaluation of a foundational model in Bedrock using your own custom benchmark questions and answers. You can also have humans in your organization perform this evaluation via the Bedrock service.
- **RAG**: RAG is a general concept that has recently come up alongside the GenAI revolution, and it stands for **retrieval augmented generation**. Essentially, it allows a user to get better answers from a foundational model by providing it with custom information, like your company’s own proprietary information. Oftentimes, this tactic is more cost effective yet just as performant as a fine tuning.
- **Bedrock Knowledge Base**: This is Bedrock’s implementation of a RAG service. Basically, you upload your information to S3 and behind the scenes, Bedrock Knowledge Base sets up a **vector database** to convert your information in S3 into vector embeddings stored in this database. By converting the text into vector embeddings, we can perform mathematical calculations to produce a **similarity score** to retrieve the most relevant documents per the user’s query. Options for this vector database backend include:
    - AWS OpenSearch (the most popular option)
    - AWS Aurora
    - MongoDB
    - Redis
    - Pinecone
- **Bedrock Guardrails**: This is the means to protect a company’s information by setting up these “guardrails” to prevent certain information from reaching the foundation model. For example, you might want to ensure that all Social Security numbers are scrubbed before they go to the foundation model for security reasons. Guardrails is designed to do just this. It can also be set to detect things like violence, hateful speech, prompt injection, and more. You can also create multiple Guardrails, each with a varying degree of settings.
- **Bedrock Studio**: This is a UI designed for users to work on their own prompt engineering and other things with the Bedrock models.
- **Agents**: AI agents are this concept that will fulfill a task without having particularly explicit instructions on how to complete that task. This is very different from the standard computer science world, where code is always very explicitly written in a precise, specific way.
    - David’s notes: While I admittedly haven’t tried Bedrock Agents, I have tried to create agents in other fashions using state of the art models. As of August 2024, I do not recommend using agents. Because they do have the “freedom” to do whatever they want, they often get stuck in a weird dead end or in an endless loop. In my opinion, they are currently too unreliable for business use. As technology progresses, I expect my opinion to change on the matter!



### Prompt Engineering
This section covers what prompt engineering is and a few tactics for optimization.

- **What is prompt engineering?**: Prompt engineering is the concept of refining your input into a foundation model (FM) to enhance and optimize your desired results. Ideal prompt engineering generally consists of…
    - **Instructions**: What you want the FM to do
    - **Context**: Information that the model may not have been exposed to to enhance results (see RAG above)
    - **Input data**: Any sort of input data
    - **Output format**: What you want the output to be formatted (e.g. “Give me a response in less than 50 words.”)
- **Negative prompting**: This is the concept of prompting to intentionally exclude specific content in the FM’s response.
- **System prompts**: System prompts are a “meta prompt” applied to any user query going forward. System prompts are often used by a chatbot owner to enforce things like friendliness and helpfulness. (Or, if you’re an idiot like me, this is where you tell it to answer like Jar Jar Binks.)
- **Temperature**: This is a value that can be tweaked to control the creativity of the model’s response. Temperature is often adjustable between 0-1 or 0-2. The higher the number, the more creative the response; the lower the number, the more deterministic the response.
    - David’s notes: For the exam, focus on the values ranging from 0-1. Technically speaking, the model can accept 1,000,000 as a value. It’s just that generally speaking, any temperature that exceeds a 1 or 2 starts to become nonsensical.
    - Another David note: For my computer science friends out there, temperature is NOT the same as a seed!! A seed fixes the outputs, while the temperature only makes them more deterministic. That means setting the temperature to zero, you are pretty likely to get the same results but NOT guaranteed like you would be with a seed number.
- **Top P**: Top P is another value that can be set to put a constraint on what probability of most likely words you want to surface in the model response. This value generally ranges between 0 and 1. A low P value (e.g. 0.25) would retrieve only the most likely words, where as a high P value (e.g. 0.99) would be more liberal in its range of likely words, producing a more diverse output. (Diverse in the sense of different kinds of words. If this value is set too high, you can imagine that your output could become incomprehensible!)
- **Top K**: Top K is very similar to Top P, but instead of being a percentage-like value, it’s a fixed value. For example, if you set Top K to equal 10, the model will respond with the top 10 most probable words. Again, a higher Top K generally influences a more creative output.
- **Length**: In the context of large language models, length refers to the number of tokens you want to set as a maximum response. If the model is still going once the length is hit, it halts its process and produces the output.
- **Stop sequences**: Behind the scenes, the model knows to stop producing an output because it will encounter a special “stop” token. Again, we as users of services like ChatGPT don’t see this in the UI, but it is indeed what is going on behind the scenes. Likewise, this field allows you to also use your own stop sequences to serve as that signal for the model to stop producing a response.
- **Zero-shot prompting**: This is the concept of providing a task to an FM without any sort of specific instructions nor examples.
- **Few-shot prompting**: As opposed to zero-shot prompting, this is when you would provide multiple examples of an expected output to help guide the FM toward your desired output. (Note: If you provide a single example, this is also called **one-shot prompting**.)
- **Chain of Thought prompting**: This is the concept of asking the FM to consider its output (“think step by step”) as it is being produced. Oftentimes, people have found that a model is able to provide a better sense of reasoning since it has to explicitly walk itself through each step without necessarily jumping to any conclusions.