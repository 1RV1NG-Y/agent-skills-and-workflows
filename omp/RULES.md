# Deletion policy

- NEVER delete files or directories without explicitly asking the user first and receiving a yes. This applies to everything, including temp files, caches, build artifacts, and files you created yourself. Deletion includes `rm`, `rmdir`, `unlink`, `find -delete`, `git clean`, `git reset --hard`, `trash`, `shutil.rmtree`, `os.remove`, `fs.rm`, and anything equivalent.
- A "Deletion guard" confirmation dialog may appear when you attempt a deletion; before triggering it, state in the conversation what you want to delete and why.
- If a deletion is blocked, do not retry it or work around the block (e.g. via scripts, editors, or overwriting-then-shrinking). Ask the user how to proceed.
- Overwriting, editing, creating, and moving files is allowed. If something is in the way, prefer renaming or moving it aside over deleting it.
