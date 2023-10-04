# How GitHub builds GitHub with GitHub

## General info

- Date: 24 May 2023
- Event: [[2.records.events.microsoft-build-2023.md]]
- Speakers:
    - Brian Randell, GitHub
    - Martin Woodward, GitHub
- URL: https://build.microsoft.com/en-US/sessions/e3492a33-2601-4378-9ee8-a78d40b32df6

## Summary

Presentation of the internal GitHub development process and some new GitHub features.

Facts:

- GitHub is a Ruby on Rails application
- Monolithic architecture
- Hosted in a single repository on GitHub: [github/github](https://github.com/github/github) (private)
- Size of the repository is 16 GB
- 1.4 million commits
- 1.5k engineers working on the code base
- 80k deployments to production per year

The GitHub features listed below have been presented.

### Codespaces

[Codespaces](https://github.com/features/codespaces) is essentially a compute instance in the cloud (Azure) on which the code of a repository gets downloaded and checked out.

In the case of GitHub, the entire GitHub repository can be ready to use in less than one minute (versus 45 minutes for cloning it to a local machine).

The code in Codespaces can be accessed transparently from Visual Studio Code, or it's also possible to SSH into the Codespaces instance.

When checking out the GitHub code, it's possible to run a local dev version of GitHub.

### Copilot

[GitHub Copilot](https://github.com/features/copilot) is a conversational AI tool (similar to ChatGPT) that runs directly in the code editor (e.g. Visual Studio Code or Neovim) and can assist with writing code.

The following languages seem to be [fully supported by GitHub Copilot](https://docs.github.com/en/enterprise-cloud@latest/get-started/learning-about-github/github-language-support):

- C							
- C++							
- C#				
- Go				
- Java				
- JavaScript				
- PHP				
- Python		
- Ruby				
- Scala				
- TypeScript

Some features of other languages may be supported as well.

> Note: a [GitHub Copilot for the CLI](https://githubnext.com/projects/copilot-cli/) is currently in development too. This Copilot will assist in writing shell commands.

### Projects

[GitHub Projects](https://docs.github.com/en/issues/planning-and-tracking-with-projects/learning-about-projects/about-projects) in 2022 and now includes more facilities for visualising data and managing issues of multiple repositories. For example, it's possible to hierarchically nest issues in order to bettter organise them.

### GitHub Actions

Demonstration of how the GitHub repository internally uses [GitHub Actions](https://github.com/features/actions) to automate the builds and other things.

### Push protection

[Push protection](https://docs.github.com/en/enterprise-cloud@latest/code-security/secret-scanning/protecting-pushes-with-secret-scanning) is a new feature that scans pushes for secrets in the code that is being pushed, and prevents the push if it finds any secrets. The goal is to prevent the accidential pushing of secrets to a GitHub repository.

Secrets of more than 100 services are recognised natively, and it's possible to define custom regexes for detecting custom secrets.

### CodeQL

[CodeQL](https://codeql.github.com/) is a new feature that allows running queries on repositories for detecting specific vulnerabilities. For example, if there is a new vulnerability, a query that detects this vulnerability can be defined (in CodeQL syntax), and this query can then be run on any repository to detect the vulnerability.

### Telemetry

Demonstration of how telemetry data of GitHub is analysed in [Azure Data Explorer](https://azure.microsoft.com/en-us/products/data-explorer). Data in Azure Data Explorer can be queried with the [Kusto Query Language (KQL)](https://learn.microsoft.com/en-us/azure/data-explorer/kusto/query/). For example, it's possible to instantly count the number of repositories on GitHub with a simple KQL query.

## Discussion

All in all a very good presentation. Especially the introductions of Codespaces and GitHub Copilot were valuable.
