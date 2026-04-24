---
name: book
description: Direct command workflow to generate a novel using the Bestseller Novel Architect framework.
---

# Book Generation Workflow

**Trigger**: This workflow is activated when the user issues a direct command to create a book or novel (e.g., calling the "book" workflow).

## Mandatory Prerequisite
You MUST immediately utilize the `bestseller-novel-architect` skill. All output must strictly adhere to the 7 Pillars defined in that skill.

## Execution Steps

Follow these steps sequentially. Do not skip ahead.

### 1. Ideation Phase
- Greet the user and confirm that the Automated Book Generation Workflow has started.
- Ask the user for the **Genre**, **Premise**, and the **Number of Chapters** they want to write.
- *Wait for user input.*

### 2. Script Generation
- Once the user provides the requirements, generate a Python script named `generate_novel.py` in the root of the project.
- The script MUST use the `google-genai` library and the **gemini-3.1-pro-preview** model.
- You must structure the Python script based on the blueprint found in `bestseller-novel-architect/examples/python/automated_gemini_generator.py`.
- The script must include structured Pydantic outputs for Character and Outline generation, and a loop to generate a Prologue and chapters sequentially based on the outline.
- **CRITICAL**: The script MUST include an **Auto-Retry Logic** (in case of empty or blocked API responses) and a **Chapter/Prologue Caching** mechanism (to save intermediate chapters to text files and prevent data loss).
- The script must compile the final output to a `.docx` file using `python-docx`, ensuring a Table of Contents (สารบัญ) and Prologue are included before Chapter 1.

### 3. Execution & Verification
- Instruct the user to ensure they have their `GEMINI_API_KEY` set in their environment variables.
- Propose running the following command to install dependencies and execute the script. Use `python -m pip` for better Windows compatibility, and run the script with `-u` unbuffered mode directing to a log file:
  `python -m pip install google-genai pydantic python-docx; python -u generate_novel.py > generation_log.txt 2>&1`
- *Wait for user approval before running the command.*
- Inform the user that they can monitor the progress in real-time by viewing `generation_log.txt`.
- Once completed, provide the user with the path to the compiled `.docx` file.
