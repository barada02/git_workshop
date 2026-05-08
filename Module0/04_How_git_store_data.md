# How Git Stores Data (Snapshots, NOT diffs)

This is the most critical technical concept to grasp. Most beginners assume Git works like a spreadsheet—recording that "on Tuesday, I changed Line 10." If you think this way, Git’s behavior will eventually confuse you.

Git does not think in "lines"; it thinks in **Snapshots**.

![versioning](../assets/versioning.png)

### 📸 The "Photo Album" vs. "The List of Changes"

Most older version control systems (like SVN) use **Delta-based** storage. They store one base file and then a long list of "diffs" (the differences).

* **The Delta Way (Diffs):** To see what your code looks like today, the computer has to start at Version 1 and "apply" every single change ever made in order. It’s like a recipe: "Start with water, add flour, then add salt."
* **The Git Way (Snapshots):** Every time you commit, Git effectively takes a high-resolution photo of **every file** in your project at that exact moment.

---

### 🛠️ How it Works Under the Hood

When you make a commit in Git:

* **If a file has changed:** Git takes a new "photo" of the entire file and stores a compressed version of it.
* **If a file has NOT changed:** Git is smart. It doesn't take a new photo; it simply It just points to the previous version (creates a **link** to the previous version) it already has stored.
* **The Result:** Your project history isn't a list of "edits"—it’s a stream of snapshots.

So internally:

Efficient like diffs
Conceptually like snapshots

### 🔥 Why This "Snapshot" Intuition Matters

1. **Speed:** Because Git has the "full photo" of every version, switching between branches is nearly instantaneous. It doesn't have to calculate math to figure out what a file looked like; it just grabs the snapshot from that date.
2. **Integrity:** Everything in Git is check-summed (using a SHA-1 hash) before it is stored. Because it stores snapshots, if even a single bit of data is corrupted, Git will know immediately because the "photo" won't match the original "fingerprint."
3. **The "Time Machine" Reality:** When you "checkout" an old version, Git isn't undoing lines of code; it is literally replacing your current folder's contents with the contents of that old snapshot.

#### 🎯 Real Meaning of a Commit

👉 A commit is NOT just “saving changes”

👉 A commit =
A full snapshot + metadata (author, message, time)

---

### 💡 The Comparison Table

| Feature | Delta-Based (Older Systems) | Snapshot-Based (Git) |
| --- | --- | --- |
| **Storage Logic** | Stores the *difference* between files. | Stores a *mini-filesystem* of the whole project. |
| **Efficiency** | Saves space, but slow to "rebuild" files. | Extremely fast to switch versions/branches. |
| **Mental Model** | A list of "To-Do" instructions. | A collection of "Save Game" states. |
| **Independence** | Version 5 depends on Versions 1, 2, 3, and 4. | Version 5 is a complete, stand-alone "photo." |

> **Key takeaway for your notes:** Git is basically a tiny, incredibly fast filesystem that sits on top of your project, taking pictures of your progress every time you tell it to "Commit."

### 🧠 Interview Insight

If asked:

👉 “How does Git store data?”

Answer:

Git stores data as snapshots of the project, not just differences
Each commit represents a complete state of the repository
Internally, Git optimizes storage by reusing unchanged files