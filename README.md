# Martin Hunt

**`Scientific and Embedded Software Developer`**

🔭 I'm currently working on **Writing software for Signal Processing and Hearing Research**.  I'm hoping to get approval to make much of it open source in the near future.

---

## 🏫 What I'm Learning


### 🤖 AI Coding Tools

This is an exciting time for software development. Over the last few years I've shifted my workflow as the models and tools have improved. At this point I'm writing >90% of my code with AI, across unit tests, documentation, and full modules. I've read hundreds of articles, watched dozens of videos, and put these tools through several real projects. Here's what I've learned.

My progression: GitHub Copilot as smarter autocomplete -> prompt engineering for tests and docs -> Claude Code. Switching to Claude Code enabled memory (CLAUDE.md / AGENTS.md), skills, hooks, plugins — what the community now calls the "user harness." Tuning that environment is the difference between AI-generated code that I'd ship and AI-generated code that I wouldn't.

### What works

**Brownfield with a real test suite.** An existing codebase is an executable specification. The model can read the structure, infer the style, follow established patterns, and — critically — *run the tests* to verify its work. The feedback loop is tight: change -> test -> diff. That's the loop that produces shippable code.

**Tests are the most important part of the spec.** Prose specs are ambiguous, decay over time, and can't be verified. Tests are unambiguous and runnable. When I add a feature, the model writes failing tests first, then implements until they pass. When I fix a bug, step one is a test that reproduces it. The model doesn't need to "understand the spec" — it needs a goal it can verify by running code.

**Greenfield is brownfield with a bootstrap step.** Use plan mode to sketch the project, generate an initial skeleton *with tests*, then operate as brownfield from there. The spec-writing phase is short and disposable — once code exists, the code is the spec.

**Invest in the harness.** Code quality tracks harness quality. Once the harness can run tests, format, and lint on its own, the model can verify its own work between turns, and the surface area you have to babysit collapses.

### What doesn't

The industry is rapidly reinventing software engineering, and much of it is hype. Solid engineering is getting drowned out by PR-driven stories about startups burning a million dollars in tokens to ship a side project.

**Vibe Coding** works for throwaway prototypes — note-taking apps with cute names and nice landing pages. Don't ship anything you'd need to maintain.

**Spec-Driven Development** is more thoughtful but structurally broken. You write a detailed spec; the model generates code from it. The spec is never perfect, so you iterate. But each regeneration throws away the understanding you'd built about the previous version, the code is something neither you nor the model owns, and there's no clean exit to hand-editing. You're locked in the loop, burning tokens.

The deeper problem is that prose is the wrong feedback medium. Tests run; specs don't. Without an executable target, every "iteration" is just rephrasing.

### Harness engineering notes

- **It's a hierarchy.** Global CLAUDE.md and skills apply to every project, so keep them minimal — preferences, not project specifics. Project-level files add the build/test commands, conventions, and domain knowledge that change per repo. Directory-level files handle subsystem quirks. Each layer extends the one above it.

- **What goes in CLAUDE.md.** Build/test/lint commands the model should run before declaring done; conventions you keep restating ("we use X over Y, here's why"); a domain glossary for non-obvious terms; paths to design docs or schemas worth reading first; explicit "never do Z" rules from past mistakes. Keep it terse — every line costs context on every turn.  You can break the file up into multiple files and import them using the "@" syntax to keep things organized, but the context cost remains.

- **Skills vs hooks.** Skills are model-invoked capabilities the agent decides to use ("review this PR", "run security scan"). Hooks are deterministic shell scripts the harness fires on events (post-edit format, pre-commit lint). Different mechanisms: skills handle judgment calls, hooks handle invariants. Don't make the model "remember to format" — that's a hook.

- **Allowlist your read-only commands.** Auto-permitting common reads — `git status`, `ls`, `grep`, your test runner — is one of the biggest friction reducers. The model stops asking permission for things you'd never deny, and the loop tightens dramatically.

