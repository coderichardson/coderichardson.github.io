---
title: "Writing Technical Documentation"
date: 2022-06-04 17:09:00 +0000
tags:
  - "Documentation"
---

Often in infosec we get caught up on CVEs, the latest breach, or ransomware. Unfortunately, the other half of the job (project management, documentation, etc) can sometimes get less attention. Admittedly, they don't make movies about completing the paperwork after most action films. But in the real world it's what can lose court cases or certify a company as compliant with a government regulation.

We all wish documentation was clearer when reading it but very few enjoy writing it. I'm going to paint a broad brush here and put them all into two categories:

1. Formal technical documentation

- E.g. SOC reports, company policies, SIG assessments, etc.

2. Informal technical documentation

- E,g, the internal (or even customer facing) documentation explaining a concept or how to complete a technical task such as updating the OS version on a firewall.

I'm not a Technical Writer, but I don't find writing documentation as painful as some, and I appreciate coming across what I find to be well-written documents. Here are my thoughts on writing good documentation.

### Formal Technical Documentation

Some quick tips if you're writing formal documentation (some of these are personal preference, some are fairly standard):

- Justify text.
- Use page numbers.
- Use a header with a company logo when appropriate.
- Include a title page and table of contents.
- Use italics to introduce new terms.
- Spell out any acronyms upon introduction with the acronym following in parenthesis if used again later in the text.
- Be mindful of the type of document you're writing and include relevant content. For example, policies should be general in nature and procedures should include specific steps. Besides, if you have to change the steps in your procedure at any point at least you only have to update one piece of documentation!

I actually like the [NSA's Cybersecurity Advisories & Guidance docs](https://www.nsa.gov/Press-Room/Cybersecurity-Advisories-Guidance/) as an example ([here](https://media.defense.gov/2022/Mar/01/2002947139/-1/-1/0/CTR_NSA_NETWORK_INFRASTRUCTURE_SECURITY_GUIDANCE_20220301.PDF) is their 2022 Network Infrastructure Guidance), though they contain some low-level steps that would be more fitting under my definition of "information technical documentation."

### Informal Technical Documentation

First, there's nothing wrong with taking all the advice from the *Formal Technical Documentation* section and applying it to less formal documents. But my focus here will be more on getting across technical concepts to the reader.

One of my favorite things to do is get familiar with style guides. Read through a few from prominent companies and get a feel for how they write their informal documentation. This is a good starting place and these style guides are something I often revisit. While I don't agree with everything in theirs, Microsoft [has a great one](https://docs.microsoft.com/en-us/style-guide/procedures-instructions/formatting-text-in-instructions) that introduces a variety of ideas for writing. A couple other examples of good documentation but that have different "flows" are [GitHub's API documentation](https://docs.github.com/en/rest/guides/getting-started-with-the-rest-api) and [AWS's documentation](https://docs.aws.amazon.com/AWSEC2/latest/WindowsGuide/concepts.html).

There are no rules you have to follow, so pick a style that you like best and stick with it throughout the document (and establish it up front or in an appendix to the document if it differs from the norm). This **establishes consistency** in your writing. The most frequent example I see of this is in writing commands or instructing a user to perform an action. For example:

**Example 1**

1. Open command prompt.
2. Type appwiz.cpl and press enter.
3. Choose an application to uninstall.
4. Select uninstall.

**Example 2**

1. Open Command Prompt.
2. Type **appwiz.cpl** and press **Enter**.
3. In Control Panel choose an application to uninstall.
4. Select **Uninstall**.

**Example 3**

1. Open Command Prompt.
2. Type appwiz.cpl and press **Enter**.
3. In Control Panel choose an application to uninstall.
4. Select **Uninstall**.

These are three different ways of writing the same set of instructions. Example 3 provides, in my opinion, the clearest steps to follow. It capitalizes the names of applications, uses a monospace font for commands the user should input, and emphasizes other required actions using bold font.

Some other practices that help in a similar fashion:

- If the text in a command is a placeholder it should be italicized or placed in angle brackets:

- robocopy *source destination*
- robocopy <source> <destination>

- Optional parts of a command should be placed in square brackets:

- robocopy *source* *destination* [/e]

Also, in informal documentation screenshots are great, but they should be used only when there may be confusion about a particular step. There is no need to take a screenshot of every single prompt, etc. Not to mention the problem with updating documentation with new screenshots when the UI of the application changes.

Diagrams, flow charts, and other visual illustrations of a concept are also great additions to technical documentation. Sometimes even with the best practices followed, a wall of text instructions will never be clearer than a visual illustration.

### Final Thoughts

You can probably go through the rest of my blog and find that I haven't followed my own rules at times. But I hope what I have followed makes it easier on those in the future that read what I write.

I didn't touch on topics like making writing accessible (things like adding descriptions to screenshots or captions to videos) or styles of writing ([passive vs active voice](https://owl.purdue.edu/owl/general_writing/academic_writing/active_and_passive_voice/active_versus_passive_voice.html)) among other things. All important topics and I encourage reading more about them.

I will take a moment here to advocate for the Oxford comma and to mention that double-spaces after a period are not necessary in any formal writing (even APA took it out of the requirements a few years ago) but shouldn't get as much hate as they do in informal writing.

Let me know if you have examples of great documentation, or maybe a practice you follow when writing documents that I haven't touched on here.