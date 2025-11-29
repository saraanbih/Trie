# Trie Implementation in 8086 Assembly

This repository contains a simple Trie (prefix tree) implementation in 8086 assembly language, compatible with TASM or MASM. It supports basic operations: insert, search, and full delete with node cleanup to reclaim memory. The Trie is designed for uppercase English letters ('A'-'Z') and uses a fixed memory pool for nodes.

## Features
- **Insert**: Adds words to the Trie, creating nodes as needed.
- **Search**: Checks if a word exists in the Trie (returns 1 if found, 0 otherwise).
- **Full Delete**: Deletes a word and removes unused nodes along the path (garbage collection-like cleanup to avoid memory waste).
- **Node Structure**: Each node is 53 bytes:
  - Byte 0: IS_END flag (1 if end of word, 0 otherwise).
  - Bytes 1-52: 26 word pointers (2 bytes each) for 'A' to 'Z'.
- **Limitations**:
  - Supports only uppercase letters.
  - Fixed maximum of 10 nodes.
  - Max word length: 64 characters.
  - No lowercase or special character support (assumes valid input).

## Prerequisites
- Turbo Assembler (TASM) or Microsoft Macro Assembler (MASM).
- DOS emulator like DOSBox (to run the .exe).

## How to Build and Run
1. **Save the Code**: Copy the code into a file named `trie.asm`.
2. **Assemble**:
   ```
   tasm trie.asm
   ```
3. **Link**:
   ```
   tlink trie.obj
   ```
   This generates `trie.exe`.
4. **Run**:
   - Open DOSBox.
   - Mount your folder (e.g., `mount c c:\path\to\folder`).
   - Run `trie.exe`.

## Code Structure
- **Data Segment**: Constants, memory pool (TRIE_MEM), path stack for delete, test words.
- **Procedures**:
  - `CREATE_NODE`: Allocates and zeros a new node.
  - `GET_CHILD`: Retrieves child pointer for a character.
  - `SET_CHILD`: Sets child pointer for a character.
  - `HAS_CHILD`: Checks if a node has any children.
  - `PUSH_PATH` / `POP_PATH`: Manages path stack for delete traversal.
  - `INSERT`: Adds a word.
  - `SEARCH`: Searches for a word.
  - `DELETE_FULL`: Deletes a word and cleans up unused nodes.
- **MAIN**: Demo: Inserts two words, searches, deletes one, searches again.

## License
This project is in the public domain. Feel free to use, modify, or distribute it.
