# Week 7 Lab: Vim

<br>

## Part 1:
---
## Task - Changing the name of the `start` parameter and its uses to `base` in `DocSearchServer.java`

<br>

### Sequence of key presses in Vim: `/star<Enter>cebase<Esc>n.n.:wq<Enter>` (21 keys total)

<br>1. `/star`

![](lab4_1.png)

Typing `/star` after opening `DocSearchServer.java` in Vim highlights the first instance of the string in the file below the cursor, which starts at the top of the file.

<br>2. `<Enter>`

![](lab4_2.png)

Pressing `<Enter>` positions the cursor on the first character of the highlighted string that `/star` found.

<br>3. `ce`

![](lab4_3.png)

Typing `ce` enters __INSERT__ mode and changes (replaces) the word the cursor was on to the end of the word with nothing, hence why the word _start_ disappears.

<br>4. `base`

![](lab4_4.png)

Typing `base` adds the word to the file where the word _start_ used to be.

<br>5. `<Esc>`

![](lab4_5.png)

Pressing `<Esc>` exits __INSERT__ mode.

<br>6. `n`

![](lab4_6.png)

Pressing `n` finds the next instance of the string _star_ from the `/star` prompt in the file, moving the cursor to the beginning of the instance.

<br>7. `.`

![](lab4_7.png)

Pressing `.` repeats the last command which was `cebase`, replacing the word _start_ with the word _base_.

<br>8. `n.`

![](lab4_8.png)

Repeating steps 6 and 7 by typing `n.` again replaces the next instance of the word _start_ in the file with the word _base_. Since all the instances of _start_ at this point are now _base_, we do not need to type `n.` any more times.

<br>9. `:wq<Enter>`

![](lab4_9.png)

Since we have finished editing the file, typing `:wq<Enter>` saves the file and exits Vim.

<br>

## Part 2: Vim vs. Visual Studio Code
---

<br>

### To edit `DocSearchServer.java` following the task from part 1:
### - In VScode it took: __45 seconds__
### - In Vim it took: __23 seconds__ 


The only difficulty I faced was searching for the instances of the word _start_ manually in VScode in order to replace them with the word _base_.

<br>

If I were working on a project that I had to run remotely, I would prefer to use Vim to create and edit files because it reduces the complexity of the work by keeping everything remote. Rather than transferring files between local and remote, and having multiple instances of the terminal open, I can keep everything on the remote, making the work simpler and less prone to error. However, certain factors regarding a project could lead me to use VScode over Vim even if the project needed to be run remotely. If the project involves many files, the edits that need to be made to the files are really extensive/complex, and/or the project involes many libraries and functions, then VScode would provide me with more easily accessible information that would make working on the project much smoother than in Vim. In such circumstances, I would probably choose VScode over Vim for a project.