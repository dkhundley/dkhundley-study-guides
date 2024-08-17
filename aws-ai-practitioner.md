# AWS AI Practitioner Study Guide
This page contains my notes for the new AWS AI practitioner certification. The goal is to cover the high level objectives you’ll need to know for the exam. If you would like a specific deep dive on anything, I would recommend referencing additional material, including the study resources I recommend below.



## Study Resources
While I personally already have a lot of experience working with AI on AWS, I’m still glad I opted to check out these study materials to refine my knowledge on pieces I don’t work with as often. Specifically, I leveraged the following two resources on Udemy by Stephen Maarek, who has produced a number of great AWS courses that I’ve taken historically for other AWS exams.

- [**Video Course**](https://www.udemy.com/share/10bvuD3@1rKUZUHRjAzbnkdoKBdveLxMgZEnHJX0NBmYNP7668Q3DtlXfdKGh8Omk6qOdsY=/): This course contains a number of videos about each objective covered in the exam.
- [**Practice Exams**](https://www.udemy.com/share/10bvwn3@J-lVKxcoTQj-kkUgkwxUnT9dpQMk5vrDLG0AniHwoeut-PNUcU-8_W6QTXL8l90=/): Complementary to the video course above, these practice tests will allow you to hone your knowledge with realistic questions that you may encounter on the exam itself. The practice exams also explain the intuition behind why a question’s correct answer is what it is.



## Study Notes
We’ll now move into my personal study notes. The notes will largely correlate to how the sections are laid out in the video course referenced above, but it is not particularly necessary to review the course to make sense of my notes. My notes also come from my own personal experience working with these services on AWS.



### Artificial Intelligence (AI) & Machine Learning (ML)
In this section, we’ll cover an introduction to just what is artificial intelligence (AI) and machine learning (ML). If you want a deeper dive on any of these concepts, I would again recommend the Udemy course linked above. Active practitioners in the AI/ML space can probably skip this section. (Note: I’m deviating from the ordering of the Udemy course here. This section doesn’t come until later in the course, but I personally thought it made more sense to bring it to the forefront.)

- **Artificial Intelligence (AI)**: AI is a broad term to refer to when a machine emulates human-like intelligence. When I mean human-like intelligence, I mean a range of activities from classifying shapes, speaking verbally in words, recognizing people in images, and many more things that we as humans can do via natural biological processes. AI today largely manifests as advanced statistical processes that we refer to as machine learning, but AI is not necessarily limited to only manifesting as machine learning. Robotics are also considered a form of AI.
- **Machine learning (ML)**: Machine learning is a subset of AI, and much of what we know as AI today manifests as machine learning. Machine learning (ML) is an advanced statistical processes that can learn to generalize patterns in data after being exposed to that data in what we refer to as **model training**. For a simple example, think about the weather. If we wanted to train an AI model to predict tomorrow’s weather, we would feed it lots of data from previous years so that the mathematical algorithm underlying the ML model can learn, “Oh yes, it’s hot in the summer and cold in the winter.”
- **Deep learning (DL)**: When machine learning first came around, it manifested in simpler, structured datasets. (Imagine big Excel spreadsheets.) With things like images or audio files, the means of creating AI models around them began to require many, many more parameters than a standard deep learning model. Because of their emulation of the brain, deep learning models have manifested in what we refer to as **neural networks**. Because these neural networks go so deep on how many parameters they require, we refer to this more nuanced branch of machine learning as deep learning. Part of this distinction also is a bit of a shorthand expression to say, “You’re going to need specialized hardware for this.” A commodity laptop, like your own personal laptop, would struggle to train a deep learning model. Deep learning models often require **graphical processing units (GPUs)**. (Which is why NVIDIA’s stock is doing so well, since they are the world’s most prevalent manufacturer of GPUs!)
- **Generative AI (GenAI)**: Generative AI (or GenAI) is a more recent subset of deep learning that has become popularized since the development of the **Transformer architecture** in 2017. GenAI allows a user to generate some content based on content that the GenAI model has been trained on. For example, you may be familiar with ChatGPT. ChatGPT would be considered a text-based GenAI model that can produce text based on what the user’s input prompt is. (Note: We cover more on prompts and prompt engineering in a later section.)



### Intro to AWS & Cloud Computing
Being a “foundation” level exam, there are a few correlates over to the more general Cloud Practitioner exam. These things are about AWS in general and are NOT specific to anything related to AI.

- **IAM**: Standing for Identity & Access Management, IAM shows up in all AWS exams, and for good reason! This is the service that enforces who can do what in your AWS account, including non-human resources. Getting your IAM roles and policies in order is of UTMOST importance when enforcing security of your company’s information!!
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



### Amazon Q
Generally speaking, Amazon Q is currently AWS’s initiative to bring Generative AI to all aspects of AWS. I honestly expect this to evolve beyond Q over time, but for now, the exam covers the bulleted information below.

- **Available models**: As of today, you may only use models from within AWS Bedrock for the Amazon Q services. This specifically means that using the OpenAI models are not allowed today.
- **Amazon Q Business**: This is a GenAI assistant for your business, such as providing summaries, generating content, and performing routine tasks. In order to make use of this service, you WILL have to expose your company or personal information to the service!! It can connect to 40+ different services (e.g. S3, RDS, Aurora) via data connectors. You can also use 3rd party plugins. Users are managed with IAM.
- **Amazon Q Apps**: This is a subservice of Amazon Q Business. It is designed to allow a user to create a web-based application using natural language.
    - David’s note: I’m sure this service will significantly improve over time, but as of today, I can say with confidence that most companies probably don’t want to use this service. This is because many companies, especially larger corporations, adhere to UX standards, like specific Hex values for colors and the like. Strictly enforcing those UX standards can be a tricky thing to do, and relying on AI to do that today is not the most prudent decision. (Again, I expect my opinion to change over time as the AI technology improves!)
- **Amazon Q Developer**: Amazon Q Developer can answer questions about AWS documentation and resources in your AWS account. (E.g. “List all my AWS Lambda functions.”) Another facet of Amazon Q Developer also works as an AI code companion similar to GitHub Copilot.