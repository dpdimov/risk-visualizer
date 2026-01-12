# Startup Risk Visualizer - Deployment Instructions

## Project Overview

A React-based interactive teaching tool for Entrepreneurial Finance that visualizes multiplicative startup risk across 9 milestones, mapping to a framework of 4 Assessment Criteria (Opportunity, Scalability, Execution, Return) and 4 Business Models (Revenue, Cost, Cash, Investment).

## The 9-Milestone Framework

| # | Milestone | Risk % | Months | Assessment | Model |
|---|-----------|--------|--------|------------|-------|
| 1 | Problem-Solution Fit | 40% | 6 | Opportunity | Discovery |
| 2 | Team Assembly | 35% | 6 | Execution | Foundation |
| 3 | Technology Readiness | 30% | 12 | Execution | Pre-product |
| 4 | Product Development | 25% | 9 | Execution | Cost Model |
| 5 | Product-Market Fit | 22% | 12 | Opportunity | Revenue Model |
| 6 | Unit Economics Validation | 18% | 9 | Scalability | Cost Model |
| 7 | Scalable Growth | 15% | 9 | Scalability | Revenue Model |
| 8 | Favorable Capital Structure | 15% | 6 | Return | Investment Model |
| 9 | Cash Flow Positive | 12% | 12 | Execution | Cash Model |

## Tech Stack

- React 18
- Recharts (for visualizations)
- Inline CSS (no external stylesheets needed)

## Deployment Option 1: Vercel (Recommended)

### Step 1: Create Project Structure

```bash
mkdir risk-visualizer
cd risk-visualizer
npm create vite@latest . -- --template react
```

### Step 2: Install Dependencies

```bash
npm install recharts
```

### Step 3: Replace Files

Replace `src/App.jsx` with the contents of `risk-visualizer.jsx`

Update `src/App.jsx` to have proper default export:
```jsx
// Copy entire contents of risk-visualizer.jsx here
// The component is already named StartupRiskVisualizer with default export
```

Update `src/main.jsx`:
```jsx
import React from 'react'
import ReactDOM from 'react-dom/client'
import StartupRiskVisualizer from './App'

ReactDOM.createRoot(document.getElementById('root')).render(
  <React.StrictMode>
    <StartupRiskVisualizer />
  </React.StrictMode>,
)
```

Update `index.html` title:
```html
<title>Startup Risk Visualizer | Entrepreneurial Finance</title>
```

### Step 4: Test Locally

```bash
npm run dev
```

### Step 5: Deploy to Vercel

```bash
npm install -g vercel
vercel login
vercel
```

Follow prompts. Vercel auto-detects Vite and configures everything.

### Step 6: Custom Domain (Optional)

In Vercel dashboard → Project → Settings → Domains → Add your domain

---

## Deployment Option 2: GitHub Pages

### Step 1: Create Project with Vite

```bash
mkdir risk-visualizer
cd risk-visualizer
npm create vite@latest . -- --template react
npm install recharts
```

### Step 2: Configure for GitHub Pages

Update `vite.config.js`:
```js
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'

export default defineConfig({
  plugins: [react()],
  base: '/risk-visualizer/', // Must match repo name
})
```

### Step 3: Add GitHub Actions Workflow

Create `.github/workflows/deploy.yml`:
```yaml
name: Deploy to GitHub Pages

on:
  push:
    branches: ['main']
  workflow_dispatch:

permissions:
  contents: read
  pages: write
  id-token: write

concurrency:
  group: 'pages'
  cancel-in-progress: true

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4
      - name: Setup Node
        uses: actions/setup-node@v4
        with:
          node-version: 20
          cache: 'npm'
      - name: Install dependencies
        run: npm ci
      - name: Build
        run: npm run build
      - name: Setup Pages
        uses: actions/configure-pages@v4
      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: './dist'
  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    needs: build
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
```

### Step 4: Enable GitHub Pages

In repo Settings → Pages → Source: GitHub Actions

### Step 5: Push to GitHub

```bash
git init
git add .
git commit -m "Initial commit"
git remote add origin https://github.com/YOUR_USERNAME/risk-visualizer.git
git push -u origin main
```

---

## Quick Start for Claude Code

Copy and run this sequence:

```bash
# Create and setup project
mkdir risk-visualizer && cd risk-visualizer
npm create vite@latest . -- --template react
npm install recharts

# The main component file will be provided - copy to src/App.jsx

# Test locally
npm run dev

# Deploy to Vercel
npx vercel
```

---

## Features Summary

### Journey View
- Area chart showing composite risk and success probability progression
- Interactive milestone selection with detailed info panel
- Timeline summary showing total journey and time remaining

### Framework View
- 4 Assessment Criteria cards (Opportunity, Scalability, Execution, Return)
- 4 Business Models section (Revenue, Cost, Cash, Investment)
- Visual progress tracking per category
- Click-through to milestone details

### Interactive Controls
- Toggle milestone achievement (checkbox)
- Adjust risk percentage per milestone (slider: 5-60%)
- Adjust duration per milestone (input: 1-36 months)
- Show/hide formulas toggle

### Calculated Metrics
- Composite Risk: 1 - ∏(1 - rᵢ)
- Success Probability: 1 - Composite Risk
- Required Multiple: 1 / P(success)
- Required IRR: (Multiple)^(1/years) - 1

### Investment Implications Panel
- Current stage assessment
- Milestones achieved counter
- Typical funding stage indicator

---

## File Structure After Setup

```
risk-visualizer/
├── index.html
├── package.json
├── vite.config.js
├── src/
│   ├── App.jsx          ← Main component (risk-visualizer.jsx)
│   └── main.jsx         ← Entry point
└── .github/
    └── workflows/
        └── deploy.yml   ← Only if using GitHub Pages
```

---

## Environment

- Node.js 18+ required
- Works in all modern browsers
- Responsive but optimized for desktop/tablet (teaching context)

---

## University of Bath Branding (Optional)

To add institutional branding, update the footer section in the component and optionally add a logo import.
