
<h1 align="center">
PromptRefiner for VS Code 🚀
</h1>

<br> prompt-refiner/
<br>  ├ .vscode/               # デバッグ設定（F5で拡張機能を実行する設定）
<br>  ├ src/
<br>  │   ├ extension.ts       # 拡張機能のエントリポイント（APIの登録など）
<br>  │   ├ providers/
<br>  │   │   ├ promptProvider.ts  # 仮想ファイル (prompt://) の管理ロジック
<br>  │   │   └ viewProvider.ts    # サイドパネル (Webview) の表示・通信制御
<br>  │   ├ services/
<br>  │   │   └ aiService.ts       # vscode.lm API を使った校正ロジック
<br>  │   └ webview/           # サイドパネル内のフロントエンドコード
<br>  │  &nbsp;&nbsp;&nbsp;&nbsp; ├ main.js        # Webview内のJS（コピーボタンの制御など）
<br>  │  &nbsp;&nbsp;&nbsp;&nbsp; └ style.css      # サイドパネルの見た目
<br>  ├ media/                 # アイコンや画像などの静的資産
<br>  ├ package.json           # 拡張機能の定義（サイドパネルの登録やコマンド定義）
<br>  ├ tsconfig.json          # TypeScriptの設定
<br>  └ README.md              # 整備したプロジェクト概要

「誤送信ゼロ」と「最高品質のプロンプト」を両立する、プロンプト専用サンドボックス。

AIチャット（Copilot等）への入力を開始する前に、このサイドパネルでプロンプトを練り上げます。誤ってEnterを押しても送信されることはありません。AIがあなたの意図を汲み取り、より精度の高いプロンプトへリアルタイムで昇華させます。

## ✨ 主な機能
リアルタイム・インテリジェンス校正

## 入力中の誤字脱字を即座に修正（例：「このファイナル」→「このファイルを」）。
AIにとって曖昧な表現を、具体的で構造的なプロンプトへ自動最適化。

## セーフティー・改行設計
Enter キーは常に改行として機能。誤送信のストレスから解放されます。

## 「一手間」のコピー儀式
校正後のプロンプトを確認し、明示的にコピー操作（または専用ボタン）を行うことでクリップボードへ。そのままCopilot Chatへシームレスに貼り付け可能。

## VS Code ネイティブ統合
サイドパネルに常駐。GitHub Copilotの vscode.lm APIを利用するため、追加のAPIキー設定は不要。

## 🛠 開発者向け情報
### 推奨スタック
Version Control: GitHub（VS Code Marketplaceとの親和性、GitHub Actionsによる自動配布のため）

### Language: TypeScript
API: VS Code Language Model API (GitHub Copilotの推論能力を活用)

### セットアップ
このリポジトリをクローン

npm install を実行

F5 キーを押して、拡張機能開発用ウィンドウを起動

サイドバーの PromptRefiner アイコンをクリックして開始

### 🛠 開発に役立つ「もう一歩先のツール」の提案
GitHub以外で、VS Code拡張機能開発において検討に値するツールをいくつか紹介します。

1. Yeoman & vscode-generator-code (必須級)
拡張機能のディレクトリ構造を自動生成するツールです。yo code と打つだけで、TypeScriptの設定やテスト環境が整った状態で開発をスタートできます。

2. Azure DevOps (代替候補)
もし将来的にエンタープライズ向けの厳格な管理が必要になった場合、Microsoft製品との親和性がGitHub以上に高い場合がありますが、個人・チーム開発ならGitHubで十分です。

3. Webpack / Esbuild
拡張機能は一つのJSファイルにビルドする必要があります。最近は高速な esbuild を使うのが主流です。

## 🛠 アーキテクチャ：仮想ファイルによるプロンプト編集
- 本拡張機能は、プロジェクトディレクトリ内に物理的なファイルを作成することなく、メモリ上の仮想ドキュメントとしてプロンプトを管理します。
- Prompt Workspace (Virtual File): 独自のURIスキーム prompt://refiner/scratchpad.md を使用。VS Code標準のMarkdownエディタ機能をフル活用でき、Enter キーによる自由な改行と編集が可能です。
- Structured Markdown Output: AIによる校正結果は、単なるテキスト修正に留まりません。役割（Role）、背景（Context）、制約事項（Constraints）などが適切に構造化された Markdown形式のプロンプト として生成されます。

