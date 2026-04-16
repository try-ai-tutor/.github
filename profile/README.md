# try-ai-tutor

AI-tutored auto-grading pipeline for programming assignments.
Try it yourself — no setup required.

## How it works

1. **Accept** an assignment link below
2. **Clone** the repo GitHub Classroom creates for you
3. **Write** your solution and push
4. The CI pipeline runs **pytest inside a Docker container** to grade your code
5. An **AI tutor** reads the test results and generates personalized feedback
6. Check the Actions tab for your score and tutor comments

## Try it

| Assignment | Type | Link |
|------------|------|------|
| 020 - Area | Code | [Accept assignment](https://classroom.github.com/a/S7hWRc_v) |
| 020p - Area (prompt) | Prompt-only | [Accept assignment](https://classroom.github.com/a/6tkc2Nk-) |

### Code assignment

Write `exercise.py` to solve the problem. Push your code, and the grader runs
your solution against the test suite. The AI tutor explains what went wrong
(or right).

### Prompt-only assignment

Write `prompt.md` instead of code. The CI workflow sends your prompt to an LLM,
which generates `exercise.py` on your behalf. The same pytest suite grades the
generated code. The challenge: communicate your intent clearly enough that the
LLM produces a correct solution.

## If accepting the assignment fails with a 500 error

GitHub Classroom sometimes returns a 500 error when you accept an assignment.
The repo gets created, but you are not added as a collaborator — so you cannot
see or push to it.

You cannot fix this yourself (no access = no way to request access through
GitHub). Contact the instructor out-of-band (email or course channel) with
your GitHub username and the assignment name. The only known fix is for the
instructor to add you manually as a collaborator.

## What's behind the curtain

```
push → GitHub Actions → Docker container
         ├── pytest (syntax + style + results)
         ├── AI tutor (reads failures, writes feedback)
         └── score reported via Autograding Reporter
```

- **Grader images** are pre-built and pulled from `ghcr.io`
- **Reusable workflows** live in `workflows-central`
- Each assignment has its own test suite — you cannot see the tests beforehand

## About this project

This pipeline handles **20+ assignments x 150+ students** per semester at a
university in South Korea. Data collected since 2023 shows that AI tutoring
lowered the frustration barrier for beginners: median iterations per assignment
rose from 1 to 4 (students kept trying instead of giving up), and the despair
tail (p90 iterations) collapsed from 37 to 18.

The prompt-only variant is an experiment in teaching prompt engineering as a
graded skill — same grader, new input modality.

Built and managed with [Claude Code](https://claude.ai/code),
[Gemini](https://gemini.google.com), and [Grok](https://grok.com).
