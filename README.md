# software_engineering

sequenceDiagram
    participant Developer
    participant GitHubRepo
    participant GitHubActions
    participant TestServer
    participant DeploymentServer

    Developer->>GitHubRepo: git push origin main
    GitHubRepo->>GitHubActions: Trigger workflow (on: push)
    
    GitHubActions->>GitHubActions: Checkout code
    GitHubActions->>TestServer: Run tests (unit/integration)
    TestServer-->>GitHubActions: Test results (pass/fail)

    alt Test passed
        GitHubActions->>DeploymentServer: Deploy application
        DeploymentServer-->>GitHubActions: Deployment success
    else Test failed
        GitHubActions-->>Developer: Notify failure
    end

    GitHubActions-->>Developer: CI/CD result notification