## 🚀 特徴的なワークフロー
- Markdownで自由に起稿: 仮想ファイル上で、表やリスト、コードブロックを用いて複雑な前提条件を記述。
- リアルタイム構造化: AIが入力内容を解析し、最適なプロンプト構造（# 指示 # 制約 等）に自動でリライト。
- プレビュー & 確定: サイドパネルに表示された「洗練されたMarkdownプロンプト」を確認し、納得したらクリップボードへコピー。

---

<h1 align="center">
VS Code Extension Samples 
</h1>

This repository contains sample code illustrating the VS Code extension API. Each sample is a self-contained extension that explains one topic in [VS Code API](https://code.visualstudio.com/api/references/vscode-api) or VS Code's [Contribution Points](https://code.visualstudio.com/api/references/contribution-points). You can read, play with or adapt from these samples to create your own extensions.

You can expect from each sample:
- An explanation of its functionality
- A gif or screenshot demonstrating its usage
- Link to a guide on VS Code website, if it has one
- Listing of used VS Code API and Contribution Points
- Code of the same style, enforced using ESLint

## Prerequisites

You need to have [node](https://nodejs.org/en/) and [npm](https://nodejs.org/en/) installed on your system to run the examples. It is recommended to use the node version used for VS Code development itself which is documented [here](https://github.com/Microsoft/vscode/wiki/How-to-Contribute#prerequisites)

## Usage

- `git clone https://github.com/Microsoft/vscode-extension-samples`
- `code <any-sample-folder>`
- `npm install` in the terminal, then `F5` to run the sample
- Alternatively, follow the instructions in each sample's README for setting up and running the sample

## Getting Started

- [Hello World Sample](helloworld-sample): The Hello World sample for VS Code. See [Extension Anatomy](https://code.visualstudio.com/api/get-started/extension-anatomy) documentation.
- [Hello World Minimal Sample](helloworld-minimal-sample): A minimal version of Hello World Sample written in JavaScript.
- [Hello World Test Sample](helloworld-test-sample): Hello World sample with extension integration test. See [Testing Extensions](https://code.visualstudio.com/api/working-with-extensions/testing-extension) documentation.
- [Hello World Web Sample](helloworld-web-sample): The Hello World sample for VS Code Web. See the [Web Extensions](https://code.visualstudio.com/api/extension-guides/web-extensions) guide.

## Samples

<!-- SAMPLES_BEGIN -->
| Sample | Guide on VS Code Website | API & Contribution |
| ------ | ----- | --- |
| [Webview Sample](https://github.com/Microsoft/vscode-extension-samples/tree/main/webview-sample) | [/api/extension-guides/webview](https://code.visualstudio.com/api/extension-guides/webview) | [window.createWebviewPanel](https://code.visualstudio.com/api/references/vscode-api#window.createWebviewPanel)<br>[window.registerWebviewPanelSerializer](https://code.visualstudio.com/api/references/vscode-api#window.registerWebviewPanelSerializer) |
| [Webview View Sample](https://github.com/Microsoft/vscode-extension-samples/tree/main/webview-view-sample) | N/A | [window.registerWebviewViewProvider](https://code.visualstudio.com/api/references/vscode-api#window.registerWebviewViewProvider) |
| [Webview Codicons Sample](https://github.com/Microsoft/vscode-extension-samples/tree/main/webview-codicons-sample) | N/A |  |
| [Status Bar Sample](https://github.com/Microsoft/vscode-extension-samples/tree/main/statusbar-sample) | N/A | [window.createStatusBarItem](https://code.visualstudio.com/api/references/vscode-api#window.createStatusBarItem)<br>[StatusBarItem](https://code.visualstudio.com/api/references/vscode-api#StatusBarItem) |
| [Tree View Sample](https://github.com/Microsoft/vscode-extension-samples/tree/main/tree-view-sample) | [/api/extension-guides/tree-view](https://code.visualstudio.com/api/extension-guides/tree-view) | [window.createTreeView](https://code.visualstudio.com/api/references/vscode-api#window.createTreeView)<br>[window.registerTreeDataProvider](https://code.visualstudio.com/api/references/vscode-api#window.registerTreeDataProvider)<br>[TreeView](https://code.visualstudio.com/api/references/vscode-api#TreeView)<br>[TreeDataProvider](https://code.visualstudio.com/api/references/vscode-api#TreeDataProvider)<br>[contributes.views](https://code.visualstudio.com/api/references/contribution-points#contributes.views)<br>[contributes.viewsContainers](https://code.visualstudio.com/api/references/contribution-points#contributes.viewsContainers) |
| [Task Provider Sample](https://github.com/Microsoft/vscode-extension-samples/tree/main/task-provider-sample) | [/api/extension-guides/task-provider](https://code.visualstudio.com/api/extension-guides/task-provider) | [tasks.registerTaskProvider](https://code.visualstudio.com/api/references/vscode-api#tasks.registerTaskProvider)<br>[Task](https://code.visualstudio.com/api/references/vscode-api#Task)<br>[ShellExecution](https://code.visualstudio.com/api/references/vscode-api#ShellExecution)<br>[contributes.taskDefinitions](https://code.visualstudio.com/api/references/contribution-points#contributes.taskDefinitions) |
| [Multi Root Sample](https://github.com/Microsoft/vscode-extension-samples/tree/main/basic-multi-root-sample) | N/A | [workspace.getWorkspaceFolder](https://code.visualstudio.com/api/references/vscode-api#workspace.getWorkspaceFolder)<br>[workspace.onDidChangeWorkspaceFolders](https://code.visualstudio.com/api/references/vscode-api#workspace.onDidChangeWorkspaceFolders) |
| [Completion Provider Sample](https://github.com/Microsoft/vscode-extension-samples/tree/main/completions-sample) | N/A | [languages.registerCompletionItemProvider](https://code.visualstudio.com/api/references/vscode-api#languages.registerCompletionItemProvider)<br>[CompletionItem](https://code.visualstudio.com/api/references/vscode-api#CompletionItem)<br>[SnippetString](https://code.visualstudio.com/api/references/vscode-api#SnippetString) |
| [Code Actions Sample](https://github.com/Microsoft/vscode-extension-samples/tree/main/code-actions-sample) | N/A | [languages.registerCodeActionsProvider](https://code.visualstudio.com/api/references/vscode-api#languages.registerCodeActionsProvider)<br>[CodeActionProvider](https://code.visualstudio.com/api/references/vscode-api#CodeActionProvider) |
| [File System Provider Sample](https://github.com/Microsoft/vscode-extension-samples/tree/main/fsprovider-sample) | N/A | [workspace.registerFileSystemProvider](https://code.visualstudio.com/api/references/vscode-api#workspace.registerFileSystemProvider) |
| [Editor Decorator Sample](https://github.com/Microsoft/vscode-extension-samples/tree/main/decorator-sample) | N/A | [TextEditor.setDecorations](https://code.visualstudio.com/api/references/vscode-api#TextEditor.setDecorations)<br>[DecorationOptions](https://code.visualstudio.com/api/references/vscode-api#DecorationOptions)<br>[DecorationInstanceRenderOptions](https://code.visualstudio.com/api/references/vscode-api#DecorationInstanceRenderOptions)<br>[ThemableDecorationInstanceRenderOptions](https://code.visualstudio.com/api/references/vscode-api#ThemableDecorationInstanceRenderOptions)<br>[window.createTextEditorDecorationType](https://code.visualstudio.com/api/references/vscode-api#window.createTextEditorDecorationType)<br>[TextEditorDecorationType](https://code.visualstudio.com/api/references/vscode-api#TextEditorDecorationType)<br>[contributes.colors](https://code.visualstudio.com/api/references/contribution-points#contributes.colors) |
| [L10n Sample](https://github.com/Microsoft/vscode-extension-samples/tree/main/l10n-sample) | N/A |  |
| [Terminal Sample](https://github.com/Microsoft/vscode-extension-samples/tree/main/terminal-sample) | N/A | [window.createTerminal](https://code.visualstudio.com/api/references/vscode-api#window.createTerminal)<br>[window.onDidChangeActiveTerminal](https://code.visualstudio.com/api/references/vscode-api#window.onDidChangeActiveTerminal)<br>[window.onDidCloseTerminal](https://code.visualstudio.com/api/references/vscode-api#window.onDidCloseTerminal)<br>[window.onDidOpenTerminal](https://code.visualstudio.com/api/references/vscode-api#window.onDidOpenTerminal)<br>[window.Terminal](https://code.visualstudio.com/api/references/vscode-api#window.Terminal)<br>[window.terminals](https://code.visualstudio.com/api/references/vscode-api#window.terminals) |
| [Extension Terminal Sample](https://github.com/Microsoft/vscode-extension-samples/tree/main/extension-terminal-sample) | N/A | [window.createTerminal](https://code.visualstudio.com/api/references/vscode-api#window.createTerminal)<br>[window.Pseudoterminal](https://code.visualstudio.com/api/references/vscode-api#window.Pseudoterminal)<br>[window.ExtensionTerminalOptions](https://code.visualstudio.com/api/references/vscode-api#window.ExtensionTerminalOptions) |
| [Color Theme Sample](https://github.com/Microsoft/vscode-extension-samples/tree/main/theme-sample) | [/api/extension-guides/color-theme](https://code.visualstudio.com/api/extension-guides/color-theme) | [contributes.themes](https://code.visualstudio.com/api/references/contribution-points#contributes.themes) |
| [Product Icon Theme Sample](https://github.com/Microsoft/vscode-extension-samples/tree/main/product-icon-theme-sample) | [/api/extension-guides/product-icon-theme](https://code.visualstudio.com/api/extension-guides/product-icon-theme) | [contributes.productIconThemes](https://code.visualstudio.com/api/references/contribution-points#contributes.productIconThemes) |
| [Vim Sample](https://github.com/Microsoft/vscode-extension-samples/tree/main/vim-sample) | N/A | [commands](https://code.visualstudio.com/api/references/vscode-api#commands)<br>[StatusBarItem](https://code.visualstudio.com/api/references/vscode-api#StatusBarItem)<br>[window.createStatusBarItem](https://code.visualstudio.com/api/references/vscode-api#window.createStatusBarItem)<br>[TextEditorCursorStyle](https://code.visualstudio.com/api/references/vscode-api#TextEditorCursorStyle)<br>[window.activeTextEditor](https://code.visualstudio.com/api/references/vscode-api#window.activeTextEditor)<br>[Position](https://code.visualstudio.com/api/references/vscode-api#Position)<br>[Range](https://code.visualstudio.com/api/references/vscode-api#Range)<br>[Selection](https://code.visualstudio.com/api/references/vscode-api#Selection)<br>[TextEditor](https://code.visualstudio.com/api/references/vscode-api#TextEditor)<br>[TextEditorRevealType](https://code.visualstudio.com/api/references/vscode-api#TextEditorRevealType)<br>[TextDocument](https://code.visualstudio.com/api/references/vscode-api#TextDocument) |
| [webpack-sample](https://github.com/Microsoft/vscode-extension-samples/tree/main/webpack-sample) | [/api/working-with-extensions/bundling-extension](https://code.visualstudio.com/api/working-with-extensions/bundling-extension) |  |
| [esbuild-sample](https://github.com/Microsoft/vscode-extension-samples/tree/main/esbuild-sample) | [/api/working-with-extensions/bundling-extension](https://code.visualstudio.com/api/working-with-extensions/bundling-extension) |  |
| [Source Control Sample](https://github.com/Microsoft/vscode-extension-samples/tree/main/source-control-sample) | [/api/extension-guides/scm-provider](https://code.visualstudio.com/api/extension-guides/scm-provider) | [workspace.workspaceFolders](https://code.visualstudio.com/api/references/vscode-api#workspace.workspaceFolders)<br>[SourceControl](https://code.visualstudio.com/api/references/vscode-api#SourceControl)<br>[SourceControlResourceGroup](https://code.visualstudio.com/api/references/vscode-api#SourceControlResourceGroup)<br>[scm.createSourceControl](https://code.visualstudio.com/api/references/vscode-api#scm.createSourceControl)<br>[TextDocumentContentProvider](https://code.visualstudio.com/api/references/vscode-api#TextDocumentContentProvider)<br>[contributes.menus](https://code.visualstudio.com/api/references/contribution-points#contributes.menus) |
| [Commenting API Sample](https://github.com/Microsoft/vscode-extension-samples/tree/main/comment-sample) | N/A |  |
| [Document Editing Sample](https://github.com/Microsoft/vscode-extension-samples/tree/main/document-editing-sample) | N/A | [commands](https://code.visualstudio.com/api/references/vscode-api#commands) |
| [Custom Data Sample](https://github.com/Microsoft/vscode-extension-samples/tree/main/custom-data-sample) | [/api/extension-guides/custom-data-extension](https://code.visualstudio.com/api/extension-guides/custom-data-extension) |  |
| [CodeLens Provider Sample](https://github.com/Microsoft/vscode-extension-samples/tree/main/codelens-sample) | N/A | [languages.registerCodeLensProvider](https://code.visualstudio.com/api/references/vscode-api#languages.registerCodeLensProvider)<br>[CodeLensProvider](https://code.visualstudio.com/api/references/vscode-api#CodeLensProvider)<br>[CodeLens](https://code.visualstudio.com/api/references/vscode-api#CodeLens) |
| [Call Hierarchy Sample](https://github.com/Microsoft/vscode-extension-samples/tree/main/call-hierarchy-sample) | N/A | [languages.registerCallHierarchyProvider](https://code.visualstudio.com/api/references/vscode-api#languages.registerCallHierarchyProvider)<br>[CallHierarchyProvider](https://code.visualstudio.com/api/references/vscode-api#CallHierarchyProvider)<br>[CallHierarchyItem](https://code.visualstudio.com/api/references/vscode-api#CallHierarchyItem)<br>[CallHierarchyOutgoingCall](https://code.visualstudio.com/api/references/vscode-api#CallHierarchyOutgoingCall)<br>[CallHierarchyIncomingCall](https://code.visualstudio.com/api/references/vscode-api#CallHierarchyIncomingCall) |
| [Custom Editors Sample](https://github.com/Microsoft/vscode-extension-samples/tree/main/custom-editor-sample) | [/api/extension-guides/custom-editors](https://code.visualstudio.com/api/extension-guides/custom-editors) | [window.registerCustomEditorProvider](https://code.visualstudio.com/api/references/vscode-api#window.registerCustomEditorProvider)<br>[CustomTextEditorProvider](https://code.visualstudio.com/api/references/vscode-api#CustomTextEditorProvider)<br>[contributes.customEditors](https://code.visualstudio.com/api/references/contribution-points#contributes.customEditors) |
| [Semantic tokens](https://github.com/Microsoft/vscode-extension-samples/tree/main/semantic-tokens-sample) | [/api/language-extensions/semantic-highlight-guide](https://code.visualstudio.com/api/language-extensions/semantic-highlight-guide) | [languages.registerDocumentSemanticTokensProvider](https://code.visualstudio.com/api/references/vscode-api#languages.registerDocumentSemanticTokensProvider)<br>[vscode.DocumentSemanticTokensProvider](https://code.visualstudio.com/api/references/vscode-api#vscode.DocumentSemanticTokensProvider) |
| [Test Provider Sample](https://github.com/Microsoft/vscode-extension-samples/tree/main/test-provider-sample) | N/A |  |
| [Getting Started Sample](https://github.com/Microsoft/vscode-extension-samples/tree/main/getting-started-sample) | N/A |  |
| [notebook-renderer-sample](https://github.com/Microsoft/vscode-extension-samples/tree/main/notebook-renderer-sample) | [/api/extension-guides/notebook#notebook-renderer](https://code.visualstudio.com/api/extension-guides/notebook#notebook-renderer) | [contributes.notebookRenderer](https://code.visualstudio.com/api/references/contribution-points#contributes.notebookRenderer) |
| [notebook-extend-markdown-renderer-sample](https://github.com/Microsoft/vscode-extension-samples/tree/main/notebook-extend-markdown-renderer-sample) | [/api/extension-guides/notebook#notebook-renderer](https://code.visualstudio.com/api/extension-guides/notebook#notebook-renderer) | [contributes.notebookRenderer](https://code.visualstudio.com/api/references/contribution-points#contributes.notebookRenderer) |
| [jupyter-server-provider-sample](https://github.com/Microsoft/vscode-extension-samples/tree/main/jupyter-server-provider-sample) | N/A |  |
| [Chat Sample](https://github.com/Microsoft/vscode-extension-samples/tree/main/chat-sample) | N/A |  |
| [Chat Tutorial](https://github.com/Microsoft/vscode-extension-samples/tree/main/chat-tutorial) | N/A |  |
| [Notifications Sample](https://github.com/Microsoft/vscode-extension-samples/tree/main/notifications-sample) | N/A |  |
<!-- SAMPLES_END -->

### Language Server Protocol Samples

<!-- LSP_SAMPLES_BEGIN -->
| Sample | Guide on VS Code Website | API & Contribution |
| ------ | ----- | --- |
| [Snippet Sample](https://github.com/Microsoft/vscode-extension-samples/tree/main/snippet-sample) | [/api/language-extensions/snippet-guide](https://code.visualstudio.com/api/language-extensions/snippet-guide) | [contributes.snippets](https://code.visualstudio.com/api/references/contribution-points#contributes.snippets) |
| [Language Configuration Sample](https://github.com/Microsoft/vscode-extension-samples/tree/main/language-configuration-sample) | [/api/language-extensions/language-configuration-guide](https://code.visualstudio.com/api/language-extensions/language-configuration-guide) | [contributes.languages](https://code.visualstudio.com/api/references/contribution-points#contributes.languages) |
| [LSP Sample](https://github.com/Microsoft/vscode-extension-samples/tree/main/lsp-sample) | [/api/language-extensions/language-server-extension-guide](https://code.visualstudio.com/api/language-extensions/language-server-extension-guide) |  |
| [LSP Log Streaming Sample](https://github.com/Microsoft/vscode-extension-samples/tree/main/lsp-log-streaming-sample) | N/A |  |
| [LSP Multi Root Server Sample](https://github.com/Microsoft/vscode-extension-samples/tree/main/lsp-multi-server-sample) | https://github.com/Microsoft/vscode/wiki/Extension-Authoring:-Adopting-Multi-Root-Workspace-APIs#language-client--language-server |  |
| [LSP Web Extension Sample](https://github.com/Microsoft/vscode-extension-samples/tree/main/lsp-web-extension-sample) | [/api/language-extensions/language-server-extension-guide](https://code.visualstudio.com/api/language-extensions/language-server-extension-guide) |  |
| [LSP User Input Sample](https://github.com/Microsoft/vscode-extension-samples/tree/main/lsp-user-input-sample) | N/A |  |
| [LSP Embedded Language Service](https://github.com/Microsoft/vscode-extension-samples/tree/main/lsp-embedded-language-service) | N/A |  |
| [LSP Embedded Request Forwarding](https://github.com/Microsoft/vscode-extension-samples/tree/main/lsp-embedded-request-forwarding) | N/A |  |
| [Wasm language server](https://github.com/Microsoft/vscode-extension-samples/tree/main/wasm-language-server) | N/A |  |
<!-- LSP_SAMPLES_END -->

## License

Copyright (c) Microsoft Corporation. All rights reserved.

Licensed under the [MIT](https://github.com/microsoft/vscode-extension-samples/blob/main/LICENSE) License.
