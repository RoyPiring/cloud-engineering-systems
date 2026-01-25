<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Build an AI Security Scanner with Gemini

**Project Link:** [View Project](http://learn.nextwork.org/projects/ai-security-audit)

**Author:** Roy Piring Jr  
**Email:** rpiringhawaii@gmail.com

---

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-security-audit_sec4e5f6)

---

## Introducing Today's Project!

This project implements a command-line security scanner that uses Google Gemini to analyze Python code for security vulnerabilities. The scanner evaluates code, identifies potential risks, and assigns severity ratings using color-coded output.

The objective is to explore how AI models can augment traditional static analysis by identifying common security issues through contextual reasoning. The project combines Python automation, AI integration, and security analysis into a single, practical tool.

### Key tools and concepts

The tools used in this project are Python, the Google Gemini API, and the Colorama library.

Python provides the scripting and automation foundation. The Gemini API is used to perform AI-driven security analysis based on structured prompts. Colorama enhances terminal output by visually distinguishing vulnerability severity levels.

Key concepts explored include AI-assisted security analysis, prompt engineering for structured outputs, automated code scanning, and severity classification. A core skill exercised in this project is adapting prompts and interpreting AI responses to produce actionable security insights.

### Challenges and wins

This project took approximately 90 minutes to complete. The primary challenge was refining the security prompts to consistently produce accurate, detailed, and relevant vulnerability assessments from the Gemini model.

The most successful outcome was validating that the scanner could identify realistic security issues such as SQL injection risks, hardcoded credentials, and unsafe coding practices. This confirmed that AI can be effectively applied to augment security reviews when guided with well-structured prompts.

### Why I did this project

I completed this project to explore how AI can enhance software security analysis beyond traditional pattern-based tools. The goal was to gain hands-on experience integrating an AI model into a security workflow while improving Python automation skills.

This project also served as a foundation for future expansion, including integrating the scanner into CI/CD pipelines to perform automated security checks during development.

---

## Connecting to Gemini API

This step establishes connectivity to the Google Gemini API. A structured project environment is created, and credentials are configured to allow secure interaction with the API.

This setup is required so the scanner can submit code to Gemini for analysis and receive structured responses identifying potential vulnerabilities. Proper configuration ensures reliable access and a clean development workflow.

Tasks to Complete:

- Create a dedicated project directory and configure the Python environment

- Install required libraries and dependencies

- Configure and validate access to the Gemini API

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-security-audit_sec2c3d4)

The connection was verified by executing a test command that listed available Gemini models. Receiving a valid response confirmed that the API key was correctly configured and that the environment could successfully communicate with Gemini.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-security-audit_sec4e5f6)

The scanner.py script accepts Python code as input, constructs a security-focused prompt, and submits it to the Gemini model. The response is then parsed to identify potential vulnerabilities.

When executed, the scanner identified issues such as SQL injection risks, hardcoded credentials, and insecure library usage. This demonstrates that the Gemini API can be leveraged to analyze code contextually and surface meaningful security concerns.

---

## Building the Vulnerability Scanner

In this step, the vulnerability scanner logic is implemented. The scanner is designed to analyze Python code and report potential security issues in a structured format.

The implementation supports:

- Testing against intentionally vulnerable code samples

- Crafting a detailed security prompt that guides Gemini’s analysis

- Detecting common vulnerability categories such as SQL injection, hardcoded secrets, and weak authentication practices

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-security-audit_sec7h8i9)

The Gemini model identified vulnerabilities including SQL injection risks, exposed API keys, and unsafe file handling. The security prompt was designed to request a comprehensive analysis covering issues such as cross-site scripting, insecure session handling, and improper input validation.

This structured approach enables consistent output, easier evaluation of scanner accuracy, and iterative improvement through prompt refinement.

---

## Adding Severity Ratings

This step enhances the scanner by adding severity classification to identified vulnerabilities. Severity ratings help prioritize remediation efforts by indicating relative risk.

Key enhancements include:

- Installing the Colorama library to enable colored terminal output

- Updating the Gemini prompt to request severity levels for each finding

- Implementing a mapping function to associate severity levels with specific colors

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-security-audit_sec0k1l2)

The security prompt was updated to request severity classifications of Critical, High, Medium, Low, and Informational. This ensures consistent categorization across findings.

The add_colors_to_output function maps severity levels to colors using Colorama. Critical findings appear in red, High in yellow, Medium in orange, Low in blue, and Informational in green.

A Critical severity indicates an issue that could lead to significant system compromise or data exposure and should be addressed immediately. This visual prioritization improves usability and operational decision-making.

---

## Scanning Real Python Files

This step extends the scanner to analyze entire Python files instead of isolated code snippets. Real-world security reviews require scanning full files and codebases.

The scanner reads the contents of a specified file, submits the code to Gemini for analysis, and outputs categorized vulnerabilities with severity indicators.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-security-audit_sec3n4o5)

The vulnerable.py file was scanned using the command python scanner.py vulnerable.py. The scanner detected SQL injection risks, hardcoded API keys, and insecure file handling logic.

The scan_file function reads the file contents, sends them to Gemini via the security prompt, and processes the AI response to extract and display categorized findings with color-coded severity ratings.

---

## Wrap-up

---

---
