# Unix File System with B-Trees

A Unix-style file system that supports file and directory operations with metadata storage, using B-Trees as the core index for O(log n) insertion, deletion, and lookup.

## Overview

Traditional directory lookups can degrade to linear scans as directories grow. This project implements a simplified Unix-like file system where files and directories are indexed in a B-Tree, keeping operations fast and balanced regardless of how many entries are stored.

## Features

- **File operations:** create, read, write, delete
- **Directory operations:** mkdir, rmdir, ls, cd, nested paths
- **Metadata storage:** name, size, type, permissions, created/modified timestamps
- **B-Tree index:** balanced storage with O(log n) insert, delete, and lookup
- **Node splitting and merging** to keep the tree balanced as entries are added and removed

<!-- TODO: remove any operations you didn't implement, add any you did (e.g. mv, cp, chmod) -->

## Why B-Trees?

| Operation | Linear list | B-Tree |
|-----------|-------------|--------|
| Lookup    | O(n)        | O(log n) |
| Insert    | O(n)        | O(log n) |
| Delete    | O(n)        | O(log n) |

B-Trees keep many keys per node, which keeps the tree shallow and minimizes the number of node reads per operation. That is the same reason real file systems (NTFS, HFS+, Btrfs) and databases use B-Tree variants for their indexes.

## Architecture

```
            ┌──────────────────────┐
  command → │   Shell / CLI layer  │
            └──────────┬───────────┘
                       ▼
            ┌──────────────────────┐
            │  File system API     │  path resolution, permissions
            └──────────┬───────────┘
                       ▼
            ┌──────────────────────┐
            │  B-Tree index        │  insert / delete / search / split / merge
            └──────────┬───────────┘
                       ▼
            ┌──────────────────────┐
            │  Metadata + storage  │  inodes, file contents
            └──────────────────────┘
```

## Tech Stack

- **Language:** <!-- TODO: e.g. C, C++, Java, Python -->
- **Core data structure:** B-Tree (order <!-- TODO: e.g. t = 3 -->)

## Project Structure

<!-- TODO: adjust to match your repo -->

```
.
├── src/
│   ├── btree.*          # B-Tree implementation
│   ├── filesystem.*     # file and directory operations
│   ├── metadata.*       # inode / metadata handling
│   └── main.*           # CLI entry point
├── tests/
│   └── test_btree.*     # unit tests
└── README.md
```

## Getting Started

```bash
git clone https://github.com/<your-username>/unix-filesystem-btree.git
cd unix-filesystem-btree
# TODO: add your build/run command, e.g.
# make && ./fs
# python main.py
```

## Example Usage

<!-- TODO: replace with real output from your program -->

```
$ mkdir projects
$ cd projects
$ touch notes.txt
$ write notes.txt "hello world"
$ ls -l
-rw-r--r--  11B  2023-05-12 14:02  notes.txt
$ rm notes.txt
```

## What I Learned

- How node splitting and merging keep a B-Tree balanced
- How real file systems separate metadata (inodes) from file contents
- Tradeoffs between tree order, depth, and lookup cost

## Future Work

- Persist the file system to disk between sessions
- Add file permissions enforcement and multiple users
- Benchmark lookup time against a linear directory implementation

## Author

**Sai Manideep Reddy Lakkireddy**
[LinkedIn](https://linkedin.com/in/sai-manideepreddy--/) · saimanideeplakkireddy@gmail.com
