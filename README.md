<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Building and Testing Node.js</title>
</head>
<body>
    <h1>Building and Testing Node.js</h1>
    <p>You can create a continuous integration (CI) workflow to build and test your Node.js project.</p>

    <h2>Introduction</h2>
    <p>This guide shows you how to create a continuous integration (CI) workflow that builds and tests Node.js code. If your CI tests pass, you may want to deploy your code or publish a package.</p>

    <h2>Prerequisites</h2>
    <p>We recommend that you have a basic understanding of Node.js, YAML, workflow configuration options, and how to create a workflow file. For more information, see:</p>
    <ul>
        <li><a href="#">"Writing workflows"</a></li>
        <li><a href="#">"Getting started with Node.js"</a></li>
    </ul>

    <h3>Using a Node.js Workflow Template</h3>
    <p>To get started quickly, add a workflow template to the <code>.github/workflows</code> directory of your repository.</p>
    <p>GitHub provides a workflow template for Node.js that should work for most Node.js projects. The subsequent sections of this guide give examples of how you can customize this workflow template.</p>

    <ol>
        <li>On GitHub, navigate to the main page of the repository.</li>
        <li>Under your repository name, click <strong>Actions</strong>.</li>
        <li>If you already have a workflow in your repository, click <strong>New workflow</strong>.</li>
        <li>The "Choose a workflow" page shows a selection of recommended workflow templates. Search for "Node.js".</li>
        <li>Filter the selection of workflows by clicking <strong>Continuous integration</strong>.</li>
        <li>On the "Node.js" workflow, click <strong>Configure</strong>.</li>
        <li>Edit the workflow as required. For example, change the Node versions you want to use.</li>
        <li>Click <strong>Commit changes</strong>.</li>
    </ol>
    <p>The <code>node.js.yml</code> workflow file is added to the <code>.github/workflows</code> directory of your repository.</p>

    <h3>Specifying the Node.js Version</h3>
    <p>The easiest way to specify a Node.js version is by using the <code>setup-node</code> action provided by GitHub. For more information see, <a href="#">setup-node</a>.</p>

    <pre><code>YAML
strategy:
  matrix:
    node-version: ['18.x', '20.x']
steps:
- uses: actions/checkout@v4
- name: Use Node.js ${{ matrix.node-version }}
  uses: actions/setup-node@v4
  with:
    node-version: ${{ matrix.node-version }}
</code></pre>

    <h2>Installing Dependencies</h2>
    <p>GitHub-hosted runners have npm and Yarn dependency managers installed. You can use npm and Yarn to install dependencies in your workflow before building and testing your code.</p>

    <h3>Example Using npm</h3>
    <pre><code>YAML
steps:
- uses: actions/checkout@v4
- name: Use Node.js
  uses: actions/setup-node@v4
  with:
    node-version: '20.x'
- name: Install dependencies
  run: npm ci
</code></pre>

    <h3>Example Using Yarn</h3>
    <pre><code>YAML
steps:
- uses: actions/checkout@v4
- name: Use Node.js
  uses: actions/setup-node@v4
  with:
    node-version: '20.x'
- name: Install dependencies
  run: yarn --frozen-lockfile
</code></pre>

    <h2>Building and Testing Your Code</h2>
    <p>You can use the same commands that you use locally to build and test your code.</p>
    <pre><code>YAML
steps:
- uses: actions/checkout@v4
- name: Use Node.js
  uses: actions/setup-node@v4
  with:
    node-version: '20.x'
- run: npm install
- run: npm run build --if-present
- run: npm test
</code></pre>
</body>
</html>
