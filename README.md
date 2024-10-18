[![Bolt.new: AI-Powered Full-Stack Web Development in the Browser](./public/social_preview_index.jpg)](https://bolt.new)

# Bolt.new Fork by Syndicate604

This fork of bolt.new allows you to choose the LLM that you use for each prompt! Currently you can use OpenAI, Anthropic, Ollama, or Groq models - and it is easily extended to use any other model supported by the Vercel AI SDK! See instructions below for running this locally and extending to include more models.

# Bolt.new: AI-Powered Full-Stack Web Development in the Browser

Bolt.new is an AI-powered web development agent that allows you to prompt, run, edit, and deploy full-stack applications directly from your browser—no local setup required. If you're here to build your own AI-powered web dev agent using the Bolt open source codebase, [click here to get started!](./CONTRIBUTING.md)

## What Makes Bolt.new Different

Claude, v0, etc are incredible- but you can't install packages, run backends or edit code. That’s where Bolt.new stands out:

- **Full-Stack in the Browser**: Bolt.new integrates cutting-edge AI models with an in-browser development environment powered by **StackBlitz’s WebContainers**. This allows you to:
  - Install and run npm tools and libraries (like Vite, Next.js, and more)
  - Run Node.js servers
  - Interact with third-party APIs
  - Deploy to production from chat
  - Share your work via a URL

- **AI with Environment Control**: Unlike traditional dev environments where the AI can only assist in code generation, Bolt.new gives AI models **complete control** over the entire  environment including the filesystem, node server, package manager, terminal, and browser console. This empowers AI agents to handle the entire app lifecycle—from creation to deployment.

Whether you’re an experienced developer, a PM or designer, Bolt.new allows you to build production-grade full-stack applications with ease.

For developers interested in building their own AI-powered development tools with WebContainers, check out the open-source Bolt codebase in this repo!

## Prerequisites

Before you begin, ensure you have the following installed:

- Node.js (v20.15.1)
- npm (v9.4.0)

## Setup

1. Clone the repository (if you haven't already):

```bash
git clone [https://github.com/syndicate604/bolt.new-open-llm/]
```

2. Install dependencies:

```bash
npm install
```

3. Rename `.env.example` to .env.local and add your LLM API keys (you only have to set the ones you want to use and Ollama doesn't need an API key because it runs locally on your computer):

```
GROQ_API_KEY=XXX
OPENAI_API_KEY=XXX
ANTHROPIC_API_KEY=XXX
```

Optionally, you can set the debug level:

```
VITE_LOG_LEVEL=debug
```

**Important**: Never commit your `.env.local` file to version control. It's already included in .gitignore.

## Adding New LLMs:

To make new LLMs available to use in this version of Bolt.new, head on over to `app/utils/constants.ts` and find the constant MODEL_LIST. Each element in this array is an object that has the model ID for the name (get this from the provider's API documentation), a lable for the frontend model dropdown, and the provider. 

By default, Anthropic, OpenAI, Groq, and Ollama are implemented as providers, but the YouTube video for this repo covers how to extend this to work with more providers if you wish!

When you add a new model to the MODEL_LIST array, it will immediately be available to use when you run the app locally or reload it. For Ollama models, make sure you have the model installed already before trying to use it here!

## Available Scripts

- `npm run dev`: Starts the development server.
- `npm run build`: Builds the project.
- `npm run start`: Runs the built application locally using Wrangler Pages. This script uses `bindings.sh` to set up necessary bindings so you don't have to duplicate environment variables.
- `npm run preview`: Builds the project and then starts it locally, useful for testing the production build. Note, HTTP streaming currently doesn't work as expected with `wrangler pages dev`.
- `npm test`: Runs the test suite using Vitest.
- `npm run typecheck`: Runs TypeScript type checking.
- `npm run typegen`: Generates TypeScript types using Wrangler.
- `npm run deploy`: Builds the project and deploys it to Cloudflare Pages.

## Running Bolt

Everytime you change the MODELS you need to run 'npm run build' or the models will not change.  
'npm run dev' will not work without Google Canary so instead run 'npm run start' this will run the full Bolt in Linux Chrome with Vite.

```bash
npm run build
npm run start 
```

This will first rebuild and then start the Vite server. You will need Google Chrome Canary for DEV only (WINDOWS/MAC), to run this locally! It's a very easy install and a good browser for web development anyway. Otherwise just run the program. 

## Tips and Tricks

Here are some tips to get the most out of Bolt.new:

- **Be specific about your stack**: If you want to use specific frameworks or libraries (like Astro, Tailwind, ShadCN, or any other popular JavaScript framework), mention them in your initial prompt to ensure Bolt scaffolds the project accordingly.

- **Use the enhance prompt icon**: Before sending your prompt, try clicking the 'enhance' icon to have the AI model help you refine your prompt, then edit the results before submitting.

- **Scaffold the basics first, then add features**: Make sure the basic structure of your application is in place before diving into more advanced functionality. This helps Bolt understand the foundation of your project and ensure everything is wired up right before building out more advanced functionality.

- **Batch simple instructions**: Save time by combining simple instructions into one message. For example, you can ask Bolt to change the color scheme, add mobile responsiveness, and restart the dev server, all in one go saving you time and reducing API credit consumption significantly.
