---
layout: post
title: Styling email message using markdown
category: pgAdmin4
comments: true
---

### What is Markdown ?

Markdown is written in plain text format which is converted into structured HTML using javascript.
Websites like Github, reddit and jekyll are using markdown for their various purposes.
It increases readability for users and now becoming popular popular among writers, developers, scientists and in academics.

**Other applications of Markdown:**

  - Write email message with markdown syntax (Markdown usage in Gmail, follow steps given in article.)
  - Writing documentation for applications.
  - Used to format README files.

### Examples of various Markdown syntax:

## Headings

    # This is an <h1> tag
    ## This is an <h2> tag
    ###### This is an <h6> tag

  **converts to:**

# This is an <h1> tag

## This is an <h2> tag

###### This is an <h6> tag


## Emphasis

  - Bold

        **Text written inside double star is converted to bold**
        __Text written inside double _ is converted to bold__

    **converts to:**


    **Text written inside double star is converted to bold**
    __Text written inside double _ is converted to bold__

  - Italics

        *Text written inside single star is converted to italics*
        __Text written inside single _ is converted to italics*

    **converts to:**

    *Text written inside single star is converted to italics*
    __Text written inside single _ is converted to italics_

## Lists

  - Numbered Lists

        1. I am programmer
        2. I work at EnterpriseDB.
        3. I use markdown for styling gmail content.

    **converts to:**

      1. I am programmer
      2. I work at EnterpriseDB.
      3. I use markdown for styling gmail content.

  - Bullet list
    You can use either - dashes or * star for displaying bullet list

        - I am programmer
        * I work at EnterpriseDB.
        * I use markdown for styling gmail content.
          - Nested list
          * Another nested element

    **converts to:**

  - I am programmer
  * I work at EnterpriseDB.
  * I use markdown for styling gmail content.
    - Nested list
    * Another nested element




## Code and syntax highlighting

### Syntax highlighting using backticks(``).
  For example: I love `Python` and `Javascript`
  Here i put backticks(``) around Python and Javascript and they are highlighted.

### Highlight Code block

Code block highlighting supports number of languages and to highlight them, wrap code around triple backticks.
Below is an example of highlighting Python and Javascript code:

    # to highlight javascript code, type javascript after three backticks
    ```javascript
    var s = "Highlight Javascript code";
    alert(s);
    ```

    # to highlight python code, type python after three backticks
    ```python
    s = "Highlight python code snippets"
    print s
    ```

    # to highlight normal text, just put text between pair of three backticks
    ```
    Normal text which needs not highlighting.
    ```

**converts to:**

```javascript
var s = "Highlight Javascript code";
alert(s);
```

```python
s = "Highlight python code snippets"
print s
```

```
Normal text which needs not highlighting.
```


## Tables

Using (|) pipes, (-) hyphen and (:) colon, a nice looking table can be drawn.
Also, it supports inline markdown syntax inside table such as `bold`, `italics`, `backticks` which makes it more handy to display larger table data in more cleaner way.

    | PL rank       | (%) used      |
    | ------------- |:-------------:|
    | Python        | 80.5%         |
    | *Javascript*  | 90.3%         |
    | `Ruby`        | 60.3%         |

**converts to:**

<img src="../images/table_markdown.png" alt="Table markdown image" style="width: 230px;"/>


## Links
If you want to link an external webpage or blog, using markdown it is quite easy.

    link to [pgAdmin4](http://pgadmin.org) website.

**converts to:**

link to [pgAdmin4](http://pgadmin.org)


## Images

Images can also be displayed with content using markdown syntax. For example to display wikipedia logo, use below format:

    ![Wikipedia Logo](https://de.wikipedia.org/static/images/project-logos/dewiki-2x.png)
    Format: ![Alt Text](url)

**converts to:**

  ![Wikipedia Logo](https://de.wikipedia.org/static/images/project-logos/dewiki-2x.png)

## How to use Markdown syntax to style the email message?

I personally use Chrome extension [Markdown here](http://markdown-here.com/) to serve the purpose. It is quite easy to use.

**Follow below steps to use it:**

 - [Markdown here](http://markdown-here.com/) is available as browser extension for `Google Chrome`, `Firefox`, `Opera` etc.
 - Once you install, an icon will display at top right corner of browser.
 - Compose an email, type few lines using markdown syntax, for example:

        Hello,

        ### An email with example message:
        - _Ruby_ is most used programming language.
        - Python is `scripting` language.
        - **Javascript** is `weak typed`, `dyanamic`, `high level` language.

 - Copy paste above content in your email.
 - Right click inside email and then click `Markdown Toggle`, or click on Markdown icon in the toolbar or
 press `CTRL+ALT+M` shortcut key.

**Woohaa! Now message will be looks like:**

Hello,

### An email with example message:

  - _Ruby_ is most used programming language.
  - Python is `scripting` language.
  - **Javascript** is `weak typed`, `dyanamic`, `high level` language.

Enjoy :)

---
