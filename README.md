# JS DSA Notes

A structured and comprehensive documentation project focused on **JavaScript Data Structures and Algorithms (JS-DSA)**.

This repository contains well-organized notes, examples, explanations, and practice problems—built to help students, interview candidates, and developers strengthen their DSA foundations using JavaScript.

The documentation is generated using **MkDocs Material**, providing a clean, fast, and searchable interface for readers.

---

## 📂 Project Structure

```
js-dsa-notes/
├── docs/
│   ├── index.md
│   ├── Basics/
│   ├── Data-Structures/
│   ├── Algorithms/
│   └── Practice/
├── mkdocs.yml
├── README.md
└── site/ (auto-generated after build)
```

The `docs/` directory contains all DSA notes, grouped into topics for easy navigation:

- **Basics** → Asymptotic notations, variables, functions, loops, methods, OOPs concepts
- **Algorithms** → Sorting, searching, recursion, dynamic programming, greedy algorithms
- **Data-Structures** → Arrays, linked lists, stacks, queues, trees, graphs, hash maps, sets
- **Practice Problems** → Interview questions categorized by difficulty (Easy, Medium, Hard)  

---

## 🚀 Live Documentation (GitHub Pages)

This project is designed to be deployed with **GitHub Pages** using MkDocs.

Once deployed, all content will be available in a beautiful Material documentation site.

**🔗 [View Live Documentation](https://yxshkm404.github.io/javascript-dsa-notes/)**

---

## 🛠 Using MkDocs Locally

To contribute or modify the documentation, install MkDocs and the Material theme:

### 1. Install Dependencies

```bash
pip install mkdocs mkdocs-material
```

### 2. Start the Documentation Server

```bash
mkdocs serve
```

This starts a live-reload dev server at:

```
http://127.0.0.1:8000/
```

### 3. Build the Documentation

```bash
mkdocs build
```

This generates a production-ready `site/` folder.

### 4. Deploy to GitHub Pages

```bash
mkdocs gh-deploy
```

This will build and push the generated site to the `gh-pages` branch automatically.

---

## 📘 MkDocs Navigation (Configured in mkdocs.yml)

This project uses a structured navigation layout to mirror the folder organization:

```yaml
site_name: "JavaScript DSA Notes"
site_url: https://yxshkm404.github.io/javascript-dsa-notes/
repo_url: https://github.com/yxshkm404/javascript-dsa-notes
repo_name: GitHub

theme:
  name: material
  palette:
    - scheme: default
      primary: indigo
      accent: deeporange
      toggle:
        icon: material/weather-night
        name: Switch to dark mode
    - scheme: slate
      primary: indigo
      accent: deeporange
      toggle:
        icon: material/white-balance-sunny
        name: Switch to light mode
  font:
    text: Roboto
    code: Roboto Mono

nav:
  - Home: index.md
  - Basics:
      - Asymptotic Notations: Basics/Asymptotic-Notations.md
      - Functions: Basics/functions.md
      - Loops: Basics/loops.md
      - Methods: Basics/methods.md
      - OOPs: Basics/oops.md
      - Variables: Basics/variables.md
  - Algorithms:
      - Dynamic Programming: Algorithms/dynamic-programming.md
      - Greedy: Algorithms/greedy.md
      - Misc: Algorithms/misc.md
      - Recursion: Algorithms/recursion.md
      - Searching: Algorithms/searching.md
      - Sorting: Algorithms/sorting.md
  - Data Structures:
      - Arrays: Data-Structures/arrays.md
      - Doubly Linked List: Data-Structures/Doubly-linked-list.md
      - Graph: Data-Structures/graph.md
      - Hash Map: Data-Structures/hash-map.md
      - Linked List: Data-Structures/linked-list.md
      - Map: Data-Structures/map.md
      - Object: Data-Structures/object.md
      - Queue: Data-Structures/queue.md
      - Sets: Data-Structures/sets.md
      - Stack: Data-Structures/stack.md
      - Strings: Data-Structures/strings.md
      - Tree: Data-Structures/tree.md
  - Practice Problems:
      - Easy: Practice/easy.md
      - Medium: Practice/medium.md
      - Hard: Practice/hard.md
```

Contributors only need to add new Markdown files under `docs/` and update the navigation when necessary.

---

## 🤝 How to Contribute

We warmly welcome contributions from learners, educators, and developers.

### Steps to Contribute

1. **Fork the repository**

2. **Clone your fork**
   ```bash
   git clone https://github.com/yxshkm404/javascript-dsa-notes.git
   cd javascript-dsa-notes
   ```

3. **Create a new branch**
   ```bash
   git checkout -b feature-new-topic
   ```

4. **Install MkDocs dependencies** (if not already done)
   ```bash
   pip install mkdocs mkdocs-material
   ```

5. **Add or edit Markdown files** under the appropriate folder:
   - `Basics/`
   - `Data-Structures/`
   - `Algorithms/`
   - `Practice/`

6. **Preview changes**
   ```bash
   mkdocs serve
   ```

7. **Update navigation** in `mkdocs.yml` if you add new pages.

8. **Commit and push**
   ```bash
   git add .
   git commit -m "Added new topic: XYZ"
   git push origin feature-new-topic
   ```

9. **Open a Pull Request**

Your contribution will be reviewed and merged if it aligns with the project guidelines.

---

## 🌟 Encourage to Contribute

This project grows stronger with community involvement.

Whether you're documenting a concept, fixing errors, adding examples, or improving the structure, **your contribution matters**.

Every added explanation, code snippet, or diagram helps someone learn DSA more effectively.

### If you find this project valuable, consider:

- Adding missing topics
- Improving explanations
- Adding visual diagrams
- Submitting practice questions or solutions
- Reporting issues or suggesting enhancements

Together, we can build one of the best **community-driven JS DSA learning resources**.

---

## 📜 License

This project is licensed under the MIT License - feel free to use and distribute with attribution.

---

## ⭐ Support

If you find this project helpful, please **star the repository** ⭐

Your support helps the project reach more learners and encourages future improvements.

---

**Happy Learning and Contributing!** 🚀