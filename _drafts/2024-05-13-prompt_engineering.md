---
title: "Write better prompts"
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

[def]: https://platform.openai.com/examples
[def1]: https://platform.openai.com/docs/guides/prompt-engineering
[def2]: https://learning.edx.org/course/course-v1:IBM+AI0131EN+3T2023
[def3]: https://www.spellbook.legal/
[def4]: https://promptperfect.jina.ai/
