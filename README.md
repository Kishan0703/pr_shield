# 🛡️ LGTM (Looks Good To Me) - AI-Powered PR Review Platform

LGTM is a full-stack, AI-powered Pull Request review platform and security watchdog. It seamlessly integrates with GitHub to provide automated, context-aware code reviews and security scans directly in your development workflow.

## 🌟 Key Features

- **🤖 AI-Powered Code Reviews**: Uses advanced LLMs (OpenAI, Anthropic, Gemini) to analyze PRs and provide actionable feedback.
- **🌳 Context-Aware Indexing**: Leverages AST (Abstract Syntax Trees) via Tree-sitter to understand repository context.
- **🔒 Security Watchdog**: Scans for vulnerabilities and includes a custom GitHub Action to gate CI/CD pipelines based on security findings.
- **⚡ Real-time Dashboard**: A rich web interface for monitoring repo health, commit diffs, review feeds, and analytics.
- **💳 Payment Integration**: Powered by Dodo Payments for SaaS billing.

## 🏗️ Platform Architecture

The repository is structured as a monorepo containing three main components:

- `/client`: A React-based single-page application built with Vite and TailwindCSS.
- `/server`: An Express/Node.js API backend that handles GitHub Webhooks, background processing (via BullMQ/Redis), and Socket.io for real-time client updates.
- `/lgtm-action`: A GitHub Action that halts CI runs if LGTM Security flags blocking issues.

## 💻 Tech Stack

**Frontend (Client)**
- React 19, TypeScript, Vite
- TailwindCSS, PostCSS
- React Router, Zustand (State Management)
- Recharts (Analytics), Socket.IO Client

**Backend (Server)**
- Node.js, Express, TypeScript
- MongoDB (Mongoose), Redis (ioredis), BullMQ (Background Jobs)
- Tree-sitter (Multi-language AST Parsing)
- AI SDKs: `@anthropic-ai/sdk`, `@google/generative-ai`, `openai`
- Dodo Payments, Octokit (GitHub API), Sentry

## 🚀 Getting Started

### Prerequisites

- Node.js (v20+ recommended)
- MongoDB instance (local or Atlas)
- Redis instance (local or Upstash/Redis Labs)
- GitHub App credentials

### Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/Kishan0703/pr_shield.git
   cd pr_shield
   ```

2. Install backend dependencies:
   ```bash
   cd server
   npm install
   ```

3. Install frontend dependencies:
   ```bash
   cd ../client
   npm install
   ```

### Configuration

#### Server
Create a `.env` file in the `server` directory (use `.env.example` as a template):
```env
PORT=3000
MONGODB_URI=mongodb://localhost:27017/lgtm
REDIS_URL=redis://localhost:6379
# Add your GitHub App and API keys here
```

#### Client
Create a `.env` file in the `client` directory:
```env
VITE_API_URL=http://localhost:3000
VITE_SOCKET_URL=http://localhost:3000
VITE_DODO_ENV=test
```

### Running Locally

You will need to run both the client and server concurrently.

**Start the Server:**
```bash
cd server
npm run dev
```

**Start the Client:**
```bash
cd client
npm run dev
```

## ⚙️ Background Workers

The server utilizes BullMQ and Redis for heavy lifting, split across three primary background jobs:
1. **Context Worker**: Parses code using Tree-sitter to build a searchable AST context of the repository.
2. **Review Worker**: Evaluates PRs using configured AI models and posts feedback directly to GitHub.
3. **Security Worker**: Scans the codebase for potential vulnerabilities and enforces security policies.

## 🛡️ GitHub Action Integration

LGTM includes a native GitHub Action (`lgtm-action`) to integrate security gates directly into your CI pipeline. 
See the [LGTM Security Watchdog Action README](./lgtm-action/README.md) for usage instructions.

## 📝 License

This project is licensed under the MIT License.


