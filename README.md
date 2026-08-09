# SNU-DevOps

DevOps coursework (SNU Chennai, B.Tech CSE-IoT) — a progression of Git/version-control fundamentals through to CI/CD pipelines, containerization, and deployment strategies, plus the standalone lab-exercise repos from the same course merged in as subfolders.

## Lab exercises (`Lab/`)

| Exercise | Topic |
|---|---|
| `Ex01_GithubBasic` | Git & GitHub fundamentals |
| `Ex02_GitLab` | Git on GitLab |
| `Ex03_Bitbucket` | Git on Bitbucket |
| `Ex04_GitAdvanced` | Advanced Git commands |
| `Ex05_Maven` | Introduction to Maven |
| `Ex06_JavaMaven` | Java build automation with Maven |
| `Ex07_JavaMavenManual` | Manual Java/Maven project setup |
| `Ex08_Jenkins` | CI/CD for a web app using Jenkins, Git, and a local HTTP server (`my-web-app/`) |
| `Ex09_Docker` | Jenkins + Docker: containerizing an Apache server (`docker-apache-server/`) |
| `Ex10_JenkinsDocker` | CI/CD for a web app using Jenkins, Git, and Docker containers |
| `Ex11_JenkinsDockerNode` | CI/CD pipeline for a Node.js application using Jenkins and Docker |
| `Ex12_BlueGreenDeployement` | Blue-green deployment strategy for a Node.js application |
| `CIA/CIA.md` | Continuous assessment: Git fundamentals reference |
| `CIA/CIA2.md` | Continuous assessment: end-to-end CI/CD pipeline on AWS (S3) for a Node.js app |
| `QnA/` | Written exercise answers (Maven build lifecycle customization, etc.) |

Each `ExNN` folder has its own `ExN.md` writeup with the exercise steps; `Ex08`-`Ex12` also include the actual project code, `Ex01`-`Ex07` are primarily Git/Maven workflow exercises documented in their `.md`/`.docx` files.

## Merged standalone-repo projects

These were originally separate repositories from the same course, merged here as top-level folders (full original commit history preserved via `git subtree`):

- `DevOpsFinal` — course final project (Dockerfile, Jenkinsfile, docker-compose, health checks)
- `ModelLabDevOps` — Maven/Jenkins model lab
- `aws-cicd-pipeline-app` — Node.js app with AWS CodeBuild / Azure Pipelines CI/CD config
- `blue-green-deployment-app` — Node.js blue-green deployment exercise
- `nodejs-ci-cd-app` — Node.js CI/CD pipeline exercise
- `ci-cd-webapp` — static webapp CI/CD exercise
- `JenkinLabExercise` — Jenkins pipeline exercise

## Running

Most `Lab/ExNN` and merged-project folders are self-contained Node.js apps or static sites:

```bash
cd <folder>
npm install   # if package.json is present
node server.js   # or open index.html directly
```

Docker-based exercises (`Ex09`, `Ex10`-`Ex12`, and most merged projects) include a `Dockerfile`/`compose` file:

```bash
docker compose up --build
```
