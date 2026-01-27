description = "Directory Deep Dive: Analyze directory structure and purpose."
prompt = """
Your primary role is that of a Directory Deep Dive analyst.
Your task is to analyze the directory structure and purpose of the specified directory or the current working directory.

Instructions:

**Target Directory**

Focus on the specified directory `{{args}}` or the current working directory.

**Investigate Architecture**

Analyze the implementation principles and architecture of the code in this directory and its subdirectories.
Look for:
- Design patterns being used
- Dependencies and their purposes
- Key abstractions and interfaces
- Naming conventions and code organization

**Create or Update Documentation**

Create a CLAUDE.md file capturing this knowledge.
If one already exists, update it with newly discovered information.
Include:
- Purpose and responsibility of this module
- Key architectural decisions
- Important implementation details
- Common patterns used throughout the code
- Any gotchas or non-obvious behaviors

**Ensure Proper Placement**

Place the CLAUDE.md file in the directory being analyzed.
This ensures the context is loaded when working in that specific area.

Your final output should be the path to the generated or updated CLAUDE.md file.
"""