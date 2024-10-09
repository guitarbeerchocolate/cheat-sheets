# Vercel Cheat Sheet

## General Overview

- **Vercel** is a cloud platform designed for frontend frameworks and static sites, allowing easy and seamless deployment of applications.
- Supports popular frameworks like **Next.js**, **React**, **Vue.js**, **Svelte**, and more.
- Provides automatic **CI/CD** integration, enabling fast deployments directly from GitHub, GitLab, or Bitbucket.

---

## Basic Workflow

1. **Project Setup**

   - Install the **Vercel CLI** globally:
     ```bash
     npm install -g vercel
     ```
   - Initialize a project:
     ```bash
     vercel init
     ```
   - Link an existing project to Vercel:
     ```bash
     vercel link
     ```
   - Deploy your project:
     ```bash
     vercel
     ```
     Vercel will automatically detect the framework and set up the necessary build configuration.

2. **Connecting Git**
   - Link your repository from GitHub, GitLab, or Bitbucket for automatic deployments:
     - Go to the **Vercel Dashboard**.
     - Click "Import Project" and select the Git provider.
     - Choose the repository to link.
     - Automatic deployments will occur on every `push` to the main branch (or any branch you configure).

---

## Vercel CLI Commands

| Command                | Description                                                 |
| ---------------------- | ----------------------------------------------------------- |
| `vercel`               | Deploy the project interactively.                           |
| `vercel --prod`        | Deploy the project to production.                           |
| `vercel --prebuilt`    | Deploy a prebuilt output without running the build command. |
| `vercel dev`           | Start a local development server.                           |
| `vercel env add`       | Add environment variables (e.g., for API keys).             |
| `vercel env pull`      | Download environment variables to a `.env` file.            |
| `vercel logs [url]`    | View deployment logs.                                       |
| `vercel inspect [url]` | Inspect a deployment.                                       |
| `vercel --token`       | Authenticate using a Vercel token (for CI/CD).              |

---

## Configuration (vercel.json)

- You can add a `vercel.json` file in the root of your project to configure:
  - **Build settings**
  - **Redirects/Rewrites**
  - **Headers**
  - **Environment variables**

Example configuration for redirects and environment variables:

```json
{
  "redirects": [
    { "source": "/old-url", "destination": "/new-url", "permanent": true }
  ],
  "rewrites": [
    { "source": "/api/:path*", "destination": "https://api.example.com/:path*" }
  ],
  "env": {
    "NEXT_PUBLIC_API_URL": "https://api.example.com"
  }
}
```

---

## Environment Variables

1. **Setting environment variables** via CLI:

   ```bash
   vercel env add <type> <key>
   ```

   - Replace `<type>` with `production`, `preview`, or `development`.
   - Replace `<key>` with the variable name.

2. **Fetching environment variables**:
   ```bash
   vercel env pull .env
   ```

---

## Custom Domains

- Add custom domains via the dashboard or CLI:
  ```bash
  vercel domains add yourdomain.com
  ```
- To remove a domain:
  ```bash
  vercel domains remove yourdomain.com
  ```

---

## Deployments

1. **Preview Deployments**

   - Every branch or pull request (PR) gets its own preview URL (e.g., `branch-name.vercel.app`).
   - Preview deployments are useful for testing before merging changes to production.

2. **Production Deployments**
   - To push changes to the live site, deploy to the `main` branch, or use:
     ```bash
     vercel --prod
     ```

---

## Logs and Monitoring

1. **Deployment Logs**

   - Access logs via CLI:
     ```bash
     vercel logs <deployment-url>
     ```
   - Or view logs directly in the **Vercel Dashboard** under each deployment.

2. **Monitoring**
   - Vercel offers insights such as **performance metrics** (Lighthouse scores) for each deployment.
   - Use the dashboard to monitor **real-time performance** and **traffic**.

---

## Serverless Functions

- **Vercel** allows you to deploy **Serverless Functions** as API endpoints.
- Create a directory called `api/` in your project, and add `.js`, `.ts`, or `.go` files for each function:

  ```bash
  /api/hello.js
  ```

  Example `hello.js` function:

  ```javascript
  export default function handler(req, res) {
    res.status(200).json({ message: "Hello from Vercel!" });
  }
  ```

- The endpoint will be available at `https://your-project.vercel.app/api/hello`.

---

## Vercel Analytics

- Vercel Analytics provides privacy-focused web analytics without cookies.
- Enables you to track real-time user visits, page load times, and errors.
- You can enable it from the **dashboard** for specific projects.

---

## Integrations

- Vercel integrates with a wide variety of services:
  - **GitHub Actions**, **Slack notifications**, **Sentry** (for error tracking), **Datadog**, etc.
- You can manage integrations from the **Vercel Dashboard** under the **Integrations** tab.

---

## Useful Links

- [Vercel Documentation](https://vercel.com/docs)
- [Vercel CLI](https://vercel.com/docs/cli)
- [Vercel Dashboard](https://vercel.com/dashboard)

---
