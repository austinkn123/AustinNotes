
- **`agents/`**: _Who_ the AI is (Product Manager).
- **`skills/`**: _What_ the AI handles (User Stories).
- **[copilot-instructions.md](vscode-file://vscode-app/c:/Users/Austin/AppData/Local/Programs/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-browser/workbench/workbench.html)**: _How_ the AI should code (Tech stack & Architecture rules).
- **`PULL_REQUEST_TEMPLATE.md`**: how to format the output (Process consistency).

## When to Separate skills and templates (Advanced Cases)

You might separate if:

- **Multiple skills share identical templates** (rare)
- **Very large, complex templates** (100+ lines)
- **Team collaboration** where different people own instructions vs formats
- **Template versioning** is needed independently