- **The feedback loop is the point.** 
  - Same mistake twice -> CLAUDE.md. If you correct "use X not Y" once, fine. If you correct it again next session, the lesson didn't persist — because you are the memory, not the harness. Write it down once and the model gets it free forever.

  - Ten minutes of back-and-forth -> skill. Long thrash usually means you're hand-walking the model through a procedure: "first check the logs, then run this, then look for that pattern...". That procedure is a skill. Encode it once, invoke it with one phrase next time.

  - Every correction is a signal. The general form. Before you type the correction, ask: why was this needed? Missing context? -> CLAUDE.md. Missing capability? -> skill or hook. Missing permission? -> allowlist. The correction itself is the symptom; the harness gap is the cause.

- **Plan mode for anything non-trivial.** Let the model think before it writes. Plan mode separates "design the change" from "make the change" and catches misunderstandings before they hit code. For one-line fixes it's overhead; for anything multi-file it's the cheapest insurance you can buy.


## 📸 Project Screenshot Gallery

Unfortunately, many of the projects I have worked on are proprietary and cannot be shared publicly. Much of my code was written for embedded devices most of the rest for desktops. The ones with GUIs were written so the realtime code running on the embedded device (or desktop) is controlled by IPC and a small embedded web server. I have included screenshots of some of the applications I have developed in the last few years to provide a visual representation of my work. These screenshots showcase the user interfaces and features of the applications, giving insight into the types of projects I have been involved in. Please note that while the screenshots provide a glimpse into my work, they do not fully capture the complexity and functionality of the applications I have developed. If you are interested in learning more about my work or have specific questions about the projects, please feel free to reach out to me directly. I am happy to discuss my experience and the technologies I have used in more detail.


### Featured Projects

<table>
<tr>
<td width="60%">

**🎯 SpeechFit - Audiology Research Platform**

An application for conducting hearing research studies and managing participant sessions. Features include real-time data visualization, researcher dashboards, session management, and advanced acoustic analysis tools.

*Tech Stack: C++, Python, FastAPI, Vue.js, PostgreSQL, NiceGUI*

</td>
<td width="40%">
<img src="screenshots/speechfit_landing.png" alt="SpeechFit Landing" width="100%"/>
</td>
</tr>
</table>

<details>
<summary><b>📷 View More SpeechFit Screenshots</b></summary>
<br/>
<table>
<tr>
<td width="50%"><img src="screenshots/speechfit_sessions.png" alt="SpeechFit Sessions" width="100%"/><br/><sub><i>Session Management Interface</i></sub></td>
<td width="50%"><img src="screenshots/speechfit_resdearcher.png" alt="SpeechFit Researcher" width="100%"/><br/><sub><i>Researcher Dashboard</i></sub></td>
</tr>
<tr>
<td width="50%"><img src="screenshots/speechfit_ho2_results.png" alt="SpeechFit Results" width="100%"/><br/><sub><i>HO2 Test Results Visualization</i></sub></td>
<td width="50%"><img src="screenshots/speechfit.png" alt="SpeechFit Main" width="100%"/><br/><sub><i>Testing View</i></sub></td>
</tr>
</table>
</details>

---

<table>
<tr>
<td width="60%">

**🧪 LTest - Hearing Testing Suite**

A hearing assessment tool providing comprehensive audiological testing capabilities. Includes automated test protocols, real-time threshold tracking, and detailed result reporting for clinical and research applications.

*Tech Stack: C++, Python, NumPy, SciPy, Nuitka*

</td>
<td width="40%">
<img src="screenshots/ltest_1.png" alt="LTest Interface 1" width="100%"/>
<sub><i>Audiologist View</i></sub></td>
</tr>
</table>

<details>
<summary><b>📷 View More LTest Screenshots</b></summary>
<br/>
<table>
<tr>
<td align="center"><img src="screenshots/ltest_2.png" alt="LTest Interface 2" width="80%"/><br/><sub><i>Users View</i></sub></td>
</tr>
<tr>
<td align="center" width="33%">
<img src="screenshots/quicksin.png" alt="QuickSIN" width="100%" style="border: 1px solid #ddd; border-radius: 4px;"/>
<br/><br/>
<b>🗣️ QuickSIN</b><br/>
<sub>Quick Speech-in-Noise assessment tool for evaluating hearing performance in noisy environments. Clinical-grade testing application.</sub>
</td>
</tr>
</table>
</details>

---

### Additional Tools & Applications

