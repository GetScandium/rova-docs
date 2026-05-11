# Project Management

In Rova, **Projects** are the primary container for your automation efforts. They allow you to isolate test suites, configurations, and contexts for different parts of your application or different products.

## Projects vs. Workspaces

- **Workspaces**: Top-level entity for your company or team. Manages billing, global members, and shared API keys.
- **Projects**: Exist inside a workspace. A workspace can contain multiple projects (e.g., "Marketing Site", "Mobile App", "Admin Dashboard").

## Organizing Your Projects

### When to Create a New Project
- **Different Tech Stacks**: If you have a separate frontend for your customer portal and your internal admin tool.
- **Microservices**: If you want to isolate tests for different micro-frontends.
- **Client Isolation**: If you are an agency managing multiple clients under one workspace.

## Project Settings

### 1. General Settings
Manage the project name, description, and default starting URL for new tests.

### 2. Context Management
Define the domain knowledge and UI patterns that apply specifically to this project. (See [Project Contexts](contexts.md) for details).

### 3. Manage Upload Assets
Upload assets are files that you provide to Rova that Rova can then make use of whenever it encounters the need to upload a file during a test execution. Consider this a media library.
For example, if a test requires the upload of a profile picture, Rova can look into the media library to select and upload a relevant image file.

> [!TIP]
> Ensure your files are well named so it is easier for Rova to identify which file(s) are relevant to the test at hand.

## Best Practices

### 1. Centralize Common Configurations
If multiple suites share the same environment variables or base URLs, define them at the project level to ensure consistency.

### 2. Use Project Labels
Labels help you categorize tests within a project. For example, use labels like `Experimental`, `Stable`, or `External-Only`.


> [!TIP]
> **Recommendation**: Create a "Sandbox" project for your team to experiment with new AI goals and scripts without affecting your production regression suites.
