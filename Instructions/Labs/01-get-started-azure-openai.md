# Lab 01: Get started with Azure OpenAI Service

Azure OpenAI Service brings the generative AI models developed by OpenAI to the Azure platform, enabling you to develop powerful AI solutions that benefit from the security, scalability, and integration of services provided by the Azure cloud platform. In this exercise, you'll learn how to get started with Azure OpenAI by provisioning the service as an Azure resource and using Azure OpenAI Studio to deploy and explore OpenAI models.

This exercise takes approximately **40** minutes.

## Task 1: Provision an Azure OpenAI resource

Before you can use Azure OpenAI models, you must provision an Azure OpenAI resource in your Azure subscription.

1. Once you are logged in to the Azure Portal, create an **Azure OpenAI** resource with the following settings:
    - **Subscription**: An Azure subscription that has been approved for access to the Azure OpenAI service.
    - **Resource group**: Create a new resource group with a name of your choice.
    - **Region**: Choose any available region.
    - **Name**: A unique name of your choice.
    - **Pricing tier**: Standard S0
2. Wait for deployment to complete. Then go to the deployed Azure OpenAI resource in the Azure portal.

## Task 2: Deploy a model

Azure OpenAI provides a web-based portal named **Azure OpenAI Studio**, that you can use to deploy, manage, and explore models. You'll start your exploration of Azure OpenAI by using Azure OpenAI Studio to deploy a model.

1. On the **Overview** page for your Azure OpenAI resource, use the **Explore** button to open Azure OpenAI Studio in a new browser tab.
2. In Azure OpenAI Studio, create a new deployment with the following settings:
    - **Model name**: text-davinci-003
    - **Deployment name**: text-davinci

> **Note**: Azure OpenAI includes multiple models, each optimized for a different balance of capabilities and performance. In this exercise, you'll start with the **Davinci** model from the **GPT-3** family of text generation models. **text-davinci-003** is a good general model for summarizing and generating natural language. For more information about the available models in Azure OpenAI, see [Models](https://learn.microsoft.com/azure/cognitive-services/openai/concepts/models) in the Azure OpenAI documentation.

## Task 3: Explore a model in the Completions playground

*Playgrounds* are useful interfaces in Azure OpenAI Studio that you can use to experiment with your deployed models without needing to develop your own client application.

1. In Azure OpenAI Studio, in the left pane under **Playground**, select **Completions**.
2. In the **Completions** page, ensure your **text-davinci** deployment is selected and then in the **Examples** list, select **Summarize an article (abstractive)**.

    The summarize text sample consists of a *prompt* that provides some text, starting with the line **Provide a summary of the text below...**. Starting the prompt with this sentence tells the model to summarize the following block of text.

3. At the bottom of the page, note the number of *tokens* detected in the text. Tokens are the basic units of a prompt - essentially words or word-parts in the text.
4. Use the **Generate** button to submit the prompt to the model and retrieve a response.

    The response consists of a summary of the original text. The summary should communicate the key points from the original text in less verbose language.

5. Use the **Regenerate** button to resubmit the prompt, and note that the response may vary from the original one. A generative AI model can produce new language each time it's called.
6. Under the summarized response, add a new line and enter the following text:

    *How has AI advanced?*

7. Use the **Generate** button to submit the new prompt and review the response. The previous prompt and response provide context in an ongoing dialog with the model, enabling the model to generate an appropriate answer to your question.
8. Replace the entire contents of the prompt with the following text:

    *Provide a summary of the text below that captures its main idea.* 
    
    *Azure OpenAI Service provides REST API access to OpenAI's powerful language models including the GPT-4, Codex and Embeddings model series. These models can be easily adapted to your specific task including but not limited to content generation, summarization, semantic search, and natural language to code translation. Users can access the service through REST APIs, Python SDK, or our web-based interface in the Azure OpenAI Studio.*

9. Use the **Generate** button to submit the new prompt and verify that the model summarizes the text appropriately.

## Task 4: Use a model to classify text

So far, you've seen how to use a model to summarize text. However, the generative models in Azure OpenAI can support a range of different types of task. Let's explore a different example; *text classification*.

1. In the **Completions** page, ensure your **text-davinci** deployment is selected and then in the **Examples** list, select **Classify text**.

    The classify text sample prompt describes the context for the model in the form of an instruction to classify a news article into one of a range of categories. It then provides the text for the news article (prefixed by *News article:*) and ends with *Classified category:*. The intention is that the model "completes" the final line of the prompt by predicting the appropriate category.

2. Use the **Generate** button to submit the prompt to the model and retrieve a response. The model should predict an appropriate category for the news article.
3. Under the predicted category, add the following text:

    *news article: Microsoft releases Azure OpenAI service. Microsoft corporation has released an Azure service that makes OpenAI models available for application developers building apps and services in the Azure cloud.*

    *Classified category:*

4. Use the **Generate** button to continue the dialog with the model and generate an appropriate categorization for the new news article.

## Task 5: Explore prompts and parameters

Up until now, you've based your prompts on examples that are provided in Azure OpenAI Studio. Let's try something different.

