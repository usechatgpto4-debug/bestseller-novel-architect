---
name: bestseller-novel-architect
description: Master framework for crafting Bestseller and Nobel-level novels. Use this skill when prompted to write a novel directly, generate a python script for novel generation, or build a web app for novel creation.
---

# Bestseller & Nobel Novel Architect (Agent Protocol)

This skill provides a systematic framework for crafting high-quality novels based on the techniques of Bestseller and Nobel-prize-winning authors. 

**AGENT BEHAVIOR MANDATE**: When invoked, you must STRICTLY adhere to the 7 Pillars of this framework. Do not output generic stories. Every plot, character, and chapter must be deliberately designed using these principles.

## 1. The Core Framework (The 7 Pillars)
*(Agent must refer to these pillars in every generation task)*

### Pillar 1: Structure (Three-Act Structure)
- **Act I: Setup (25%)**: Introduce the protagonist, the ordinary world, and the **Inciting Incident** that breaks the status quo.
- **Act II: Confrontation (50%)**: Escalate obstacles (Rising Action), introduce sub-mysteries, include a **Midpoint** (paradigm shift), and end with an **All is Lost** moment.
- **Act III: Resolution (25%)**: The final Climax and Denouement.
- *Constraint*: Before writing, confirm if the user is a "Plotter" (requires detailed outline first) or "Pantser" (starts with a situation and explores).

### Pillar 2: Point of View (POV)
Force the user to select one:
- **1st Person**: For intimate, emotional, or psychological depth.
- **3rd Person Limited**: For suspense and focused narrative.
- **3rd Person Omniscient**: For sweeping, complex themes.
- **Alternating POVs**: For fast-paced thrillers or mysteries.

### Pillar 3: Character Characteristics
- **MANDATORY**: Every main character MUST have:
  1. A clear external goal.
  2. A psychological flaw or trauma (Internal Conflict).
  3. Relatable, specific ordinary details.
- Use the **Iceberg Theory**: Show their actions and dialogue, but imply the deeper emotional weight beneath the surface.

### Pillar 4: Pacing (Beginning, Middle, End)
- **Beginning**: Must hook the reader immediately.
- **Middle**: Must NOT sag. Inject sub-mysteries or mini-goals for every chapter.
- **End**: High stakes climax that resolves the character's internal flaw and external goal.

### Pillar 5: Character Arc
Must map to one of these:
- **Positive Arc**: Overcomes the "Lie they believe" to find the "Truth".
- **Negative Arc**: Succumbs to their flaw/fear.
- **Complex Arc**: Accepts a painful past, finding peace rather than a traditional happy ending.

### Pillar 6: Chapter Structure
Every chapter must have:
- **Title (MANDATORY)**: A unique and evocative Chapter Title (ชื่อบท).
- **Opening**: Start *in medias res* or connect to the previous cliffhanger.
- **Body**: A micro-conflict. The character must attempt a goal, face an obstacle, and make a decision.
- **Ending**: NEVER tie all loose ends. Must end on a Hook.

### Pillar 7: Chapter Hooks & Cliffhangers
Rotate between these hook types at the end of chapters:
- **Action**: Life-threatening danger.
- **Revelation**: New game-changing information.
- **Question**: A mystery introduced.
- **Emotional**: A heavy emotional realization or decision.
- **Shift/Cutaway**: Sudden cut to another POV.
- **Promise**: A hint of what will happen next.

### Pillar 8: Show, Don't Tell & Sensory Details
- **MANDATORY**: Focus on the 5 senses (sight, sound, smell, touch, taste). 
- Do NOT summarize emotions (e.g., "He was sad"). Instead, describe the physical and physiological reactions (e.g., "His chest tightened, and his vision blurred").
- Use strong, active verbs.

### Pillar 9: Core Components (Prologue & Table of Contents)
- **MANDATORY**: Every novel MUST contain a **Prologue (บทนำ)** that hooks the reader with an inciting incident, action, or deep mystery BEFORE Chapter 1.
- **MANDATORY**: Every novel MUST contain a **Table of Contents (สารบัญ)** right after the Title Page and before the Prologue.

