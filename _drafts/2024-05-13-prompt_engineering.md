---
title: "Write better prompts"
categories: 
- informationsecurity
tags:
- blue team
classes: 
- wide
excerpt: "Writeup based on an free edx course." 
toc: true
--- 

## Introduction
* Prompt: input that produces the desired output
* standard or naive approach
    * unspecific prompt
* Building Blocks of a well-constructed prompt
    * Instructions: give distinct guidelines regarding the task
    * Context: Provides a framework for generating relevant content
    * Input data: any piece of information provided as part of the prompt
    * Output indicator: assesing attributes of the output
* process involved in prompt engineering
    * Define the goal
    * Craft initial prompt
    * Test the prompt
    * Analysze the response
    * Refine the prompt
    * Iterate the process

## best practices for prompt creation
* clarity - simple and concise language
    * use clear and concise language
    * avoid jargon and complex terms
    * provide explicide instructions
* context - background and required details
    * establish the context
    * include relevant informations
* precision - being specific and providing examples
    * be specific
    * include examples
* Role-Play/Persona pattern - response by assuming a persona and offering relevant context
    * assume a persona

## Techniques and approaches
* Interview Pattern Approach
    * designing prompts by simulating a conversation
    * "Act as a salesperson for smartphones and ask me questions about my needs, one after the other. In the end, recommend me a smartphone."
* Chain of Thought Approach
    * breaking down a complex task into smaller ones through a sequence of more straightforward prompts
    * involves training the model with the logic behind the sollution
    * Example: feed the model with the related questions aling with their sollution
    * effective phrases:
        * Let's think step by step
        * Let's work this out in a step by step way to be sure we have the right answer.
* tree of thought approach
    * generating multiple lines of thought, resembling a decision tree
    * Instructions:
        * Imagine three different experts are answering this question. All experts will write down 1 step of their thinking, then share it with the group. Then all experts will go on to the next step, etc. If any expert realises they're wrong at any point then they leave. The question is...[def6]
* Text to Image Prompts Techniques
    * Style modifiers
        * Descriptors used to influce the artistic style or visual attributes of images
            * Color, Size, Contrast, Shape, Texture
            * Art styles
            * historical art periopds
            * photography techniques
            * type of art materials used
            * traits of well knows arts or brands
    * Quality boosters
        * hight resolution, 2k, 4k, hyper-detailed, sharp, focus, complementary colors
        * Examples:
            * Create a human portrait with sharp, crisp details and fine lines.
    * Repetition
        * leverages the power of iterative sampling to enhance image diversity
            * A tiny, tiny, tiny, tiny, tiny, tiny, cozy cabin in the heart of the dense, dense, dense, dense, dense, dense forest.
    * Weighted terms
        * Words or phrases that have a powerful emotional or psychological impact
        * Examples:
            * Craft an image of a cozy living room wirth a warm: 10 | crackling: 8 | fireplace.
            * Generate a vibrant citiyscape with shimmering: 6| neon-lit: 8 | skyscrapers.
            * Depict a bustling street market, with colorful: -6|, exotic: 10| food staals.
    * Fix deformed generation
        * Technique is used to modify deformities or anomalies that my impact the effectivness of the image
        * Examples
            * Mother Teresa with waving hand [disfigured, deformed hands, distorted hands, distorted fingers, bad anatomy, bad hands]

## prompt engineering tools
* provide
    * suggestions for prompts
    * contextual understanding
    * Iterative refinement
    * bias mitigration
    * domain-specific aid
    * libraries of predifined prompts
* examples:
    * IBM watsonsx.ai Prompt Lab
    * Spellbook
    * Dust
    * PromptPerfect

## Examples
* define the persona
    * Act as a computer scientist, what are the top 10 linux commands i should explain in a beginner course, add a short tutorial for each

## source

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
