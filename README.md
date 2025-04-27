# 🧠 Memory Tracker

This file provides a simple **garbage collection**-like mechanism for C projects.  
It tracks all allocated memory dynamically and ensures everything is properly freed at the end or in case of an error.

---

## 📂 File: `memory_tracker.c`

### 🛠️ Functions

- `void ft_free(t_gb **head)`
  - 🧹 Frees all tracked memory and clears the tracking list.

- `t_gb *ft_new_addr(void *add)`
  - ➕ Creates a new tracking node for a given memory address.

- `t_gb *ft_last_addr(t_gb *head)`
  - 🔚 Returns the last node in the tracking list.

- `void ft_add_new(t_gb **head, t_gb *new)`
  - 📌 Adds a new node to the end of the tracking list.

- `void *ft_malloc(ssize_t len)`
  - ⚙️ Custom malloc function:
    - 📦 Allocates memory.
    - 📋 Tracks the allocation in a linked list.
    - 🧹 If `len < 0`, it frees all previously allocated memory.
    - ❌ If allocation fails, frees all memory and exits the program.

---

## 🧪 Usage

Instead of using `malloc` directly, use `ft_malloc(size)`:
```c
char *str = ft_malloc(20 * sizeof(char));
```

When needed (typically at the end of execution or on error), you can **free all allocated memory** by calling:
```c
ft_malloc(-1);
```
or by directly calling:
```c
ft_free(&head);
```
*(where `head` is the static pointer inside `ft_malloc`.)*

---

## ✅ Advantages

- **Safe memory management**: No leaks if used properly.
- **Centralized free**: Clean up everything at once.
- **Error Handling**: If memory allocation fails, it frees everything and exits.

---

## 📌 Notes

- This system **only tracks memory allocated through `ft_malloc`**.
- It does not handle partial frees — everything is freed at once.
- Make sure you don't manually `free(ptr)` individually — let the tracker manage it.

---

## 👨‍💻 Author

- **By**: [iezzam@student.42.fr](https://profile.intra.42.fr/users/iezzam)
- **Created**: 2025/04/27

