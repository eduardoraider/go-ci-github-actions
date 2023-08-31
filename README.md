# Continuous Integration for a Go Application using GitHub Actions

This repository demonstrates how to set up Continuous Integration (CI) for a Go application using GitHub Actions. The main focus of this README is to guide you through the process of automating tests and creating a CI pipeline using GitHub Actions.

## Prerequisites

Before you begin, ensure the following prerequisites are met:

1. **Go**: Install Go by following the instructions provided on the [official website](https://golang.org/doc/install).
2. **Docker**: Install Docker by following the instructions for your operating system from the [official Docker documentation](https://docs.docker.com/get-docker/).
3. **GitHub Account**: Sign up for a GitHub account if you don't have one.

## Continuous Integration with GitHub Actions

Follow these steps to set up automated tests and a CI pipeline for your Go application using GitHub Actions:

### 1. Clone the Repository

```bash
git https://github.com/eduardoraider/go-ci-github-actions.git
cd go-ci-github-actions
```

### 2. Run the tests locally

```bash
docker-compose up -d
go test -v main_test.go
```

### 3. Create `.github/workflows` Directory

Create a `.github/workflows` directory in the root of your repository.

### 4. Configure GitHub Actions Workflow

Create a YAML file (e.g., `go.yml`) within the `.github/workflows` directory to define your CI workflow. Below is an example:

```yaml
name: Go

on:
  push:
    branches: [ "main" ]
  pull_request:
    branches: [ "main" ]

jobs:

  test:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v3

    - name: Set up Go
      uses: actions/setup-go@v4
      with:
        go-version: '1.20'

    - name: Build DB
      run: docker-compose build

    - name: Create DB
      run: docker-compose up -d

    - name: Test
      run: go test -v main_test.go

  build:
    needs: test
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v3

    - name: Build
      run: go build -v main.go
```

### 5. Push to GitHub

Commit and push your changes to GitHub. This will trigger the GitHub Actions workflow.

### 6. Monitor Workflow

Go to the "Actions" tab in your GitHub repository to monitor the status of the workflow. It should automatically run tests for your Go application.


## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE.txt) file for details.

---

#### by Eduardo O Raider
🛠 🥋 **Software Engineer**