<table>
<tr>
<td align="center" width="33%">
<img src="screenshots/wdrctool.png" alt="WDRC Tool" width="100%" style="border: 1px solid #ddd; border-radius: 4px;"/>
<br/><br/>
<b>🔊 WDRC Tool</b><br/>
<sub>Wide Dynamic Range Compression configuration Test and Verification tool for hearing aid algorithms. Allows comparison of different implementations.</sub>
</td>
<td align="center" width="33%">
<img src="screenshots/pcdtool.png" alt="PCD Tool" width="100%" style="border: 1px solid #ddd; border-radius: 4px;"/>
<br/><br/>
<b>📊 PCDTool</b><br/>
<sub>CLI tool to connect to our embedded devices by USB or Bluetooth.</sub>
</td>
<td align="center" width="33%">
<img src="screenshots/cfscope.png" alt="CF Scope" width="100%" style="border: 1px solid #ddd; border-radius: 4px;"/>
<br/><br/>
<b>🎚️ CFScope</b><br/>
<sub>Allows detailed measurement and comparison of processed audio signals. Useful for evaluating audio processing algorithms and hearing aid performance.</sub>
</td>
</tr>
<tr>
<td align="center" width="33%">
<img src="screenshots/lscope.png" alt="L Scope" width="100%" style="border: 1px solid #ddd; border-radius: 4px;"/>
<br/><br/>
<b>📡 LScope</b><br/>
<sub>Similar to CFScope, LScope provides detailed measurement and comparison of processed audio signals, focusing on different aspects of audio analysis.</sub>
</td>
<td align="center" width="33%">
<img src="screenshots/mushra.png" alt="MUSHRA" width="100%" style="border: 1px solid #ddd; border-radius: 4px;"/>
<br/><br/>
<b>🎵 MUSHRA</b><br/>
<sub>Multi-Stimulus test with Hidden Reference and Anchor implementation. Standard tool for subjective audio quality assessment in hearing research.</sub>
</td>
<td align="center" width="33%">
<img src="screenshots/BenchTest.png" alt="Bench Test" width="100%" style="border: 1px solid #ddd; border-radius: 4px;"/>
<br/><br/>
<b>⚡ BenchTest</b><br/>
<sub>Measures the SNR and THD of an audio signal when processed by different algorithms.</sub>
</td>
<tr>
<td align="center" width="33%">
<img src="screenshots/freping.png" alt="FrePing" width="100%" style="border: 1px solid #ddd; border-radius: 4px;"/>
<br/><br/>
<b>🎼 Freping</b><br/>
<sub>Frequency Warping tool. Demonstrates the effects of frequency warping on audio signals.</sub>
</td>
<td align="center" width="33%">
</td>
</tr>
</table>


### Connect with me:
<p>
I don't really do social media, but you can find me on LinkedIn if you'd like to connect or learn more about my work experience and projects.
<a href="https://www.linkedin.com/in/martin-hunt-4a4688187/" target="blank"><img align="center" src="images/linkedin.svg" alt="  https://www.linkedin.com/in/martin-hunt-4a4688187/" height="30" width="40" /></a>
</p>

### Languages and Tools:
<p>

