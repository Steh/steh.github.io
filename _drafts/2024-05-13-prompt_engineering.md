---
title: "Write Better Prompts"
categories: 
  - informationsecurity
tags:
  - blue team
classes: 
  - wide
excerpt: "" 
toc: true
--- 

## Introduction
* Prompt: input that produces the desired output
* Standard or naive approach
  * Unspecific prompt
* Building Blocks of a well-constructed prompt
  * Instructions: give distinct guidelines regarding the task
  * Context: Provides a framework for generating relevant content
  * Input data: any piece of information provided as part of the prompt
  * Output indicator: assessing attributes of the output
* Process involved in prompt engineering
  * Define the goal
  * Craft initial prompt
  * Test the prompt
  * Analyze the response
  * Refine the prompt
  * Iterate the process

## Best practices for prompt creation
* Clarity - simple and concise language
  * Use clear and concise language
  * Avoid jargon and complex terms
  * Provide explicit instructions
* Context - background and required details
  * Establish the context
  * Include relevant information
* Precision - being specific and providing examples
  * Be specific
  * Include examples
* Role-Play/Persona pattern - response by assuming a persona and offering relevant context
  * Assume a persona

## Techniques and approaches
* Interview Pattern Approach
  * Designing prompts by simulating a conversation
  * "Act as a salesperson for smartphones and ask me questions about my needs, one after the other. In the end, recommend me a smartphone."
* Chain of Thought Approach
  * Breaking down a complex task into smaller ones through a sequence of more straightforward prompts
  * Involves training the model with the logic behind the solution
  * Example: feed the model with the related questions along with their solutions
  * Effective phrases:
    * Let's think step by step
    * Let's work this out in a step-by-step way to be sure we have the right answer.
* Tree of Thought Approach
  * Generating multiple lines of thought, resembling a decision tree
  * Instructions:
    * Imagine three different experts are answering this question. All experts will write down 1 step of their thinking, then share it with the group. Then all experts will go on to the next step, etc. If any expert realizes they're wrong at any point then they leave. The question is...

## Text to Image Prompts Techniques
* Style modifiers
  * Descriptors used to influence the artistic style or visual attributes of images
    * Color, Size, Contrast, Shape, Texture
    * Art styles
    * Historical art periods
    * Photography techniques
    * Type of art materials used
    * Traits of well-known artists or brands
* Quality boosters
  * High resolution, 2k, 4k, hyper-detailed, sharp, focus, complementary colors
  * Examples:
    * Create a human portrait with sharp, crisp details and fine lines.
* Repetition
  * Leverages the power of iterative sampling to enhance image diversity
    * A tiny, tiny, tiny, tiny, tiny, tiny, cozy cabin in the heart of the dense, dense, dense, dense, dense, dense forest.
* Weighted terms
  * Words or phrases that have a powerful emotional or psychological impact
  * Examples:
    * Craft an image of a cozy living room with a warm: 10 | crackling: 8 | fireplace.
    * Generate a vibrant cityscape with shimmering: 6 | neon-lit: 8 | skyscrapers.
    * Depict a bustling street market, with colorful: -6 | exotic: 10 | food stalls.
* Fix deformed generation
  * Technique used to modify deformities or anomalies that may impact the effectiveness of the image
  * Examples:
    * Mother Teresa with waving hand [disfigured, deformed hands, distorted hands, distorted fingers, bad anatomy, bad hands]

## Prompt engineering tools
* Provide
  * Suggestions for prompts
  * Contextual understanding
  * Iterative refinement
  * Bias mitigation
  * Domain-specific aid
  * Libraries of predefined prompts
* Examples:
  * IBM watsonsx.ai Prompt Lab
  * Spellbook
  * Dust
  * PromptPerfect

## Examples
* Define the persona
  * Act as a computer scientist, what are the top 10 Linux commands I should explain in a beginner course, add a short tutorial for each

## Source

* [openai.com: Prompt examples][def]
* [openai.com: guide prompt-engineering][def1]
* [edx: Introduction to Prompt Engineering][def2]
* [Using Tree-of-Thought Prompting to boost ChatGPT's reasoning][def5]

[def]: https://platform.openai.com/examples
[def1]: https://platform.openai.com/docs/guides/prompt-engineering
[def2]: https://learning.edx.org/course/course-v1:IBM+AI0131EN+3T2023
[def3]: https://www.spellbook.legal/
[def4]: https://promptperfect.jina.ai/
[def5]: https://github.com/dave1010/tree-of-thought-prompting/tree/main
[def6]: https://github.com/dave1010/tree-of-thought-prompting/blob/main/tree-of-thought-prompts.txt