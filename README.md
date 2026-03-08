
# 📌 Project Overview

In this project, we will:

* Learn **Git and GitHub basics**
* Manage code using **branches and commits**
* Collaborate using **Pull Requests**
* Create a **CI/CD pipeline using GitHub Actions**
* Deploy a **static website to AWS S3**
* Configure **IAM roles and permissions**

---

# 🧰 Technologies Used

* Git
* GitHub
* GitHub Actions
* AWS S3
* AWS IAM
* HTML / CSS / JavaScript

---

# 📂 Project Structure

```
portfolio-website/
│
├── index.html
├── style.css
├── script.js
│
└── .github/
    └── workflows/
        └── deploy.yml
```

---

# 1️⃣ Introduction to Version Control

**Version Control** helps track and manage changes in source code.

### Benefits

* Track history of changes
* Collaborate with team members
* Restore previous versions
* Manage different features using branches

### Git

Git is a **distributed version control system** used to manage source code.

Key concepts:

* Repository
* Commit
* Branch
* Merge
* Pull Request

---

# 2️⃣ Setting Up Git and GitHub

## Install Git

Download Git from:

[https://git-scm.com/](https://git-scm.com/)

Verify installation:

```bash
git --version
```

---

## Configure Git

```bash
git config --global user.name "Your Name"
git config --global user.email "your@email.com"
```

---

## Create a Repository on GitHub

1. Go to GitHub
2. Click **New Repository**
3. Name it **portfolio-website**
4. Click **Create**

---

## Clone Repository

```bash
git clone https://github.com/username/portfolio-website.git
```

---

# 3️⃣ Working with Git: Commits, Branches, and Merges

### Add files

```bash
git add .
```

### Commit changes

```bash
git commit -m "Added portfolio website"
```

### Push to GitHub

```bash
git push origin main
```

---

## Create Branch

```bash
git checkout -b feature-homepage
```

---

## Merge Branch

```bash
git checkout main
git merge feature-homepage
```

---

# 4️⃣ Collaborative Workflows with GitHub

Teams collaborate using **branches and pull requests**.

Typical workflow:

```
Developer → Feature Branch → Pull Request → Code Review → Merge
```

Steps:

1. Create feature branch
2. Make changes
3. Push branch
4. Open Pull Request
5. Team reviews code
6. Merge to main

---

# 5️⃣ Managing Pull Requests and Code Reviews

Pull Requests help teams review code before merging.

Benefits:

* Improve code quality
* Identify bugs early
* Share knowledge

Reviewers can:

* Comment on code
* Suggest changes
* Approve merge

---

# 6️⃣ Automating Workflows with GitHub Actions

GitHub Actions allows **CI/CD automation**.

In this project we automate:

1. Code push
2. Build website
3. Deploy to AWS S3

---

# ☁️ AWS Setup

## Step 1: Create S3 Bucket

1. Go to AWS Console
2. Open **S3**
3. Click **Create Bucket**
4. Bucket name must be unique

Example:

```
sonu-portfolio-website
```

Enable:

* Static Website Hosting

Upload test file:

```
index.html
```

---

## Step 2: Enable Static Website Hosting

Inside S3 bucket:

```
Properties → Static Website Hosting → Enable
```

Set:

```
Index document: index.html
```

---

## Step 3: Bucket Policy

Allow public access for website.

Example policy:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicRead",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::sonu-portfolio-website/*"
    }
  ]
}
```

---

# 🔐 IAM Setup

Create IAM user for GitHub Actions.

Steps:

1. Go to **IAM**
2. Create **User**
3. Enable **Programmatic Access**

Attach policy:

```
AmazonS3FullAccess
```

(For production use limited permissions)

---

## Get Credentials

You will get:

```
AWS_ACCESS_KEY_ID
AWS_SECRET_ACCESS_KEY
```

---

# 🔑 Add Secrets in GitHub

Go to:

```
GitHub Repository → Settings → Secrets → Actions
```

Add:

```
AWS_ACCESS_KEY_ID
AWS_SECRET_ACCESS_KEY
AWS_REGION
S3_BUCKET_NAME
```

Example:

```
AWS_REGION = ap-south-1
S3_BUCKET_NAME = sonu-portfolio-website
```

---

# ⚙️ GitHub Actions Workflow

Create file:

```
.github/workflows/deploy.yml
```

---

## deploy.yml

```yaml
name: Deploy Portfolio to S3

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:

      - name: Checkout Code
        uses: actions/checkout@v3

      - name: Configure AWS Credentials
        uses: aws-actions/configure-aws-credentials@v2
        with:
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          aws-region: ${{ secrets.AWS_REGION }}

      - name: Deploy to S3
        run: |
          aws s3 sync . s3://${{ secrets.S3_BUCKET_NAME }} --delete
```

---

# 🚀 Deployment Process

1️⃣ Push code to GitHub

```
git add .
git commit -m "portfolio website"
git push origin main
```

2️⃣ GitHub Actions triggers automatically.

3️⃣ Workflow uploads files to **AWS S3**.

4️⃣ Website becomes live.

Example URL:

```
http://sonu-portfolio-website.s3-website-ap-south-1.amazonaws.com
```

---

# 7️⃣ Hands-on Practice

Tasks for learners:

* Create GitHub repository
* Build simple HTML portfolio
* Configure AWS S3
* Create GitHub Actions workflow
* Deploy website automatically

---

# 8️⃣ Conclusion

In this project we learned:

✔ Version Control using Git
✔ GitHub collaboration workflow
✔ CI/CD pipeline using GitHub Actions
✔ AWS S3 static website hosting
✔ IAM security configuration

This workflow is widely used in **DevOps and Cloud deployments**.

---

# 📚 Learning Resources

Git Documentation

[https://git-scm.com/docs](https://git-scm.com/docs)

GitHub Actions

[https://docs.github.com/en/actions](https://docs.github.com/en/actions)

AWS S3 Documentation

[https://docs.aws.amazon.com/s3](https://docs.aws.amazon.com/s3)

