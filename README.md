# MyIsland

**Terminal-native AI coding assistant with patch-level control, persistent memory, and Vim integration.**

---

## ✨ Concept

MyIsland is not just a chat interface for LLMs. It is a **patch-driven development environment** where every AI-generated change is:

- visible
- selectable
- editable
- reversible

Instead of blindly applying AI output, you **interact with each change as a first-class object**.

---

## 🧠 Core Idea

```
Prompt → LLM → Structured Patches → Interactive Control → Apply / Refine / Reject
```

You stay in control of:

- what gets changed
- how it gets changed
- when it gets applied

---

## ⚙️ Key Features

### 1. Patch-Centric Workflow

- LLM outputs structured patches, not plain text
- Each change is tracked individually
- Fine-grained control over modifications

### 2. Interactive Terminal UI

View changes directly in the terminal to view changes, navigate patches, and preview diffs.

```
┌──────────────────────────────┐
│ Chat / Prompt                │
├──────────────────────────────┤
│ Patch List                   │
│ [1] app.ts (refactor func)   │
│ [2] utils.ts (rename vars)   │
├──────────────────────────────┤
│ Diff Preview                 │
└──────────────────────────────┘
```

### 3. Vim / Neovim Integration

- Open any patch instantly in Vim/Neovim
- Jump directly to affected lines
- Edit before applying

```bash
nvim +{line} src/file.ts
```

### 4. One-Click Actions

- ✅ Accept patch
- ❌ Reject patch
- ✏️ Refine patch
- 🔍 Open in editor

### 5. Patch Refinement (Core Feature)

Select a specific change and improve it without affecting others:

```
improve patch_1
```

The system:

- isolates the patch
- sends focused context to the LLM
- rewrites only that piece

### 6. Persistent Memory (MemPalace)

Integrated with MemPalace for long-term context:

- stores accepted changes, coding patterns, project structure, useful history
- retrieves relevant context automatically for better results

### 7. Ollama-First Architecture

- runs fully local models via Ollama
- no API keys required
- offline-capable
- supports coding models like qwen3-coder and deepseek-coder

---

## 🏗 Architecture

```
memory (MemPalace) ←→ MyIsland CLI ←→ Ollama (LLM runtime) & File System (codebase)
                          ↓
                  Vim/Neovim integration
```

**Agent Loop:**

user prompt → retrieve memory → read files → build prompt → call Ollama → parse response into patches → render UI → user action (accept/reject/refine/open) → apply changes

---

## 📦 Patch Format (Internal)

Default JSON structure for patches including:

- `id` - patch identifier
- `file` - file path
- `changes` - array with start/end positions and old/new content
- `summary` - patch description
