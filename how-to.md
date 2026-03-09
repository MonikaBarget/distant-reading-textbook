# Working with TeachBooks at Maastricht University Press

*A practical workflow guide*

This guide explains how to set up and collaboratively develop a TeachBooks publication hosted under the **Maastricht University Press (UMPress) GitHub organisation**. The workflow separates the **official publication repository** from **development work**, which helps avoid accidental changes to the published book while enabling collaboration with colleagues and student assistants.

## 1. Request a repository from Maastricht University Press

Ask Maastricht University Press to create a repository under their GitHub organisation.

Requirements:

- The repository should be created under the **MaastrichtUniversityPress GitHub organisation**.
- It should contain the **TeachBooks template** created by TU Delft.
- You should receive at least **maintainer rights** to be able to make the necessary edits.

Example repository:

[https://github.com/MaastrichtUniversityPress/distant-reading-textbook](https://github.com/MaastrichtUniversityPress/distant-reading-textbook)

This repository becomes the **official publication repository**. The book can be automatically published via GitHub Pages.

Example published book:

[https://maastrichtuniversitypress.github.io/distant-reading-textbook/main/intro.html](https://maastrichtuniversitypress.github.io/distant-reading-textbook/main/intro.html)

## 2. Create a GitHub account and accept the invitation

To collaborate on the repository, you need a GitHub account. There are different log-in options. The most common access methods is with a custom password
and two-factor-authentication via an authentication app (such as Microsoft Authenticator).

Steps:

1. Create an account at [https://github.com](https://github.com)
2. Maastricht University Press will send you an **invitation email** to the repository.
3. Accept the invitation.

**Important:**

GitHub invitations typically **expire after seven days**, so make sure to accept them before the link becomes invalid.
Once accepted, you will be able to edit the repository. You can make changes directly via the browser interface, edit files using the Github codespace,
or edit the content locally using an IDE. For beginners, edits directly in the browser are easiest, but they also come with the highest risk of data loss!
You should at least try and use the GitHub codespace for live updates to your content. Local edits pushed to the online repository are safest.

## 3. Create a fork of the repository

Even if you have direct editing rights, it is strongly recommended to create a **fork** of the repository in your own GitHub account.
A fork is a personal copy of the repository which tracks changes you make independently. Other users cannot interfere with your fork unless you expressly invite them,
and changes made to the original repository only become active in your fork if you actively accept them.
On the other hand, having a fork also protects the original repository from accidental deletions and unwarranted changes.

Reasons for working with a fork can include the following:

- You may want to collaborate with **student assistants** on your fork before approving content and pushing it to the actual book repository.
- You may want to experiment with changes after the book has been officially published without making them immediately visible to everyone using your OER.
- You may decide to co-edit certain chapters with colleagues and only wish the final version to become part of the actual OER.

In general, development work carried out in a fork will not immediately affect the **published book**.

Example structure:

**Official repository**

MaastrichtUniversityPress/distant-reading-textbook

**Your personal fork**

YourUsername/distant-reading-textbook

To create a fork:

1. Open the repository on GitHub.
2. Click **Fork** in the top-right corner.

## 4. Recommended workflows

There are two main ways to work on the book.

### Option A: edit the official repository directly

You can edit the UMPress repository directly via:

- GitHub web interface
- GitHub Codespaces
- a local Git installation / IDE

If you maintain a fork, it should be kept **synchronised regularly**, using the following code in the terminal of your
Github Codespace or IDE:

```
git remote add upstream https://github.com/MaastrichtUniversityPress/distant-reading-textbook.git
git fetch upstream
git checkout main
git merge upstream/main
git push origin main
```

This keeps your fork aligned with the official repository, assuming that the official repository is ahead of your fork in terms of updates.

### Option B: work primarily in your fork and push to the official repository

Many authors prefer working mainly in their own fork, especially when they are not the only contributor. When you are making updates
in your fork, you have to make sure to regularly send pull requests to the official repository. Here are the steps to take:

1. Work on content in your fork.
2. Commit your changes to your fork first, ideally describing them in a commit message.
3. When you are working locally, you also need to push the changes to your fork.
4. Then create a **Pull Request (PR)** to the UMPress repository, assuming you are happy with all changes made.

Maintainers of the UMPress repository can then review and merge the changes. If you are a maintainer yourself, you can go to the "Pull Requests" section of the UMPress repository and manually accept the changes there, or you can accept pull requests via the Codespace.
Occasionally you may encounter **merge conflicts**, especially if several people edit the same files (for example `README.md`). These conflicts must be resolved before the pull request can be merged. If resolving conflicts automatically does not work, you can open the problematic file and review the sections highlighted in red manually before committing again.
README files, which contain the main information about the purpose of a repository, are often the most sensitive to merge errors. If you run into issues fixing them, make contact with the UMPress editing team!

## 5. Writing content for TeachBooks using Markdown

TeachBooks uses **Markdown (MD)** as its primary authoring format. Compared to HTML, which is commonly used for static websites but contains rather complex tags,
Markdown is intentionally simple and easy to learn. Moreover, text written in Markdown is still human-readable. For creating a text-based
Open Educational Resource mirroring a traditional teaching handbook, you will most likely need to markdown formatting detailed below:

**Example headings**

```
# Chapter Title
## Section Title
```

**Emphasis**

```
*italic*
**bold**
```

**Lists**

```
- item one
- item two
```

**Code snippets**

`````
```python
print("Hello world")
````

`````

Markdown files in TeachBooks are processed by **Sphinx**, which converts them into the final book website.

TeachBooks also supports:

- call-out boxes
- blockquotes
- figures
- footnotes
- references
- cross-links between chapters

Consult the TeachBooks documentation for advanced formatting.

## 6. Embedding images and videos

### Images

Images can be embedded directly in Markdown:

```
![Caption](images/figure.png)
```

Images sometimes appear **too large** in the rendered book. A common solution is to adjust the display size using CSS.

```
img {
  width: 75%;
}
```

This rule can be added to the project's custom stylesheet.

### Videos

Embedding videos directly in Sphinx/Markdown can be unreliable.

A robust workaround is:

1. Create a screenshot or thumbnail of the video.
2. Link the image to the external video.

```
[![Video preview](images/video-thumbnail.png)](https://video-platform-url)
```

The video itself can be hosted on:

- a university media platform like Media Site.
- YouTube, Vimeo or any other commercial hosting platform.
- PeerTube and other open-source hosting services.

## 7. Embedding executable code

TeachBooks supports executable code through Sphinx extensions.

Typical configurations include:

- MyST-NB
- Jupyter notebooks
- live executable code cells

This functionality must be activated in the Sphinx configuration file.

Example configuration:

```
extensions = [
    "myst_nb",
]
```

This allows the book to include runnable Python examples, data analysis demonstrations, or reproducible workflows.

## 8. Licences for text and code

When creating on Open Educational Resource, it is important to specify licences for both the written content and any accompanying software.
For text content, UMPress recommends the Creative Commons Attribution 4.0 (CC BY 4.0) [https://creativecommons.org/licenses/by/4.0/](https://creativecommons.org/licenses/by/4.0/)
license. 

Example attribution:

Authors: Gustavo Arosemena, Gijs van Dijck, Roland Moerland © Maastricht University Licensed under CC BY 4.0

If code is included, a software license such as **MIT** or **Apache 2.0** is recommended. It is important to select a software
license that allows full reuse of the included code, even when your code is already a derivate of someone else's software.

In a TeachBook issued by UMPress, the license information has to be appear in the repository colophon, which the UMPress team will draft for you.

## 9. Cover image, colophon, and footer

Before publication, the book should include complete chapters, as well as a README and a short repository "About" with a link to the book deployment.
Also, a cover image, a colophon, and a footer following UMPress standards are required.

### Cover image

You can work with the Maastricht University Press editing team to create a cover image. It is important that the cover image
is clear and not too distracting. The cover should also align with the visual identity of UMPress publications.

### Colophon

The colophon is an essential part of the OER metadata and should include:

- authors
- institutional affiliation
- copyright statement
- licence information
- publication details

### Footer

A standardised footer is recommended for all TeachBooks publications. Existing UMPress books can be used as templates.

## 10. Migrating content from other GitHub and Gitlab deployments

When creating your book, you may also want to migrate existing GitHub and Gitlab deployments using Vite, Vue, or Jekyll to the TeachBooks format.
Here, the most important requirement is that all MD files, images and all code files (python, R, etc.) that you want to publish as part of your book are stored in the **book** directory
that the TeachBooks template requires. You do not have to create any specific sub-directories, however, and you also do not need to rename files if they already follow standard conventions (e.g. avoiding special characters and spaces).
All you need to do is about the ```config.yml``` file in **book** and create a new navigation tree for your TeachBook in the ```toc.yml``` file. As part of the ```toc.yml``` file, you can also assign new
display names / titles to your different files / chapters, independent of the underlying file names. This gives you a lot of flexibility in layout and design.
At the same time, conflicting configuration, navigation or CSS styling files from previous deployments should not be migrated to your new TeachBook repository in order to avoid conflicts.
Only migrate the actual content you want to display to your readers later and use the in-built TeachBooks structure for styling.