1. Replace all of the text in the prompt area with the following text:

    *You are a teacher creating a test for your students.*

    *Write three multiple choice questions based on the following text.*

    *Most computer vision solutions are based on machine learning models that can be applied to visual input from cameras, videos, or images.*

    *\- Image classification involves training a machine learning model to classify images based on their contents. For example, in a traffic monitoring solution you might use an image classification model to classify images based on the type of vehicle they contain, such as taxis, buses, cyclists, and so on.*

    *\- Object detection machine learning models are trained to classify individual objects within an image, and identify their location with a bounding box. For example, a traffic monitoring solution might use object detection to identify the location of different classes of vehicle.*

    *\- Semantic segmentation is an advanced machine learning technique in which individual pixels in the image are classified according to the object to which they belong. For example, a traffic monitoring solution might overlay traffic images with "mask" layers to highlight different vehicles using specific colors.*

2. In the **Parameters** pane, set the following parameter values:
    - **Temperature**: 0
    - **Max length (tokens)**: 500
    - **Pre-response text**: Auto-generated questions. Validate before using in a test:
3. Use the **Generate** button to submit the prompt and review the results, which should consist of the value in the *pre-response text* parameter followed by multiple-choice questions that a teacher could use to test students on the computer vision topics in the prompt. The total response should be smaller than the maximum length you specified as a parameter.

    Observe the following about the prompt and parameters you used:

    - The prompt includes natural language context information that instructs the model on how to behave. Specifically, it indicates that the model should assume the role of a teacher creating a test for students.
    - The parameters include *Temperature*, which controls the degree to which response generation includes an element of randomness. The value of **0** used in your submission minimizes randomness, resulting in stable, predictable responses.

4. Use the **Regenerate** button to regenerate the response. It should be similar to the previous response.
5. Change the **Temperature** parameter value to **0.9** and then use the **Regenerate** button to regenerate the response. This time the increased degree of randomness should result in a different response. However, the questions are more likely to contain inaccuracies than the ones in the previously generated response.

## Task 6: Explore code-generation

The **text-davinci** model you deployed is a good general model that can handle most tasks well. However, in some cases it's better to choose a model that is optimized for a specific kind of task. For example, Azure openAI models can be used to generate computer code rather than natural language text, and some models have been optimized for that task.

1. In Azure OpenAI Studio, view the **Models** page; which lists all of the available models in your Azure OpenAI service resource.
2. Select the **code-davinci-002** model and use the **Deploy model** button to deploy it with the deployment name **code-davinci**.
3. After deployment is complete, in Azure OpenAI Studio, view the **Deployments** page; which lists the models you've deployed.
4. Select the **code-davinci** model deployment and use the **Open in Playground** button to open it in the playground.
5. In the **Completions** page, ensure your **code-davinci** deployment is selected and then in the **Examples** list, select **Natural language to SQL**.

    The natural language to SQL sample prompt provides details of tables in a database, and a description of the query that is required followed by the `SELECT` keyword. The intention is for the model to complete the `SELECT` statement to create a query that satisfies the requirement.

6. Use the **Generate** button to submit the prompt to the model and retrieve a response, which consists of a SQL `SELECT` query.
7. Replace the entire prompt and response with the following new prompt:

    *# Python 3*

    *# Create a function to print "Hello " and a specified string*

    *def print_hello(s):*

8. Use the **Generate** button to submit the prompt and view the code that gets generated. The prompt included an indication of the programming language to be generated (Python 3), a comment describing the desired functionality, and the first part of the function definition. The **code-davinci** model should have completed the function with appropriate Python code.

## Task 7: Explore models for chat

ChatGPT is a chatbot developed by OpenAI that can provide a wide variety of natural language responses in a conversational scenario. The model used by ChatGPT and APIs for using it are included in Azure OpenAI.

1. In Azure OpenAI Studio, view the **Models** page; which lists all of the available models in your Azure OpenAI service resource.
2. Select the **gpt-35-turbo** model and use the **Deploy model** button to deploy it with the deployment name **gpt-chat**.
3. After the model is deployed, in the **Playground** section, select the **Chat** page, and ensure that the **gpt-chat** model is selected in the pane on the right.
4. In the **Assistant setup** section, in the **System message** box, replace the current text with the following:

    *The system is an AI teacher that helps people learn about AI*

5. Below the **System message** box, click on **Add few-shot examples**, and enter the following message and response in the designated boxes:

    User: *What are different types of artificial intelligence?*

    Assistant: *There are three main types of artificial intelligence: Narrow or Weak AI (such as virtual assistants like Siri or Alexa, image recognition software, and spam filters), General or Strong AI (AI designed to be as intelligent as a human being. This type of AI does not currently exist and is purely theoretical), and Artificial Superintelligence (AI that is more intelligent than any human being and can perform tasks that are beyond human comprehension. This type of AI is also purely theoretical and has not yet been developed).*

    > **Note**: Few-shot examples are used to provide the model with examples of the types of responses that are expected. The model will attempt to reflect the tone and style of the examples in its own responses.

6. Save the changes to start a new session and set the behavioral context of the chat system.

7. In the query box at the bottom of the page, enter the following text:

    *What is artificial intelligence?*

8. Use the **Send** button to submit the message and view the response.

    > **Note**: You may receive a response that the API deployment is not yet ready. If so, wait for a few minutes and try again.

9. Review the response and then submit the following message to continue the conversation:

    *How is it related to machine learning?*

10. Review the response, noting that context from the previous interaction is retained (so the model understands that "it" refers to artificial intelligence).

In this exercise, you've learned how to provision the Azure openAI service in an Azure subscription, and how to use Azure OpenAI Studio to deploy and explore models.

As a developer, you can use the REST interface and language-specific APIs to create apps and services that consume Azure OpenAI models; enabling you to leverage generative AI models in your own applications. Coding against Azure OpenAI is covered in other exercises.
