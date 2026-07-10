# Assignment: Prompting Fundamentals on Real Tasks v2 (FL-02)

*   **Target Task from FL-01:** PhD Professor Cold-Outreach Email Structuring.
*   **Objective:** Crafting a highly contextualized, professional email outreach framework that connects my current FlyRank applied ML internship data workflows to a prospective professor's recent academic publications, keeping a zero-slop tone to secure a research interview.

---

## Run 0: The Naive Baseline
*   **The Prompt:** `"Write a cold email to a machine learning professor asking if they have any open PhD spots in their lab."`
*   **The Output Excerpt:** *"Dear Professor [Name], I hope this email finds you well. My name is [Your Name] and I am a highly passionate Master's student. I came across your cutting-edge research and am deeply inspired by your work. Do you have any openings for a PhD student in your lab next semester? I have great skills in Python and ML..."*
*   **Observed Output Difference:** Packed with generic AI filler phrases ("hope this email finds you well", "cutting-edge research") that trigger spam filters and get instantly deleted by busy academics.

---

## Run 1: Applying Technique 1 — Role Assignment
*   **The Prompt:** `"Act as an expert academic consultant and senior research advisor specializing in graduate school placement. Write a cold email to a machine learning professor asking if they have open PhD spots in their lab."`
*   **The Output Excerpt:** *"Dear Professor [Last Name], I am writing to inquire about potential doctoral vacancies within your research group. As an incoming applicant specializing in applied machine learning algorithms, my objective is to explore alignment between your current lab initiatives and my academic background..."*
*   **Note (What changed & why):** Added a professional persona layer. The output tone shifted immediately away from student enthusiasm toward a formal, peer-to-peer academic perspective. However, the text remains too broad because it lacks personal research context.

---

## Run 2: Applying Technique 2 — Context and Motivation
*   **The Prompt:** `"Act as an expert academic consultant specializing in graduate placement. I am a Master's student completing an applied ML internship at FlyRank AI, where I build unsupervised clustering pipelines over multi-million row search intent databases. I am cold-emailing a professor whose lab focuses on high-dimensional text representations. Write an outreach email to inquire about PhD vacancies."`
*   **The Output Excerpt:** *"Dear Professor [Last Name], I am currently wrapping up an ML internship at FlyRank AI, where my focus centers on designing unsupervised clustering pipelines for large-scale text intent data. Given your laboratory's prominent focus on high-dimensional text representations, I am tracking your team's developments and wish to inquire about open doctoral positions..."*
*   **Note (What changed & why):** Injected structural background data and personal motivation. The generated output completely stopped guessing and anchored the value proposition on real-world data competencies. The remaining issue is that the text body lacks clear formatting and visual flow.

---

## Run 3: Applying Technique 3 — Output Structure
*   **The Prompt:** `"Act as an expert academic consultant specializing in graduate placement. [Insert Context from Run 2]. Structure the email into exactly three distinct paragraphs: Paragraph 1 names my current background and explicit reason for outreach. Paragraph 2 references a specific gap or paper connection. Paragraph 3 delivers a single call to action to schedule a 15-minute video call. Do not include standard fluff greetings."`
*   **The Output Excerpt:** 
    *   *Paragraph 1:* I am writing to explore doctoral research alignments... Currently, as an ML intern at FlyRank AI, I engineer unsupervised vector clustering pipelines...
    *   *Paragraph 2:* I am particularly interested in how your lab addresses high-dimensional sparsity...
    *   *Paragraph 3:* If your laboratory has active vacancies, are you available for a brief 15-minute introductory meeting to discuss potential project alignment?
*   **Note (What changed & why):** Mandated a strict 3-paragraph structural architecture. This output change forced the model to be highly concise and stripped away introductory paragraph filler. Paragraph 2 remains conceptually weak because the AI doesn't know how to integrate a real academic paper reference without hallucinating metrics.

---