### Formatting Rules
- **No Western Punctuation**: Do NOT use exclamation marks (`!`) or question marks (`?`) in the novel text. Use Thai phrasing and context to convey tone, excitement, or questions.

---

## 2. Actionable Workflows (Execution Protocols)

### Workflow A: Direct Novel Generation (Automated via Python)
*Use this when the user asks you to write a story or novel directly.*
**Step 1: Ideation**: Ask the user for Genre, Premise, and Number of Chapters.
**Step 2: Script Generation**: 
- Create `generate_novel.py` using the new `automated_gemini_generator.py` blueprint.
- Ensure the script uses the `google-genai` library and `gemini-3.1-pro-preview` model.
**Step 3: Execution**: 
- Prompt the user to set `GEMINI_API_KEY`.
- Propose running `python -m pip install google-genai pydantic python-docx; python -u generate_novel.py > generation_log.txt 2>&1`.
- Wait for user approval, then execute.
- Direct the user to monitor `generation_log.txt` for real-time progress. The script will automatically output the formatted `.docx` file.

### Workflow B: Python Script Generation (Automation)
*Use this when the user asks for a Python script/tool to generate novels.*
**Architecture Rules**:
- **Frameworks**: Use `langchain` or raw LLM APIs (OpenAI/Anthropic/Gemini).
- **Structure**: Implement a State Machine or sequential pipeline (`generate_characters() -> generate_outline() -> generate_prologue() -> generate_chapters()`).
- **Persistent Story Bible**: You MUST inject the serialized `NovelOutline` JSON into the prompt for EVERY chapter and scene generation to ensure long-term plot consistency.
- **Multi-Scene Generation**: Instead of generating a full chapter in one call, first generate a `ChapterOutline` with 3-4 scenes, then loop through and generate each scene individually.
- **Auto-Critique Editor Loop**: After generating any scene or prologue, pass it to an "AI Editor" prompt to enforce formatting rules (no western punctuation) and "Show, Don't Tell". If it fails, the AI must rewrite it.
- **Core Components**: You MUST generate a Prologue and include a Table of Contents (สารบัญ) in the final output.
- **Prompts**: You MUST inject the 9 Pillars directly into the system prompts within the Python code. (e.g., `SYSTEM_PROMPT = "You are a bestseller author. Every chapter must end with one of these 6 hooks..."`)
- **Data Models**: Use `pydantic` to enforce structured JSON outputs for Character Sheets, Outlines, Chapter Outlines, and Scene Outlines.
- **Robustness**: The pipeline MUST implement **Auto-Retry Logic** (for handling empty responses/safety blocks) and **Chapter/Prologue Caching** (saving intermediate texts so progress isn't lost on crash).
- **Output Format**: The pipeline MUST include a final export step to generate a fully formatted `.docx` file.
- **Reference Blueprint**: ALWAYS refer to `examples/python/novel_generator_skeleton.py` (in this skill's directory) for the structural blueprint of the generator and the `export_to_docx` method.

### Workflow C: Web App Development
*Use this when the user asks to build a web platform for novel writing.*
**Design & UI Rules**:
- **Aesthetics**: Premium, modern, dark-mode ready, glassmorphism UI. It must feel like a professional author's tool.
- **Feature Modules**: 
  1. *Dashboard/Project Setup* (Genre, POV selection).
  2. *Character Studio* (UI to define Flaws, Goals, Arcs).
  3. *Plot Board* (Kanban or timeline UI for the Three-Act Structure).
  4. *Writing Editor* (AI-assisted editor that validates chapter hooks).
  5. *Export Engine* (Feature to compile and download the final novel as a formatted `.docx` file).
**Tech Stack Rules**: 
- Use Next.js (App Router), Tailwind CSS, and a database (Prisma/Supabase) to store the structured data.
- **AI Integration**: The API routes that call the LLM MUST use strict system prompts based on the 7 Pillars.
