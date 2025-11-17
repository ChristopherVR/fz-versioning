---
title: Changelog
order: 1.1
parent: 'index.md'
---

# Changelog

All notable changes to the "fuzor-ai-transformer" extension will be documented in this file.
## [0.4.1] - 2025-11-17

### Fixed

- **MCP Workspace Folder Creation**: Reduced unnecessary creation of the `.fuzor/mcp` folder in workspaces when MCP servers are not being installed at the workspace scope.
- **MCP Installation Scope**: Updated the installation modal to default to global scope, improving the user experience when adding new MCP servers.
- **MCP STDIO Transport Support**: Added support for MCP servers using STDIO transport with custom executables beyond npx and Python packages.
- **MCP Server Uninstallation**: Resolved an issue where uninstalling an MCP server did not properly remove the server from selected agents and FuzorAgent configurations.
- **MCP Server Selection**: Fixed an issue preventing users from deselecting MCP servers in the MCP popup when the server is not currently running.
- **MCP Server Tool Execution**: Resolved an issue where MCP servers were incorrectly skipped during tool calling, preventing their tools from being properly invoked by AI agents.

## [0.4.0] - 2025-11-13

> See the Removed section for breaking changes that may affect you.

### Added

- **Model Context Protocol (MCP) Support**: Fuzor now implements full support for the Model Context Protocol, enabling AI agents to connect to external tools, databases, APIs, and services through standardised server integrations. MCP represents a fundamental expansion of Fuzor's capabilities, allowing seamless integration with a growing ecosystem of MCP-compatible servers.
    - ![MCP Server Configuration](screenshots/changelog/images/mcp_server_config.png)
- **Fuzor-Curated MCP Library**: Pre-configured collection of verified and tested MCP servers that works great with Fuzor.
    - ![MCP Server Configuration](screenshots/changelog/images/mcp_library.png)
- **GitHub MCP Registry Compatibility**: Native support for the GitHub MCP Registry format (`mcp.json` and `mcp.config.json`), allowing installation of MCP servers from any compatible registry. Fuzor automatically transforms registry formats into compatible configurations.
- **MCP Workspace and Global Scopes**: MCP servers can be configured at workspace level (project-specific) or globally (user-wide), with automatic scope management and file-based persistence. Configuration files are stored as `.mcp/config.json` in workspace or global storage directories.
- **Per-Agent MCP Tool Selection**: Fine-grained control over which MCP servers and individual tools are available to each agent. Supports wildcard patterns (`server::*` for all tools from a server) or specific tool selection (`server::tool_name`).
    - ![MCP Server Configuration](screenshots/changelog/images/agent_mcp_selection.png)
- **MCP Transport Support**: Complete implementation of MCP transport protocols including:
    - STDIO transports: NPX (Node.js packages), Python pip packages, and Docker containers
    - Remote transports: HTTP with Server-Sent Events (SSE), Streamable HTTP, and WebSocket connections
    - OAuth 2.1 authentication support for remote servers
- **Automated MCP Package Installation**: Automatic installation of Python pip packages and Docker images when installing MCP servers. The system validates prerequisites and guides users through the installation process.
    > **Note** we weren't able to test everything so if you find any issues with a specific server please open a Git issue for us to review.
- **Chat Export/Import**: Export chat conversations to JSON files for backup, sharing, or archival. Import previously exported chats to restore conversation history or continue discussions from another machine.
    - ![MCP Server Configuration](screenshots/changelog/images/chat_history_import.png)
    - ![MCP Server Configuration](screenshots/changelog/images/chat_history_export.png)
- **Provider Lock Status Indicators**: Chat interface now displays all compatible LLM providers with visual "locked" indicators when configuration is incomplete. Hovering over locked providers shows tooltips explaining what configuration is missing (API key, endpoint, etc.).
    - ![MCP Server Configuration](screenshots/changelog/images/provider_chat_lock.png)
- **Chat History Active Session Highlight**: The current active chat session is now visually highlighted in the chat history sidebar, making it easier to identify which conversation you're currently viewing.
- **Chat History Clear Confirmation**: Added confirmation dialog when clearing all chat history to prevent accidental deletion of conversation data.
- **Universal Copy to Clipboard**: Consistent clipboard functionality throughout the application, allowing you to copy code blocks, tool outputs, configuration snippets, and other content with a single click.
- **Data Analytics Tool Output Rendering**: Purpose-built rendering components for data analysis tool results, displaying Excel, CSV, and JSON data in structured, readable table formats with proper column alignment and formatting.
    - ![Data Analytics Output](screenshots/changelog/images/data_analysis_output_1.png)
    - ![Data Analytics Output](screenshots/changelog/images/data_analysis_output_2.png)
- **Default Agent Tool Customisation**: The built-in FuzorAgent can now be customised with specific Fuzor tool sets and MCP server selections without requiring creation of a custom agent.
- **Enhanced Data Analytics Tools**: Improved tool descriptions and LLM guidance for better tool selection and usage. Added new sub-tool for fetching individual sheets from multi-sheet Excel files, enabling more granular data analysis workflows.
- **Fuzorprompt IntelliSense Enhancement**: Improved syntax highlighting and IntelliSense for `.fuzorprompt` files, providing better auto-completion and validation in preparation for the unified Prompt Library.
    - ![Data Analytics Output](screenshots/changelog/images/fuzor_prompt_highlight.png)
- **Claude 4.5 Haiku Model Support**: Added Claude 4.5 Haiku model to both GitHub Copilot and Anthropic provider configurations, offering a faster, more cost-effective option for lightweight tasks.
- **Git Library Token Authentication**: Support for personal access token (PAT) authentication with the Git library repository, as an alternative to GitHub OAuth sessions.
    > Note: These changes were made to allow users in the future to hook up Fuzor to a different git-library that has a similar structure. The other improvement to this is, in the future we can look at ways to provide git-library access to non-Github users.

### Changed

- **Transformers Has a new home**: The transformer list view has been moved to its own dedicated space. This is in preparation to eventually change Transformer library into a prompt library.
    - ![Data Analytics Output](screenshots/changelog/images/transformer_button_start.png)
    - ![Data Analytics Output](screenshots/changelog/images/transformer_list_view.png)
- **Refreshed Settings Interface**: Complete redesign of the settings view with improved visual hierarchy, clearer section organisation, and better discoverability of configuration options. The new layout groups related settings together and provides contextual help text.
    - ![Data Analytics Output](screenshots/changelog/images/settings_fuzor_ui.png)
    - ![Data Analytics Output](screenshots/changelog/images/settings_mcp_ui.png)
- **Markdown Tools Now Optional**: File-to-Markdown conversion tools moved from built-in tools to optional custom tools. This allows users to deselect them when using MCP-based alternatives like the MarkItDown server, reducing token usage and tool clutter.
- **Improved Version Checking**: Enhanced version checking logic eliminates redundant API calls and handles Git library unavailability more gracefully. Version blacklist warnings now only appear when definitively confirmed, not during temporary network issues.

### Removed

- **Confluence Custom Tool**: The custom Confluence integration tool has been removed. Users should migrate to the Fuzor-curated MCP Confluence server, which provides more comprehensive functionality and follows the standardised MCP protocol.
- **Confluence Integration Settings**: Confluence authentication and configuration settings removed from extension settings. Use the MCP server configuration interface to set up Confluence integration instead.
- **Data Enrichment Tool**: Temporarily removed due to functionality issues. This tool will be revisited and potentially reimplemented in a future release.

### Fixed

- **Tool Approval Button Display**: Resolved an issue where the approval button would not display in all instances where user approval was required for file-modifying tools.
- **Duplicate Webview Command Triggers**: Fixed a bug that caused duplicate command executions in the webview UI due to code sharing between the chat view and library view panels.

### Technical Changes

- **Dependency Updates**: Updated all npm dependencies across main extension, shared library (`@fuzor-ai/shared`), webview-ui, and fuzorWebsite projects to latest stable versions.
- **Cancellation Token Support**: Improved webview RPC command handling with proper VS Code cancellation token support, enabling graceful cancellation of long-running operations.
- **Command Manifest Cleanup**: Removed over a dozen unused VS Code commands from `package.json`, reducing extension footprint and improving activation performance.

## [0.3.20] - 2025-11-01

### Added

- **Mermaid Diagram Support**: Chat now renders Mermaid diagrams directly within conversations, providing visual representations of flowcharts, sequence diagrams, and other diagram types. Each rendered diagram includes an interactive toolbar with a copy-to-clipboard button for reusing the Mermaid code elsewhere, and a regenerate button that allows you to request the AI fix any invalid syntax that prevented proper rendering.
  - ![Mermaid Diagram Example](screenshots/changelog/images/mermaid_example.png)
- **Enhanced Code Block Rendering**: All code blocks within chat conversations now feature syntax highlighting powered by React-Prism, supporting dozens of programming languages including JavaScript, TypeScript, Python, Java, C#, SQL, and many more. Each code block includes a copy-to-clipboard button for easy code reuse, improving the developer experience when working with code snippets.
  - ![Code Block Example](screenshots/changelog/images/code_block_example.png)
- **Tool Approval Workflow**: Implemented a comprehensive approval system for tools that create, modify, or delete files in your workspace. Before any file-modifying operation executes, you'll receive an approval prompt with multiple options: "Allow Once" for single execution, "Allow for Session" to approve all uses during the current chat session, "Always Allow" to permanently approve the tool (saved to settings), or "Deny" to reject the operation. This safety mechanism helps prevent unintended changes to your codebase while maintaining flexibility for trusted operations. Settings are available to enable auto-approval for experienced users who prefer a streamlined workflow.
  - ![Tool Approval Workflow](screenshots/changelog/images/tool_approval_workflow.png)
  - ![Tool Approval Settings](screenshots/changelog/images/tool_approval_settings.png)
- **Enhanced Tool Output Rendering**: Completely redesigned how tool execution results are displayed within chat conversations. Each tool type now has a unique, purpose-built rendering component that presents information in the most appropriate format. Search results show matched files with context snippets, workspace structure displays as an interactive file tree, web content fetches present formatted article content, transformer executions show detailed input/output information, Confluence page fetches and search results display with Confluence-branded styling including metadata badges and collapsible content sections, and error messages provide clear, actionable information with relevant context.
  - ![Search Results Output](screenshots/changelog/images/tool_output_search.png)
  - ![Workspace Structure Output](screenshots/changelog/images/tool_output_workspace.png)
  - ![Fetch Link Content Output](screenshots/changelog/images/tool_output_fetch.png)
  - ![Transformer Execution Output](screenshots/changelog/images/tool_output_transformer.png)
  - ![Confluence Page Output](screenshots/changelog/images/tool_output_confluence_page.png)
  - ![Confluence Search Output](screenshots/changelog/images/tool_output_confluence_search.png)
  - ![Error Output Display](screenshots/changelog/images/tool_output_error.png)
- **Azure OpenAI Provider Validation**: Added comprehensive validation for Azure OpenAI configuration settings. The extension now validates that the resource URL follows the correct Azure format and that the API version adheres to the expected pattern, providing immediate feedback when configuration issues are detected rather than failing during execution.
- **Git Library Validation**: Implemented validation checks for the Git library configuration. When Fuzor is unable to successfully query the configured GitHub library (due to network issues, authentication problems, or invalid repository configuration), you'll now receive clear warning messages explaining the issue and suggesting remediation steps.
- **Add Knowledge CodeLens**: Introduced a new "Add Knowledge" CodeLens button that appears at the top of agent files (`.chatmode.md`), making it significantly easier to add knowledge files to agents. When clicked, the CodeLens presents a user-friendly interface to select files and specify whether they should be added as "core" knowledge (automatically injected into the system prompt for every conversation) or "optional" knowledge (available on-demand through the knowledge retrieval tool). This streamlined workflow eliminates the need to manually edit the agent's frontmatter and ensures proper file path formatting.
  - ![Add Knowledge CodeLens](screenshots/changelog/images/add_knowledge_codelens.png)
  - ![Add Knowledge Selection Interface](screenshots/changelog/images/add_knowledge_selection.png)
- **Core Knowledge Reference Counter**: Added a visual "Used (n) references" label that appears at the start of each AI assistant message in chat conversations. This label is displayed when the active agent has core knowledge files that are automatically injected into the system prompt, providing transparency about which knowledge sources are influencing the AI's responses. The counter shows the exact number of core knowledge files being referenced, helping users understand the context the AI is working with.
  - ![Core Knowledge References Label](screenshots/changelog/images/core_knowledge_references.png)
- **Agent Alias Support**: Added the ability to specify a display alias for agents, providing more user-friendly names in the interface. While the agent file name must follow technical naming conventions (e.g., `architecture-builder.chatmode.md`), you can now define a more readable alias such as "Architecture Builder" that will be displayed throughout the webview interface, including the agent selector, chat header, and agent management screens. This separation between technical identifiers and display names improves user experience without compromising file system compatibility.
  - ![Agent Alias Display](screenshots/changelog/images/agent_alias_display.png)
- **Agent Deletion**: Implemented comprehensive agent deletion functionality that allows users to permanently remove agents they no longer need. When deleting an agent, the system removes both the agent configuration file and its associated knowledge base directory, ensuring complete cleanup. This feature includes confirmation prompts to prevent accidental deletions and provides clear feedback about what will be removed, helping users maintain a clean and organized agent library.
  - ![Agent Delete Confirmation](screenshots/changelog/images/agent_delete_confirmation.png)

### Changed

- **Persistent Chat Sessions**: Chat sessions are now automatically retained when you navigate away from the chat view and return, providing a much smoother experience when you need to temporarily switch to other views like Transformers, Settings, or the main editor. Previously, navigating away would clear your conversation history. To start a new chat conversation, you must now explicitly click the "+" button in the top toolbar, giving you complete control over when to begin fresh conversations versus continuing existing ones.
- **Settings Architecture Refactor**: Completed a major reorganisation of how Fuzor stores and manages settings to create a clearer separation between extension-wide "Fuzor" settings and provider/model-specific settings. Fuzor settings (such as Git library configuration, Confluence credentials, and other extension-wide preferences) are now configured once globally and apply regardless of which AI provider or model you're using. Provider and model settings (API keys, endpoints, model parameters) remain specific to each configuration. An automatic migration script runs on first launch after upgrading, converting your existing legacy settings to the new structure without requiring manual intervention. 
  - **Breaking Change**: If you previously configured different Confluence credentials for different AI providers or models, only one set of credentials will be preserved during the migration process. This is an intentional design decision to simplify credential management going forward.
- **Enhanced File Creation Tool**: The `create_text_file` tool has been significantly expanded to support dozens of additional text-based file formats beyond the original set, including various configuration files, documentation formats, data definition files, and programming language extensions. This enhancement allows AI agents to create a much wider variety of files when assisting with project setup, documentation, and code generation tasks.
- **Default FuzorAgent System Prompt Update**: Updated the default FuzorAgent system prompt to explicitly indicate that transformer tools are not available by default. Users who require transformer creation and execution capabilities in chat must now create and use a custom agent with transformer tools explicitly enabled. This change provides clearer expectations about agent capabilities and encourages more intentional tool permission management.
- **Chat Auto-Scroll Behavior**: Modified the chat scrolling behavior to no longer automatically force scroll to the bottom when the AI sends a response. Previously, whenever a new message was received, the chat would automatically scroll to the latest message, which could be disruptive if you were reading previous messages in the conversation history. The new behavior respects your current scroll position, allowing you to review earlier messages without interruption while still providing the option to manually scroll down to see new responses. This creates a more user-friendly experience, especially during longer conversations where context from previous messages is important.
- **Fuzor Website Mobile Navigation**: Updated the Fuzor website documentation to display a proper burger menu icon for users when viewing on smaller screen sizes. This responsive design improvement ensures that navigation remains accessible and user-friendly on mobile devices and narrow browser windows, allowing users to easily access different documentation pages regardless of their device or screen size.
  - ![Mobile Navigation Burger Menu](screenshots/changelog/images/website_mobile_navigation.png)
- **Improved Version Checking**: Refined the version checking mechanism to eliminate redundant API calls that were creating unnecessary network traffic. Additionally, fixed an edge case where Fuzor would incorrectly indicate that your current version is blacklisted when there was temporary downtime of the Git library hosting the versioning information. The system now handles library unavailability more gracefully and only shows warnings when it can definitively confirm version status.

### Removed

- **Token Limit Setting**: Removed the configurable token limit setting from provider and model configuration as it was introducing unnecessary confusion for users. The extension now automatically uses the correct maximum token limit for each model based on the model's actual capabilities, ensuring optimal performance without requiring manual configuration. This change simplifies the setup process and prevents common misconfiguration issues.
- **Chat Input Controls**: Streamlined the chat interface by removing redundant controls to align with modern agentic chat extension conventions and VS Code's own Copilot chat interface. The "+" button has been removed from the chat input area (use the "+" button in the top toolbar to start new conversations instead), and the "X" close button has been removed (use the Home icon in the top toolbar to return to the main Fuzor view). These changes create a cleaner interface and more consistent user experience.
- **Dynamic Transformer Tool Creation**: Removed the previous system that automatically generated individual tool definitions for every transformer in your workspace and sent them all to the AI model. While this approach provided detailed information about each transformer's capabilities, it could consume a significant portion of the available token budget when working with large transformer libraries (100+ transformers). Transformer execution now uses a generic framework that requires the AI to work with less upfront information. When executing transformers through chat, it's now recommended to provide clear, detailed context about which transformer you want to use, what inputs it requires, and how you want the results formatted to ensure successful execution.

### Fixed

- **Non-Streaming Chat Mode**: Resolved an issue where non-streaming mode was not functioning correctly in chat conversations. Previously, when streaming was disabled, chat responses would fail to display properly or not appear at all. The fix ensures that both streaming and non-streaming modes work reliably, giving users the flexibility to choose their preferred response delivery method based on their workflow and model capabilities.

### Technical Changes

- **Extensive Test Coverage**: Added comprehensive unit tests across both the extension core and webview-ui components, significantly improving code reliability and making it easier to catch regressions during development. The test suite now covers critical functionality including settings management, tool approval workflows, chat session persistence, and provider configuration.
- **File-Based Chat Session Storage**: Migrated chat session storage from VS Code's globalState memory storage to a file-based system where each chat session is stored as an individual JSON file on disk. Each session is saved to the extension's global storage directory with the naming pattern `{sessionId}.json`, providing better scalability for large chat histories, improved performance by avoiding memory limitations, and easier debugging through direct file inspection. The system includes automatic migration logic that seamlessly transfers existing sessions from the old globalState format to individual files on first launch after upgrading, ensuring no chat history is lost during the transition.
- **Webview Build System Migration**: Migrated the webview-ui build system from webpack to Vite, resulting in faster development builds, improved hot module replacement, and better tree-shaking for production bundles. This migration also resolved several persistent dependency bundling issues that were causing runtime errors with certain npm packages.
- **Hot Module Replacement Support for Webview**: Implemented HMR (Hot Module Replacement) support for the webview-ui during development. Vite's native HMR provides instant updates to React components without losing application state when changes are made. The development server runs on port 5173 and communicates with the VS Code Extension Development Host, enabling fast, state-preserving updates to UI components. This dramatically improves developer productivity by eliminating the need to manually reload during iterative UI development.
- **Standalone Webview Warning**: Implemented a development-time safety feature that displays an informative warning message when developers attempt to access the webview-ui dev server directly in a browser (e.g., http://localhost:5173). The warning explains that the webview must be run through the VS Code Extension Development Host and provides step-by-step instructions on the proper development workflow, including how to launch with F5 and benefit from HMR. This prevents confusion and ensures developers use the correct HMR-enabled development setup.
- **SharePoint Deployment Authentication**: Enhanced the SharePoint deployment script to validate authentication credentials before attempting to deploy documentation files. The script now performs an upfront authentication check, providing immediate feedback if credentials are invalid or expired, preventing partial deployments and reducing debugging time when deployment issues occur. This improvement ensures more reliable and predictable documentation deployment workflows.
- **Webview Testing Framework**: Integrated Vitest as the testing framework for the webview-ui project, which previously lacked any testing infrastructure. The new setup enables component testing for React components and unit testing for utility functions, ensuring the chat interface and other webview components maintain expected behaviour across changes.
- **Code Quality Enforcement**: Added ESLint configuration to all projects within the monorepo (extension core, webview-ui, shared library, and fuzorWebsite) to enforce consistent coding standards across the codebase. The ESLint rules include TypeScript-aware checks, React best practices, and custom rules specific to VS Code extension development. Running `npm run lint` before commits ensures code quality compliance.
- **Dependency Updates**: Updated all dependencies across all projects to their latest stable versions, incorporating security patches, performance improvements, and new features from upstream packages. This includes updates to the VS Code extension API, React, TypeScript, build tools, and all supporting libraries.

## [0.3.16] - 2025-10-22

### Technical Changes

- **Extensive Test Coverage**: Added comprehensive unit tests across both the extension core and webview-ui components, significantly improving code reliability and making it easier to catch regressions during development. The test suite now covers critical functionality including settings management, tool approval workflows, chat session persistence, and provider configuration.
- **Main Extension Build System Migration**: Migrated the main extension project from webpack to Vite, bringing the same performance benefits and developer experience improvements to the core extension code that were previously available only in the webview. This migration enables faster build times, more efficient code splitting, and better development iteration cycles when working on the extension host code.
- **Webview Build System Migration**: Migrated the webview-ui build system from webpack to Vite, resulting in faster development builds, improved hot module replacement, and better tree-shaking for production bundles. This migration also resolved several persistent dependency bundling issues that were causing runtime errors with certain npm packages.
- **Hot Module Replacement Support**: Implemented comprehensive HMR (Hot Module Replacement) support for both the webview-ui and main extension projects. For the webview-ui, Vite's native HMR provides instant updates to React components without losing state. For the main extension, implemented automatic webview refresh functionality that monitors changes to distribution files (JavaScript, CSS, HTML) and reloads the webview when changes are detected. The file system watcher uses a 300ms debounce to avoid multiple rapid reloads, significantly improving the developer experience by eliminating the need to manually reload the extension during development. HMR features only activate when the extension is running in development mode, ensuring zero overhead in production environments.
- **Webview Testing Framework**: Integrated Vitest as the testing framework for the webview-ui project, which previously lacked any testing infrastructure. The new setup enables component testing for React components and unit testing for utility functions, ensuring the chat interface and other webview components maintain expected behaviour across changes.
- **Code Quality Enforcement**: Added ESLint configuration to all projects within the monorepo (extension core, webview-ui, shared library, and fuzorWebsite) to enforce consistent coding standards across the codebase. The ESLint rules include TypeScript-aware checks, React best practices, and custom rules specific to VS Code extension development. Running `npm run lint` before commits ensures code quality compliance.
- **Dependency Updates**: Updated all dependencies across all projects to their latest stable versions, incorporating security patches, performance improvements, and new features from upstream packages. This includes updates to the VS Code extension API, React, TypeScript, build tools, and all supporting libraries.

## [0.3.16] - 2025-10-22

### Added

- **General**: Underlying exception message logged to Output window when errors occur
- **Global Settings**: `Show stack trace on errors` option
  - When errors are logged within Output window, stack traces will be included for debugging
- **Settings et al**: Clicking on labels sets focus to associated input field, or toggles checkbox/radio button

### Fixed

- Windows Open File dialog failure when selecting files within the workspace folder

## [0.3.15] - 2025-10-18

### Added

* **Agent Configuration UI**: Interactive CodeLens interface for configuring Fuzor tools in chatmode files
  - New CodeLens provider displays "Configure Fuzor Tools..." action above `fuzorTools` frontmatter attribute in `.chatmode.md` files
  - Multi-select QuickPick UI allows users to enable/disable Fuzor tool sets for individual agents
  - Automatic frontmatter updating with proper YAML formatting preservation
  - Support for both user agents (global storage) and repository-based agents (`.github/chatmodes`)

* **SharePoint Deployment Automation**: Complete deployment system for documentation
  - Complete deployment documentation in `deployment.md`
  - Note: This deployment to SharePoint still contains a developer to run it manually.

### Fixed

* Minor improvements to chat context and agent file URI tracking preventing Knowledge base from being detected in agents containing dashes in their names.

## [0.3.14] - 2025-10-17

### Added

* **Advanced File-to-Markdown Conversion Tools**: New AI agent tools for enhanced document processing
  - `convert_office_to_markdown`: Convert Office documents (DOCX, DOC, XLSX, XLS, PPTX, PPT) to Markdown with full formatting preservation
  - `convert_pdf_to_markdown`: Convert PDF files to Markdown with page range control and image extraction
  - Integrated PDFium library for robust PDF processing with configurable page limits and image rendering
  - Enhanced image processing with PNG optimization for AI consumption

* **File Utilities Enhancements**: New file system utilities for robust file operations
  - Added `ensureDirectoryExists` function for reliable directory creation
  - Added `writeFileToPath` function for safe file writing with automatic directory creation
  - Improved file system error handling and path resolution

### Changed

* **Build System Improvements**: Updated version management and installation scripts
  - Modified `update_version.py` to run `npm run format:fix` as the final step for consistent code formatting
  - Changed `install:all` script to use `npm install` instead of `npm clean-install` for better caching
  - Enhanced shared prompt system with improved agent behavior and reasoning capabilities

### Fixed

* **Dependency Management**: Resolved npm installation issues by clearing corrupted node_modules in shared directory and reinstalling dependencies

## [0.3.13] - 2025-10-16

### Added

* **Extension Download & Installation**: In-extension download capability for new versions
  - Download and install updates directly from GitHub without leaving VS Code
  - Automatic version detection and streamlined update process
  - Requires GitHub authentication for access to releases

* **Enhanced Diff Preview Tool**: Integrated VS Code's built-in diff viewer for file changes
  - Side-by-side comparison shows exact changes before applying them
  - Users can preview, accept, or reject changes to prevent unintended modifications

### Fixed
 - Fixed issue where creating a new transformer would lose all form data when validation errors occurred


## [0.3.12] - 2025-10-15
#### Added
**AI Model Support**
- Added `claude-sonnet-4.5` model configuration to GitHub Copilot provider
  - Max tokens: 4,096
  - Context window: 128,000
  - Max input tokens: 89,827
  - Supports: Temperature, Top-P, and images
  - Pricing: Free (via Copilot subscription)
- Added `claude-sonnet-4.5` model configuration to Anthropic provider
  - Max tokens: 64,000
  - Context window: 200,000
  - Input price: $3 per million tokens
  - Output price: $15 per million tokens
  - Supports: Temperature and Top-P


## [0.3.11] - 2025-10-15

### Added

* **Confluence Integration**: Complete Confluence integration system enabling AI agents to interact with Confluence content
  - New `confluenceUtils.ts` utilities for fetching pages, searching content, and handling authentication
  - New `confluenceTools.ts` AI tools for seamless Confluence operations within chat
  - Support for multiple view types (editor, export_view, anonymous_export_view) and content expansion options
* **Enhanced Document Processing**: New dependencies for improved file handling
  - Added `turndown` for HTML to Markdown conversion
  - Added `mammoth` for Microsoft Word document processing
  - Added `@types/turndown` for TypeScript support
* **Installation Script Improvements**: Enhanced build process with separate CI and regular installation modes
  - `install:all` for regular development installs
  - `installci:all` for CI environment installs
  - Better dependency management and caching

### Changed

* **Dependency Cleanup**: Removed deprecated packages for cleaner dependency tree
  - Removed `@types/dotenv`, `@types/xlsx`, and `npm-run-all`
  - Updated package management scripts for better maintainability
* **Chat Enhancements**: Various improvements to chat functionality
  - Enhanced chat input handling and layout improvements
  - Improved mention system and tool call parsing
  - Added undo stack functionality for better user experience
* **Version Management**: Bumped all package versions to 0.3.11

### Fixed

* Minor code improvements and formatting fixes across the codebase

## [0.3.10] - 2025-10-13

### Changed

* **Tool Classification Changes**: Reorganised agent tools for better default experience
  - **File-to-Markdown tools** moved to **built-in (system) tools**: Now always available to agents by default, enabling seamless document conversion without manual configuration
  - **Transformer tools** moved to **custom (user) tools**: Now require manual selection, providing more granular control over when agents can create and execute transformers

## [0.3.9] - 2025-10-11

### Added

* **Agent Tools for Transformers**: New transformer tools enabling AI agents to create, update, search, and execute transformers directly through chat:
  - `create_transformer`: Create new transformers with specified prompts, inputs, and configuration
  - `update_transformer`: Modify existing transformers including prompts, settings, and metadata
  - `search_transformers`: Find transformers by name, description, or folder without requiring explicit "!" symbol references
  - `execute_transformer`: Run transformers directly from chat with dynamic input schemas
* **Chat Management Tool**: New `rename_chat_session` tool for managing chat sessions
  - Allows AI agents to rename the current chat session when explicitly requested by the user
* **File-to-Markdown Conversion Tool**: New `convert_file_to_markdown` tool for Office documents and PDFs
  - Office documents (DOCX, DOC, XLSX, XLS, PPTX, PPT)
  - PDF files
  - Preserves formatting including tables, lists, and headings
  - For Excel data analysis, the dedicated Data Analysis tools are preferred
* **Version Management System**: Automatic version checking with comprehensive status tracking
  - Update notifications via status bar indicator when new versions are available
  - Unsupported version warnings for versions no longer receiving support
  - Blacklist protection for versions with critical bugs
  - Dismissible notifications per release
  - Periodic hourly checks when online
* **Enhanced Chat Provider Support**: Added full chat integration for:
  - Anthropic (Claude models) with streaming and tool support
  - Gemini (Google AI) with streaming and tool support
  - GitHub Copilot (tool calling support planned for future release)
* **Drag & Drop Functionality**: 
  - Files from VS Code explorer can be dragged into chat (hold Shift to drop)
  - Transformers from tree view can be dragged into chat (hold Shift to drop)
* **Selective Fuzor Tools**: Transformers can now specify which Fuzor tools they have access to via new UI selector
* **Documentation Website**: 
  - New GitHub Pages hosting at `https://vigilant-enigma-8e9l98e.pages.github.io/`
  - GitHub Wiki for searchable guides at `https://github.com/Deloitte-Australia/fuzor-ai-transformer/wiki`
  - Offline documentation bundled with extension
  - Enhanced README files for each project component

### Changed

* Migrated Anthropic, Gemini, and GitHub Copilot providers to Vercel AI SDK for consistency and better tool integration
* Refactored LLM clients for improved streaming support and tool execution
* Enhanced transformer execution state management with unified cancellation control
* Improved telemetry for version checks and tool usage
* Updated documentation structure for better discoverability

### Fixed

* Resolved issue with Custom provider settings not being editable
* Improved tool error handling and validation
* Fixed file path resolution in file conversion tools
* Enhanced transformer execution state management to prevent race conditions

## [0.3.7] - 2025-09-28

### Added

* **Token Usage Monitoring**: New feature for tracking token usage in conversations with visual progress indicators and color-coded thresholds
* **Chat History Management**: Complete session management system with save/load, clear, delete, search, and export capabilities for chat sessions
* **Conversation Optimisation**: Intelligent tools to manage long conversations by summarising content with different prioritisation modes or removing older messages while preserving recent context
* **Optimisation UI**: Popup interface providing multiple optimisation strategies including balanced summaries, user-focused prioritisation, AI-focused prioritisation, and selective message removal

### Changed

* Bumped all package versions to 0.3.7

### Fixed

* Minor code improvements and formatting fixes

## [0.3.6] - 2025-09-26

### Added

* **VS Code Language Model Tools**: New integration allowing language models to access data analytics functionality directly within VS Code
* **Data Analytics Tools**: Comprehensive tools for dataset operations including get_dataset_headers, get_dataset_slice, get_unique_values, get_dataset_stats, filter_dataset, and aggregate_dataset
* **Tool Base Classes**: BaseVSCodeTool and DelegatingVSCodeTool classes for consistent tool implementation and registration

### Changed

* Bumped all package versions to 0.3.6
* Updated package.json with languageModelTools configuration for all data analytics tools

### Fixed

* Minor formatting and code style improvements

## [0.3.2] - 2025-09-22

### Added

* **Website Frontend**: Complete React-based website application with navigation, theming, and multiple pages including Home, Docs, and Roadmap
* **Roadmap Diagram**: Interactive roadmap visualization component using ReactFlow showing project phases and components
* **Documentation Webview**: New webview panel that embeds the website's documentation within VS Code
* **Data Enrichment Tools**: AI tools for loading and processing CSV and Excel files with secure expression evaluation
* **System Prompt Enhancements**: Updated shared system prompt to emphasize agent persistence, thorough reasoning, and clear communication before tool calls

### Changed

* Updated build scripts to include fuzorWebsite builds and installs
* Bumped all package versions to 0.3.2

### Fixed

* Minor build configuration updates

## [0.3.0] - 2025-09-18

### Added

* **Agent Library**: Working version of agents library with available tools
* **User Tools**: Data analysis tools, file tools, enhanced tool calling capabilities and streaming support across multiple AI providers
* **Knowledge Base**: Basic knowledge base with workspace context, knowledge base improvements, limit chat mode providers
* **Reasoning**: Feature for reasoning
* **Response UI**: Feature for response UI
* **Token Usage**: Feature for token usage
* **Finish Reasons**: Feature for finish reasons
* **Chat Enhancements**: Provider and model selection in chat view, chat history modal, unified chat input and settings, improved chat input area styling, image pasting, alpha mode toggle, chat message cancellation, chat history support, file attachments, command execution from webview, streaming responses, provider info display, chat session management (fork, clear)
* **Agent Builder**: Feature for agent builder
* **Agents SDK**: Use agents API, initial system message, unified chat message storage, prioritized text over images, integrated OpenAI Agent SDK, improved Markdown rendering, consolidated chat streaming
* **UI Updates**: Enhanced button hover effects, refined chat input styling

### Changed

* Major Webview-UI Refactor
* Update to use vercel
* Refactored LLM clients to use SDKs (Azure OpenAI, OpenAI, Deloitte)
* Enhanced Deloitte client image handling and authentication retry logic
* Unified chat streaming and history handling
* VS Code version back to 1.104
* Excludes shared directory from VS Code indexing

### Fixed

* Transformer bugs
* Transformer input bug
* Format fixes - Tools error handling
* Chat history fixes
* Fix brackets
* Various format fixes

### Removed

* Remove old file
* Remove new chat button (for stability)

## [0.2.3] - 2025-09-05

**Key Features Added:**
* **Interactive Chat Interface**: New React-based chat UI with message history, user input, and AI responses
* **File Attachment Support**: Upload and process text files, images, and documents within chat conversations
* **Streaming Responses**: Real-time streaming of AI responses with progress indicators
* **Chat Session Management**: Save, load, and manage multiple chat sessions with persistent history
* **Multi-Provider Support**: Compatible with all existing AI providers (OpenAI, Azure OpenAI, GitHub Copilot, Gemini, etc.)
* **Advanced Attachment Processing**: Support for various file types including PDFs, documents, images with metadata extraction
* **Chat History**: Persistent chat sessions with search and management capabilities
* **Provider/Model Selection**: Dynamic selection of AI provider and model within the chat interface

## [0.2.2] - 2025-08-29

### Added

* Added functionality to specify a model a Fuzor needs to run on.

### Changed

* Updated all dependencies to the latest versions.

### Fixed

* Resolved issue with gpt-5 and gemini-2.5-pro models not working due to incorrect configuration
* Resolved issue with duplicate gpt models being displayed for Azure Open AI provider.

## [0.2.1] - 2025-08-25

### Fixed

* Resolved issue with default value not working correctly for non-string values specified in placeholder

## [0.2] - 2025-08-16

### Added

* Added support for additional model capabilities (top_p, top_k, frequency_penalty, logprob, reasoning_effort, seed, presence_penalty, etc.) that show only when the model supports them. You can use this if you want to specify default parameters for a specific model.
    - Users can also add custom model capabilities. This is useful if you need to use a parameter not 'known' by Fuzor.

      

![Model Capability Preview](screenshots/changelog/images/model_capabilities_preview.png)

* Added functionality to override additional model capabilities on a transformer level
    - 

![Fuzor Model Capability](screenshots/changelog/images/fuzor_model_capabilities_preview.png)

* Added custom headers configuration for API calls, useful for Custom provider with different request header structures
    - 

![Custom Header Preview](screenshots/changelog/images/api_custom_headers_preview.png)

* Added new filter capabilities for the `rows` placeholder namely:
    - filterOnSheet - A dropdown will appear allowing you to select a specific sheet in the excel file to filter the data on.
    - filterOnSheetColumns - A comma separated text-field to specify a list of column names (in the filtered sheet)
    - includeHeaderColumnIndex - Specify the start of the header row if your excel sheet doesn't use the first row for headers.
     - Example:

 <span v-pre> `{{rowData::rows::{"filterOnSheet": true, "filterOnSheetColumns": true, "includeHeaderColumnIndex": true }}}` </span>

      

![Row Placeholder preview](screenshots/changelog/images/row_placeholder_preview.png)

* Added min length, max length, and pattern validation for textArea, string, and text placeholders.
    - Example: <span v-pre>`{{username::text::{"minLength":3,"maxLength":20,"pattern":"^[a-zA-Z0-9_]+$"}}}`</span>
* Added support for running multiple different Fuzors in parallel
* 

![Running multiple fuzors](screenshots/changelog/images/running_multiple_fuzors_preview.gif)

* Added parallel count setting to override max parallel count (default 5, max 20) for rows / folder execution
* Added preview functionality for placeholders when editing a Fuzor prompt.
* Added setting to prevent Fuzor from stealing focus when generating output
* Placeholders can now be marked as optional if they're not required by a Fuzor.
  Example prompts:

```
    // all of these placeholders are marked as optional
    <span v-pre>{{input?::file}}</span>
    <span v-pre>{{text::text?}}</span>
    <span v-pre>{{select?::select::["a", "b"]}}</span>
    <span v-pre>{{folder::folder?}}</span>
    <span v-pre>{{description?::textArea}}</span>
    <span v-pre>{{notes::textArea?::{"default":"No notes"}}}</span>
```

Adding a '?' symbol inside the prompt will mark it as optional.

### Changed

* Updated all dependencies for Webview and VSCode components
* Updated **most** of the providers to include latest known models:
    - OpenAI: gpt-5, gpt-5-mini, gpt-5-nano
    - Grok: grok-4
    - Anthropic: claude-4.1-opus, claude-4-opus, claude-4-sonnet
    - Deloitte: gpt-5
    - Gemini: gemini-2.5-pro, gemini-2.5-flash, gemini-2.5-flash-lite, gemini-2.0-flash, gemini-2.0-flash-lite
    - Mistral: Updated it to point towards all the latest premier models.
        - This will ensure Mistral always uses the latest version of the selected model.
    - Deepseek: deepseek-chat, deepseek-reasoner. These models will update to use the latest versions based on what's available on Deepseek's API.
        - deepseek-chat points to `DeepSeek-V3-0324` at the time of writing.
        - deepseek-reasoner points to `DeepSeek-R1-0528` at the time of writing.
    - Azure-OpenAI: Updated to include all the latest models it supports (including gpt-5)
    - OpenRouter: Refreshed the model-list to include all the models it currently supports (400+ models)
* Enhanced Fuzor Auth provider to prevent multiple browser instances for batch processing

### Fixed

* Fixed issue where executing Fuzor doesn't show the Fuzor's name in the notification
* Fixed issue where clicking on a Transformer from Fuzor settings page doesn't load the transformer
* Fixed an issue where stopping a Fuzor running from the 'View' page still allowed it to continue executing.
* Fixed an issue where cancelling a running Fuzor didn't stop it from outputting the result.

## [0.1.2] - 2025-07-31

### Changed

* Updated error message for when a non-AU Deloitte employee tries to access the Deloitte provider.
* Updated the default behaviour for providers to assume images are supported for models not explitcitly defined.

### Fixed

* Fixed an issue with the Deloitte provider not reading its model settings correctly
* Fixed an issue with the Custom provider not reading its model settings correctly
* Fixed an issue with Azure provider trying to use unsupported parameters for mini-models (o1, o3, o4)

## [0.1.0] - 2025-03-27

### Added

* Added Deloitte AI integration.
* Added Deloitte model.
* Added Deloitte API Key.
* Implemented Deloitte authentication functionality.
* Added Deloitte recommended wordings

### Fixed

* Format fixes in various parts of the codebase.

## [0.0.32] - 2025-03-18

### Fixed

* Corrected an issue with creating fuzor based on description.
* Optimized the previous fix to reduce its size and potential impact.

## [0.0.31] - 2025-03-07

* Minor fixes for relative paths
* Make run in parallel a global setting

## [0.0.30] - 2025-03-03

### Added

* Support images as inputs when using openAI and AzureOpenAi
* Open all models supported by Github Copilot
* Enhaced Select Type for user - <span v-pre>{{name::select::["option1", "option2"]::["display1", "display2"]}}</span>
* Settings is now managed by Fuzor rather than VSCode. More control over models and settings.
* Remember model settings for each model.
* Removed DeepSeek
* More warning messages for user related to being careful around client data.
* Rows type now support parallel and sequenctial execution. Previously only supported parallel. This is useful when order matters.
* Add support for OpenRouter

### Changed

* Users will need to accept terms and conditions for each model.
* Much less noise for user in logs

### Fixed

* Resolved minor formatting issues to improve code readability.

## [0.0.29] - 2025-02-25

### Added

* Added help button to the edit page.
* Created new transformer and buttons for functionality.
* Added close button and `enter` functionality.
* Opens home page on an empty click.
* Added home buttons and a logo.
* Added new transformer creation functionality.
* Added input and create button along with sparkle effect.

### Changed

* Swapped view/edit and transformers around.
* Updated UI and icon designs.
* Adjusted CSS for transformer creation functionality.
* Styling improvements and color scheme adjusts according to the theme.

### Fixed

* Fixed dependency issues.
* Fixed formatting in multiple components.
* Addressed issues with the start menu and improved navigation by allowing clicks on empty space.
* Formatting fixes across various parts of the codebase.

### Removed

* Removed the input text and create button when the web view becomes small.
* Removed on-click functionality for empty space in viewTransformer.
* Removed help section.
* Removed a CSS file to streamline styling.

## [0.0.28] - 2025-02-18

### Added

* Major: Manual ordering of transformers, apps and folders.
* Major: Execute folders - Execute all transformers in a folder sequentially.
* Major: Created help button with easy access to help page.
* Major: Added new AI Provider Grok - Grok! Grok! Grok!.
* Minor: Preview LLM prompt for Apps.

### Changed

* Refactored TransformerProvider to be more AI friendly
* Refactored BaseExecutor to be more AI friendly

## [0.0.27] - 2025-02-14

### Added

* Added functionality for handling xlsx and xls file formats.
* Added xlsx package to support new file functionalities.
* Implemented row preview feature for better data visualization.
* Integrated validation in promptUtils to enhance user input handling.
* Added createdBy name field to improve user identification.

### Changed

* Updated transformer library to display the correct icon for enhanced user interface experience.

### Fixed

* Resolved format issues to ensure consistent file processing.
* Fixed issue with test files to improve testing accuracy.
* Addressed errors related to missing first row or column, now system ignores empty rows/columns following the table.

### Removed

* No features were removed in this release.

## [0.0.26] - 2025-02-13

### Added

* Save editor functionality.
* New logo.

### Changed

* Merged branches 'main' and 'feature/save-editor' for save editor integration.
* Integrated 'feature/save-editor' into 'feature/logo' branch.

## [0.0.25] - 2025-02-13

### Added

* Add support for Mistral AI.

## [0.0.24] - 2025-02-11

### Added

* Implemented initial functionality for Fuzor Agents.
* Added support for file selection and editing.
* Introduced the ability to add output folder.
* Enhanced job functionality by adding job IDs.
* DebugExecute functionality is now available.
* Implemented execution progress display with success checkmarks.
* Last output can now be stored in storage.
* Apps now support drag and drop.
* Added a single configuration file for execution instead of a separate AgentConfig.
* Enhanced UI for a better outputs view.

### Changed

* Renamed "steps" to "jobs" to better represent their functionality.
* Altered "Agents" to "Apps" to unify the application structure.
* Modified apps to be the core components of the system; everything is treated as an app.
* Updated job name editing process for improved user interaction.
* Updated icons to match expanded and collapsed states.
* Reformatted components for better execution flow, with a focus on transformer and agent execution.
* Rearranged components within the app view for improved UX.

### Fixed

* Fixed issues where folders were not being displayed correctly.
* Rectified multiple unit test issues, ensuring all tests now pass.
* Applied various format fixes for consistency and readability.
* Addressed bugs in prompt utilities and general execution flow.

### Removed

* Separated step component to reduce file size, making project scaling more efficient.

## [0.0.23] - 2025-02-05

### Added

* Added Telemetry event for better tracking.
* Added more telemetry to enhance monitoring.
* Added more disallowed file types to improve security and compatibility.
* Added a new window for improved user interaction.

### Changed

* Cleaned up logging for better readability and maintainability.
* Improved logging fixes for more accurate debugging.
* Updated formatting for consistency across the codebase.

### Fixed

* Fixed style issues to ensure a consistent UI/UX.
* Fixed errors for videos/images, now throws an error if the file fails to read.

### Removed

* No features were removed in this release.

## [0.0.22] - 2025-02-04

### Fixed

* Fixed CSV reading issues
* Fixed issues with reading rows
* Formatted labels for better consistency

### Changed

* Merged branch 'main' into 'feature/csv-fixes' to incorporate CSV-related fixes and improvements

## [0.0.18] - 2025-02-01

### Added

* Added support for the Anthropic AI provider, including client functionality implementation.
* Added response streaming capabilities for real-time output file writing.
* Added telemetry functionality to track executions and events across the application.
* Added `anthropic-ai/sdk` (v0.36.3) as a dependency.
* Added required configuration properties: `APIKey` and `ModelName`.

### Changed

* Updated README.md to reflect new Anthropic AI provider support.
* Adjusted logging level for request/response payloads for better debugging.
* Cleaned up formatting across the codebase.
* Refactored response streaming to ensure compatibility with existing test cases.
* Enhanced telemetry integration across LLMs, execution engine, and transformers.

### Fixed

* Fixed deepseek configuration issues.
* Fixed formatting issues with Prettier.
* Fixed telemetry connection string handling and added warnings for missing configurations.

### Removed

* Removed unnecessary telemetry event posts to streamline performance.

## [0.0.17] - 2025-01-29

### Added

* First version of rows implementation.
* Support for running rows in parallel, with a limit of up to 10 rows.
* Progress display functionality to track task execution.
* Parallel processing capabilities with the ability to cancel processes.

### Changed

* Updated temperature setting to 0 for improved performance or behavior.

### Fixed

* Corrected CSV parsing to ensure accurate data handling.

### Removed

* No features were removed in this release.

## [0.0.16] - 2025-01-28

### Added

* Open file during overwrite functionality
* Enhanced prompts for generating fuzors and fuzorPrompts
* Initial working version of Fuzor Generation

### Changed

* Improved Fuzor Generation process

### Removed

* Redundant test cases

## [0.0.15] - 2025-01-27

### Added

* Added a dedicated environment for developing Fuzor.
* Added functionality to view full changelog and current release notes.
* Reintroduced the `join files` function.

### Changed

* Updated the changelog function to support full view and current release notes.

### Fixed

* No fixes in this release.

### Removed

* No features were removed in this release.

## [0.0.14] - 2025-01-26

### Added

* Added a script to fetch git commits for changelog generation.
* Introduced automatic changelog generation based on commit history.
* Added a script to generate historic changelog entries.

### Changed

* Updated the changelog generation process to include the latest changes automatically.

### Fixed

* No bug fixes in this release.

### Removed

* No features were removed in this release.

## [v0.0.13] - 2025-01-26

### Added

* Parallel execution option
* Progress indicator for operations
* User guide

### Changed

* Refactored viewEditTransformer and baseExecuter
* Improved state retention
* Enhanced export folder functionality

### Fixed

* Corrected output filename setting

### Removed

* Removed custom VSCode colors

## [v0.0.12] - 2025-01-24

### Added

* Support for all extension changes
* Optimised UX improvements

### Changed

* Updated fetchFileContent to use latest release asset

### Fixed

* Format fixes for Windows
* Fixed tooltip changes

### Removed

* Removed custom VSCode colors

## [v0.0.11] - 2025-01-23

### Added

* Validate functionality for folders
* More unit tests
* Structure validations

### Changed

* Updated package configurations

### Fixed

* Fixed validation issues

### Removed

* Removed redundant features

## [v0.0.10] - 2025-01-22

### Added

* Select type input
* Support for relative paths
* Editable input boxes
* Better placeholder messages

### Changed

* Improved description for temperature settings
* Enhanced color changes support

### Fixed

* Fixed preview and import issues
* Fixed validation and formatting

### Removed

* Removed redundant features

## [v0.0.9] - 2025-01-21

### Added

* Github Copilot integration
* Custom class extending LLMBase
* Proxy APIM support for Azure OpenAI instances

### Changed

* Updated readme screenshots
* Improved readme documentation

### Fixed

* Fixed name and description disappearance issue

### Removed

* Removed redundant features

## [v0.0.8] - 2025-01-20

### Added

* Consistent code formatting and linting
* Updated design documentation

### Changed

* Updated package scripts
* Reverted node version to 20

### Fixed

* Fixed webvitals for new version
* Fixed package lock issues

### Removed

* Removed feature branch build

## [v0.0.6] - 2025-01-19

### Added

* Folder management functionality
* Drag and drop support
* Delete and rename folder features

### Changed

* Improved folder sorting
* Updated library UI

### Fixed

* Fixed unit tests
* Fixed first loading issues

### Removed

* Removed redundant features

## [v0.0.5] - 2025-01-18

### Added

* New React webview
* Icon support
* Edit Transformer functionality
* Enhanced prompt validations
* Language registrations for .fuzor and .fuzorprompt

### Changed

* Moved styles to different files
* Updated package version

### Fixed

* Fixed unit tests
* Fixed npm package caching

### Removed

* Removed process option web UI

## [v0.0.4] - 2025-01-17

### Added

* Import-export capability for Transformer config
* Default folder open location

### Changed

* Updated package version

### Fixed

* Fixed unit tests

### Removed

* Removed redundant features

## [v0.0.3] - 2025-01-16

### Added

* DeepSeek and Azure OpenAI support
* Terms and conditions
* Consistent naming updates

### Changed

* Updated Readme to use consistent name
* Aligned version in package

### Fixed

* Removed error log and made it info
* Fixed unit tests

### Removed

* Removed redundant features
