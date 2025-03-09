# GitRAG

# Versions: The Critical and Missing Part of Code Generation

In this article, we use Pandas in a Python environment as an example to discuss the role of versions in Generative AI (GenAI) code generation.

## Current Versions of Pandas
 
The recent versions of Pandas are as follows:

- 2.2.3 (September 20, 2024)
- 2.2.2 (April 10, 2024)
-2.2.1 (February 22, 2024)
- 2.2.0 (January 19, 2024)
- 2.1.0 (August 30, 2023)
- 2.0.0 (April 3, 2023)
- 1.5.3 (January 18, 2023)

## Which Version of Pandas Are You Using?
 
The question of which Pandas version you are using can be confusing. You might always default to the version installed by your environment, lack the permissions to select a version, or only need basic Pandas functionalities.

## AI's Knowledge of Pandas Versions
 
I used the prompt “What is the latest version of Pandas? Give me a version number only” across several models. While intuition suggests different AI models might provide different answers, even the same model can yield varied responses over time. For instance, I queried OpenAI-4o-mini, with training data up to October 2023, 100 times and noted the version distribution.

<img src="./images/version freqency.png" alt="version freqency" title="version freqency">

This inconsistency highlights that AI might mix features from different versions, leading to confusion similar to that experienced by humans.

## Dealing with AI-Generated Code
 
If GenAI-generated code works seamlessly for you, that's great. However, many users find the code generation helpful yet frustrating due to occasional errors that are difficult to diagnose. Even advanced workflows, such as reflection patterns, may not work well if AI models are uncertain about version specifics.

For reliable code, especially in environments with fixed versions, attention to versioning is crucial. One effective method is to use versioned, package-specific prompts for AI models.

## Preparing Versioned Package-Specific Prompts
 
Here are some situations and strategies for preparing these prompts:

- AI Lacks Knowledge of the Package: Prepare a detailed prompt to educate the AI model.
- AI Has Outdated Version Knowledge: Provide a changelog to inform the AI of changes between versions. Use the lowest overlapping version (e.g., 1.5.3) as the knowledge base to minimize confusion.
- AI Needs an Even More Outdated Version: Though rare, use the highest available version (e.g., 2.0.3) as the base and clearly communicate the need for a downgrade.

We focus on situation 2 as an example. Unfortunately, relying on AI alone to prepare these prompts, even with file processing and web searching capabilities, often results in incomplete information. I tested tools like Perplexity.ai and GitHub Copilot, but the generated prompts frequently lacked critical details. The root cause is the absence of a standardized changelog format for Python package. Therefore, I manually extracted information from the official Pandas documentation and used GPT-4o of openai to create a satisfactory prompt ([changelog_by_openai](./changelog_by_openai.md)).

## Who Should Prepare These Prompts?
 
The responsibility for preparing prompts currently falls on developers, which can be burdensome given the need for prompts across multiple packages, versions, AI models, and model versions. Ideally, service vendors should offer this as an extended service in the medium term. In the long term, package developers should create and document these prompts for AI models.

## Conclusion
A recently published paper [2411.05830 GitChameleon: Unmasking the Version-Switching Capabilities of Code Generation Models](https://arxiv.org/abs/2411.05830) mentioned “Cumulative
year-over-year (YoY) version releases of popular Python-based machine learning libraries show
a consistent upward trend, reflecting the rapid pace of development and version updates of code
libraries and packages.”. So the versions become more and more important in code generation.
 

In the short term, developers need to prepare prompts for critical packages. However, by adopting these strategies, you can enhance the reliability of AI-generated code in your development environment.

## Go further
A related AI suggestion can be found at https://www.perplexity.ai/search/please-list-reliable-informati-NK1XQzjkSOavmjklz0BBpQ.