## Run 4: Applying Technique 4 — Few-Shot Examples (What Good Looks Like)
*   **The Prompt:** `"Act as an expert academic consultant specializing in graduate placement. [Insert Context and Structure from Run 3]. Use this few-shot template example as a guide for paragraph 2's specific execution style: 
    *   *Example Paragraph 2: 'Your recent publication on [Topic X] noted a distinct challenge regarding semantic drift in temporal datasets. My current repository addresses a similar problem by establishing out-of-sample holdout splits to isolate vector variances across an 81.8M row warehouse.'*"
*   **The Output Excerpt:** *"Your recent publication on [Insert Paper Title Here] noted a distinct challenge regarding text representations in sparse data spaces. My current repository addresses a similar problem by engineering semantic text distance measures over an 81.8M row industrial data warehouse to map latent user intent without explicit human labels..."*
*   **Note (What changed & why):** Provided a targeted structural example layout. The output successfully mirrored the technical linkage style, demonstrating how my actual internship data work can serve as a solution to a professor's researched problems.

---

## Run 5: Applying Technique 5 — Step Decomposition
*   **The Prompt:** `"Act as an expert academic consultant specializing in graduate placement. [Insert Context, Structure, and Examples from Run 4]. Before writing the final draft, execute these three steps in order: Step 1: Brainstorm a high-signal, non-spam subject line focused on technical keywords. Step 2: Write the 3-paragraph cold email draft. Step 3: Run an internal critique pass to verify that no banned terms ('passionate', 'hope this finds you well', 'cutting-edge') are present. Print the output of all steps."`
*   **The Output Excerpt:**
    *   *Step 1 (Subject Line):* Ph.D. Inquiry: Unsupervised Semantic Clustering Alignment
    *   *Step 2 & 3 (Final Audited Draft):* [Outputs a highly refined, concise, 3-paragraph outreach document free of buzzwords with embedded placeholder anchors for paper titles].
*   **Note (What changed & why):** Added step decomposition logic. Forcing the model to explicitly evaluate its own draft against a negative vocabulary constraint eliminated residual conversational slop, leaving a clean, hyper-targeted academic message.

---

## 📊 Cross-Model Comparison: Claude vs. ChatGPT

The final prompt configuration from Run 5 was tested on both platforms using the same background context.

| Feature Audit | Claude (Anthropic) | ChatGPT (OpenAI) |
| :--- | :--- | :--- |
| **Tone Check** | Highly defensive, understated, and appropriately formal. Sounds exactly like a junior academic researcher. | Tended to revert to slightly corporate phrasing ("I look forward to collaborating") if not aggressively restricted. |
| **Constraint Adherence** | 100% compliant. Followed the step-by-step decomposition layout and successfully caught and stripped all banned terms. | Skipped explicit step labeling unless pushed, printing the final draft immediately instead of showing the critique pass. |
| **Structural Integrity** | Kept paragraph lengths tightly proportional to the few-shot example. | Tended to lengthen the paragraphs, adding extra adjectives that diluted the technical precision. |
| **Failure Points** | Output can sometimes sound *too* cold or detached if the human input parameters are brief. | Prone to slipping buzzwords back in if the user input text contains them. |

---

##  The Deployed Reusable Template

This optimized, variable-swappable template allows any technical student to frame high-signal cold outreach to academic faculty members:

```text
You are an elite academic advisor specializing in graduate school admissions and scientific research placement. Your task is to draft a highly targeted, zero-slop cold outreach email to a university professor regarding doctoral research positions.

Context Parameters:
- Candidate Current Background: {Your Current Degree Status, e.g., Master's Student in Machine Learning}
- Applied Technical Project/Internship: {Describe your core technical project or internship focus, e.g., Building unsupervised vector clustering pipelines at FlyRank AI}
- Target Dataset Scale: {Scale of data handled, e.g., 81.8-million-row warehouse}
- Target Professor's Focus Area: {The lab's specific research area, e.g., High-dimensional semantic text spaces}
- Target Paper Title: {Name of a recent publication from the professor's lab}
- Primary Action Required: Schedule a brief 15-minute introductory technical video call.

Structural Constraints:
1. Subject Line: Must be descriptive and keyword-driven. Do not use generic clickbait like "Potential Student" or "Urgent Question".
2. Paragraph 1: Direct statement of academic background and explicit purpose of outreach. No fluffy opening pleasantries.
3. Paragraph 2: Direct technical hook connecting your project work to the data challenges or methodologies noted in the Professor's Target Paper Title.
4. Paragraph 3: Direct, low-friction request for a 15-minute technical discussion.

Negative Vocabulary Constraints:
Do not use any of the following terms: "hope this email finds you well", "passionate", "results-driven", "cutting-edge", "revolutionary", "honored", "pleasure". Maintain an objective, plain, and mathematically precise tone.

Execution Protocol:
