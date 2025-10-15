---
title: Changelog
order: 1.1
parent: 'index.md'
---

# Changelog

All notable changes to the "fuzor-ai-transformer" extension will be documented in this file.
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