<a href="https://aws.amazon.com" target="_blank" rel="noreferrer"> <img src="images/aws.svg" alt="aws" width="40" height="40"/></a>
<a href="https://en.wikipedia.org/wiki/Bash_(Unix_shell)" target="_blank" rel="noreferrer"> <img src="images/bash.svg" alt="bash" width="40" height="40"/> </a>
<a href="https://en.wikipedia.org/wiki/C_(programming_language)" target="_blank" rel="noreferrer"> <img src="images/c.svg" alt="c" width="40" height="40"/> </a>
<a href="https://en.wikipedia.org/wiki/C%2B%2B" target="_blank" rel="noreferrer"> <img src="images/cpp.svg" alt="cplusplus" width="40" height="40"/> </a> 
<a href="https://docs.anthropic.com/en/docs/claude-code/overview" target="_blank" rel="noreferrer"> <img src="images/claude.svg" alt="claude code" width="40" height="40"/> </a>
<a href="https://www.djangoproject.com/" target="_blank" rel="noreferrer"> <img src="images/django.svg" alt="django" width="40" height="40"/> </a>
<a href="https://www.docker.com/" target="_blank" rel="noreferrer"> <img src="images/docker.svg" alt="docker" width="40" height="40"/> </a>
<a href="https://www.electronjs.org/" target="_blank" rel="noreferrer"> <img src="images/electron.svg" alt="electron" width="40" height="40"/> </a>
<a href="https://fastapi.tiangolo.com/" target="_blank" rel="noreferrer"> <img src="images/fastapi.svg" alt="fastapi" width="40" height="40"/> </a>
<a href="https://git-scm.com/" target="_blank" rel="noreferrer"> <img src="images/git.svg" alt="git" width="40" height="40"/> </a>
<a href="https://github.com/" target="_blank" rel="noreferrer"> <img src="images/github-skill.svg" alt="github" width="40" height="40"/> </a>
<a href="https://developer.mozilla.org/en-US/docs/Web/html" target="_blank" rel="noreferrer"> <img src="images/html.svg" alt="html5" width="40" height="40"/> </a>
<a href="https://developer.mozilla.org/en-US/docs/Web/javascript" target="_blank" rel="noreferrer"> <img src="images/javascript.svg" alt="javascript" width="40" height="40"/> </a>
<a href="https://www.jenkins.io/" target="_blank" rel="noreferrer"> <img src="images/jenkins.svg" alt="jenkins" width="40" height="40"/> </a>
<a href="https://www.linux.org/" target="_blank" rel="noreferrer"> <img src="images/linux.svg" alt="linux" width="40" height="40"/> </a>
<a href="https://www.mathworks.com/products/matlab.html" target="_blank" rel="noreferrer"> <img src="images/matlab.svg" alt="matlab" width="40" height="40"/> </a>
<a href="https://matplotlib.org/" target="_blank" rel="noreferrer"> <img src="images/matplotlib.svg" alt="matplotlib" width="40" height="40"/> </a>
<a href="https://mesonbuild.com/" target="_blank" rel="noreferrer"> <img src="images/meson.svg" alt="meson" width="40" height="40"/> </a>
<a href="https://www.nginx.com/" target="_blank" rel="noreferrer"> <img src="images/nginx.svg" alt="nginx" width="40" height="40"/> </a>
<a href="https://nicegui.io/" target="_blank" rel="noreferrer"> <img src="images/nicegui.png" alt="nicegui" width="40" height="40"/> </a>
<a href="https://numpy.org/" target="_blank" rel="noreferrer"> <img src="images/numpy.svg" alt="numpy" width="40" height="40"/> </a>
<a href="https://www.postgresql.org/" target="_blank" rel="noreferrer"> <img src="images/postgresql.svg" alt="postgresql" width="40" height="40"/> </a>
<a href="https://playwright.dev/" target="_blank" rel="noreferrer"> <img src="images/playwright.svg" alt="playwright" width="40" height="40"/> </a>
<a href="https://www.python.org/" target="_blank" rel="noreferrer"> <img src="images/python.svg" alt="python" width="40" height="40"/> </a>
<a href="https://www.qt.io/" target="_blank" rel="noreferrer"> <img src="images/qt.svg" alt="qt" width="40" height="40"/> </a>
<a href="https://scipy.org/" target="_blank" rel="noreferrer"> <img src="images/scipy.svg" alt="scipy" width="40" height="40"/> </a>
<a href="https://seaborn.pydata.org/" target="_blank" rel="noreferrer"> <img src="images/seaborn.svg" alt="seaborn" width="40" height="40"/> </a>
<a href="https://www.sqlite.org/" target="_blank" rel="noreferrer"> <img src="images/sqlite.svg" alt="sqlite" width="40" height="40"/> </a>
<a href="https://tailwindcss.com/" target="_blank" rel="noreferrer"> <img src="images/tailwind.svg" alt="tailwind" width="40" height="40"/> </a>
<a href="https://code.visualstudio.com/" target="_blank" rel="noreferrer"> <img src="images/vscode.svg" alt="vscode" width="40" height="40"/> </a>
<a href="https://vuejs.org/" target="_blank" rel="noreferrer"> <img src="images/vuejs.svg" alt="vuejs" width="40" height="40"/> </a></p>

