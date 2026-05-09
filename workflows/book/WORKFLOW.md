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
- The script MUST use `generate_content_stream` (streaming) for all text generation calls to the Gemini API. Only structured JSON schema calls (outline generation) may use non-streaming `generate_content`.
- You must structure the Python script based on the blueprint found in `bestseller-novel-architect/examples/python/automated_gemini_generator.py`.
- The script must include structured Pydantic outputs for Character and Outline generation, and a loop to generate a Prologue and chapters sequentially based on the outline.
- **CRITICAL**: The script MUST include an **Auto-Retry Logic** (in case of empty or blocked API responses) and a **Chapter/Prologue Caching** mechanism (to save intermediate chapters to text files and prevent data loss).
- The script must compile the final output to a `.docx` file using `python-docx`, ensuring a Table of Contents (สารบัญ) and Prologue are included before Chapter 1.

### 3. Execution & Verification
- Instruct the user to ensure they have their `GEMINI_API_KEY` set in their environment variables.
- Install all required dependencies first:
  `python -m pip install google-genai pydantic python-docx fastapi uvicorn`
- **Start the Pixel Dashboard** to provide a real-time log viewer UI:
  `python pixel_dashboard/pixel_dashboard_poc.py`
- The dashboard runs at `http://127.0.0.1:8000`. Open the browser and instruct the user to click the **[ 📖 สร้างหนังสือ 5 บท ]** button to start the pipeline.
- The dashboard will run `generate_novel.py` as a subprocess and stream all output (including Gemini API streaming chunks) to the browser in real-time via WebSocket.
- *Wait for user approval before running the command.*
- Once the pipeline completes, the dashboard will display "เขียนหนังสือเสร็จสิ้น!" and the compiled `.docx` file will be available in the project root.
