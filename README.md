# Ayushman013-amp
Hi, I'm **Ayushman013-amp**. 
<p align="center">
  <picture>
    <source media="(prefers-color-scheme: light)" srcset="https://www.gitskins.com/api/section/hero?username=Ayushman013-amp&theme=neon&mode=light" />
    <img src="https://www.gitskins.com/api/section/hero?username=Ayushman013-amp&theme=neon" alt="Ayushman013-amp hero section" />
  </picture>
</p>
## About Me
Shapes the short profile story and positioning.
<p align="center">
  <picture>
    <source media="(prefers-color-scheme: light)" srcset="https://www.gitskins.com/api/section/about?username=Ayushman013-amp&theme=neon&mode=light" />
    <img src="https://www.gitskins.com/api/section/about?username=Ayushman013-amp&theme=neon" alt="Ayushman013-amp about section" />
  </picture>
</p>
## Skills
Selected stack and skill badges will be generated from the GitHub profile and README strategy.
<p align="center">
  <picture>
    <source media="(prefers-color-scheme: light)" srcset="https://www.gitskins.com/api/section/stack?username=Ayushman013-amp&theme=neon&mode=light" />
    <img src="https://www.gitskins.com/api/section/stack?username=Ayushman013-amp&theme=neon" alt="Ayushman013-amp stack section" />
  </picture>
</p>
## GitHub Stats
<p align="center">
  <picture>
    <source media="(prefers-color-scheme: light)" srcset="https://www.gitskins.com/api/section/stats?username=Ayushman013-amp&theme=neon&mode=light" />
    <img src="https://www.gitskins.com/api/section/stats?username=Ayushman013-amp&theme=neon" alt="Ayushman013-amp stats section" />
  </picture>
</p>
## Projects
Highlights repositories as proof of work.
<p align="center">
  <picture>
    <source media="(prefers-color-scheme: light)" srcset="https://www.gitskins.com/api/section/projects?username=Ayushman013-amp&theme=neon&mode=light" />
    <img src="https://www.gitskins.com/api/section/projects?username=Ayushman013-amp&theme=neon" alt="Ayushman013-amp projects section" />
  </picture>
</p>
## Connect
Contact and social links will appear here.
<p align="center">
  <picture>
    <source media="(prefers-color-scheme: light)" srcset="https://www.gitskins.com/api/section/social?username=Ayushman013-amp&theme=neon&mode=light" />
    <img src="https://www.gitskins.com/api/section/social?username=Ayushman013-amp&theme=neon" alt="Ayushman013-amp social section" />
  </picture>
</p>
github-space-shooter/
├── .github/
│   └── workflows/
│       └── update-space-shooter.yml
├── assets/
│   └── space-shooter.svg
├── src/
│   └── generate.js
├── package.json
├── README.md
└── LICENSE


============================================================
FILE: package.json
============================================================

{
  "name": "ayushman-github-space-shooter",
  "version": "1.0.0",
  "description": "Animated GitHub contribution space shooter",
  "type": "module",
  "scripts": {
    "generate": "node src/generate.js"
  },
  "engines": {
    "node": ">=20"
  }
}


============================================================
FILE: src/generate.js
============================================================

import fs from "node:fs";
import path from "node:path";

const USERNAME = "Ayushman013-amp";
const TOKEN = process.env.GITHUB_TOKEN;

if (!TOKEN) {
  throw new Error("GITHUB_TOKEN is required.");
}

const query = `
query($login: String!) {
  user(login: $login) {
    contributionsCollection {
      contributionCalendar {
        totalContributions
        weeks {
          contributionDays {
            date
            contributionCount
            contributionLevel
          }
        }
      }
    }
  }
}
`;

async function getContributions() {
  const response = await fetch(
    "https://api.github.com/graphql",
    {
      method: "POST",
      headers: {
        Authorization: `Bearer ${TOKEN}`,
        "Content-Type": "application/json",
        "User-Agent": "Ayushman013-amp-space-shooter"
      },
      body: JSON.stringify({
        query,
        variables: {
          login: USERNAME
        }
      })
    }
  );

  if (!response.ok) {
    throw new Error(`GitHub API error: ${response.status}`);
  }

  const data = await response.json();

  if (data.errors) {
    throw new Error(JSON.stringify(data.errors));
  }

  return data.data.user.contributionsCollection
    .contributionCalendar;
}

function escapeXml(value) {
  return String(value)
    .replaceAll("&", "&amp;")
    .replaceAll("<", "&lt;")
    .replaceAll(">", "&gt;")
    .replaceAll('"', "&quot;")
    .replaceAll("'", "&apos;");
}

function random(seed) {
  const x =
    Math.sin(seed * 9999.91) * 43758.5453;

  return x - Math.floor(x);
}

function contributionColor(level) {
  switch (level) {
    case "FOURTH_QUARTILE":
      return "#39ff88";

    case "THIRD_QUARTILE":
      return "#18c96b";

    case "SECOND_QUARTILE":
      return "#087f48";

    case "FIRST_QUARTILE":
      return "#06452d";

    default:
      return "#07131a";
  }
}

function createStars(width, height) {
  let output = "";

  for (let i = 0; i < 100; i++) {
    const x =
      Math.floor(random(i + 1) * width);

    const y =
      Math.floor(random(i + 100) * height);

    const radius =
      random(i + 200) > 0.85 ? 1.5 : 0.7;

    const duration =
      2 + random(i + 500) * 4;

    const delay =
      random(i + 300) * 5;

    output += `
      <circle
        cx="${x}"
        cy="${y}"
        r="${radius}"
        fill="#ffffff"
        opacity="0.65">

        <animate
          attributeName="opacity"
          values="0.1;1;0.1"
          dur="${duration.toFixed(2)}s"
          begin="${delay.toFixed(2)}s"
          repeatCount="indefinite"/>

      </circle>
    `;
  }

  return output;
}

function createAsteroids(count, width, height) {
  let output = "";

  for (let i = 0; i < count; i++) {
    const x =
      30 + random(i + 700) * (width - 60);

    const y =
      55 + random(i + 800) * (height - 100);

    const size =
      3 + random(i + 900) * 7;

    const duration =
      8 + random(i + 1000) * 8;

    output += `
      <g opacity="0.5">

        <path
          d="
            M ${x} ${y - size}
            L ${x + size} ${y - size / 3}
            L ${x + size / 2} ${y + size}
            L ${x - size / 2} ${y + size}
            L ${x - size} ${y}
            Z
          "
          fill="#59656d"
          stroke="#8d9ba3"
          stroke-width="1">

          <animateTransform
            attributeName="transform"
            type="rotate"
            from="0 ${x} ${y}"
            to="360 ${x} ${y}"
            dur="${duration}s"
            repeatCount="indefinite"/>

        </path>

      </g>
    `;
  }

  return output;
}

function createContributionGrid(days) {
  const startX = 42;
  const startY = 78;

  const cell = 9;
  const gap = 2;

  let output = "";

  days.forEach((day, index) => {
    const week = Math.floor(index / 7);
    const weekday = index % 7;

    const x =
      startX + week * (cell + gap);

    const y =
      startY + weekday * (cell + gap);

    const color =
      contributionColor(day.contributionLevel);

    output += `
      <rect
        x="${x}"
        y="${y}"
        width="${cell}"
        height="${cell}"
        rx="2"
        fill="${color}"
        stroke="#10232c"
        stroke-width="0.5">

        <title>
          ${escapeXml(day.date)} —
          ${day.contributionCount} contributions
        </title>

        <animate
          attributeName="opacity"
          values="0.55;1;0.55"
          dur="${3 + (index % 5)}s"
          begin="${(index % 12) * 0.15}s"
          repeatCount="indefinite"/>

      </rect>
    `;
  });

  return output;
}

function createEnemyShips(days) {
  let output = "";

  const activeDays =
    days.filter(
      day => day.contributionCount > 0
    );

  activeDays.forEach((day, index) => {
    if (index % 4 !== 0) return;

    const originalIndex =
      days.indexOf(day);

    const week =
      Math.floor(originalIndex / 7);

    const x =
      42 + week * 11;

    const y =
      165 + (index % 6) * 10;

    const duration =
      4 + (index % 5);

    output += `
      <g>

        <g
          transform="
            translate(${x} ${y})
            scale(0.55)
          ">

          <path
            d="
              M0 -10
              L8 7
              L0 3
              L-8 7
              Z
            "
            fill="#ff4d91"
            stroke="#ffffff"
            stroke-width="1">

            <animateTransform
              attributeName="transform"
              type="translate"
              values="0 0;5 -7;0 0"
              dur="${duration}s"
              repeatCount="indefinite"/>

          </path>

          <circle
            cx="0"
            cy="-1"
            r="2.5"
            fill="#ffffff"/>

        </g>

      </g>
    `;
  });

  return output;
}

function createPlayerShip(width, height) {
  return `
    <g>

      <animateTransform
        attributeName="transform"
        type="translate"
        values="
          0 0;
          15 -3;
          0 2;
          -15 -2;
          0 0
        "
        dur="5s"
        repeatCount="indefinite"/>

      <g
        transform="
          translate(
            ${width / 2}
            ${height - 42}
          )
        ">

        <path
          d="
            M0 -30
            L18 20
            L0 12
            L-18 20
            Z
          "
          fill="#61f4ff"
          stroke="#d9ffff"
          stroke-width="2"/>

        <path
          d="
            M0 -20
            L7 6
            L-7 6
            Z
          "
          fill="#162d39"/>

        <circle
          cx="0"
          cy="-7"
          r="4"
          fill="#ffffff">

          <animate
            attributeName="r"
            values="3;5;3"
            dur="1s"
            repeatCount="indefinite"/>

        </circle>

        <path
          d="
            M-7 14
            L0 35
            L7 14
          "
          fill="#ff9d42">

          <animate
            attributeName="d"
            values="
              M-7 14 L0 35 L7 14;
              M-7 14 L0 45 L7 14;
              M-7 14 L0 35 L7 14
            "
            dur="0.35s"
            repeatCount="indefinite"/>

        </path>

      </g>

    </g>
  `;
}

function createLasers() {
  return `
    <g>

      <rect
        x="120"
        y="205"
        width="3"
        height="55"
        rx="2"
        fill="#62ffb0"
        opacity="0">

        <animate
          attributeName="y"
          values="205;70"
          dur="1.5s"
          repeatCount="indefinite"/>

        <animate
          attributeName="opacity"
          values="0;1;1;0"
          dur="1.5s"
          repeatCount="indefinite"/>

      </rect>

      <rect
        x="360"
        y="205"
        width="3"
        height="55"
        rx="2"
        fill="#62ffb0"
        opacity="0">

        <animate
          attributeName="y"
          values="205;70"
          dur="1.8s"
          begin="0.5s"
          repeatCount="indefinite"/>

        <animate
          attributeName="opacity"
          values="0;1;1;0"
          dur="1.8s"
          begin="0.5s"
          repeatCount="indefinite"/>

      </rect>

      <rect
        x="650"
        y="205"
        width="3"
        height="55"
        rx="2"
        fill="#62ffb0"
        opacity="0">

        <animate
          attributeName="y"
          values="205;70"
          dur="2s"
          begin="1s"
          repeatCount="indefinite"/>

        <animate
          attributeName="opacity"
          values="0;1;1;0"
          dur="2s"
          begin="1s"
          repeatCount="indefinite"/>

      </rect>

    </g>
  `;
}

function createExplosion(x, y, delay) {
  return `
    <g
      transform="
        translate(${x} ${y})
      ">

      <circle
        cx="0"
        cy="0"
        r="3"
        fill="#ffffff"
        opacity="0">

        <animate
          attributeName="r"
          values="2;18;30"
          dur="1.5s"
          begin="${delay}s"
          repeatCount="indefinite"/>

        <animate
          attributeName="opacity"
          values="1;0.8;0"
          dur="1.5s"
          begin="${delay}s"
          repeatCount="indefinite"/>

      </circle>

      <text
        x="0"
        y="6"
        text-anchor="middle"
        font-size="20"
        opacity="0">

        💥

        <animate
          attributeName="opacity"
          values="0;1;0"
          dur="1.5s"
          begin="${delay}s"
          repeatCount="indefinite"/>

      </text>

    </g>
  `;
}

function createSvg(calendar) {
  const width = 800;
  const height = 300;

  const days =
    calendar.weeks.flatMap(
      week => week.contributionDays
    );

  const total =
    calendar.totalContributions;

  return `<?xml version="1.0" encoding="UTF-8"?>

<svg
  xmlns="http://www.w3.org/2000/svg"
  width="${width}"
  height="${height}"
  viewBox="0 0 ${width} ${height}">

  <defs>

    <linearGradient
      id="space"
      x1="0"
      y1="0"
      x2="1"
      y2="1">

      <stop
        offset="0%"
        stop-color="#02070b"/>

      <stop
        offset="50%"
        stop-color="#07151e"/>

      <stop
        offset="100%"
        stop-color="#02070b"/>

    </linearGradient>

    <filter id="glow">

      <feGaussianBlur
        stdDeviation="3"
        result="blur"/>

      <feMerge>

        <feMergeNode
          in="blur"/>

        <feMergeNode
          in="SourceGraphic"/>

      </feMerge>

    </filter>

  </defs>

  <rect
    width="${width}"
    height="${height}"
    rx="18"
    fill="url(#space)"/>

  <rect
    x="1"
    y="1"
    width="${width - 2}"
    height="${height - 2}"
    rx="18"
    fill="none"
    stroke="#17333f"
    stroke-width="2"/>

  ${createStars(width, height)}

  <text
    x="30"
    y="30"
    font-family="Arial, sans-serif"
    font-size="16"
    font-weight="700"
    fill="#ffffff">

    🚀 AYUSHMAN'S CONTRIBUTION MISSION

  </text>

  <text
    x="30"
    y="50"
    font-family="Arial, sans-serif"
    font-size="10"
    fill="#71a2b3">

    Ayushman013-amp • CODE ACTIVITY DETECTED

  </text>

  <text
    x="770"
    y="30"
    text-anchor="end"
    font-family="Arial, sans-serif"
    font-size="14"
    font-weight="700"
    fill="#39ff88">

    ${total.toLocaleString()} CONTRIBUTIONS

  </text>

  ${createAsteroids(14, width, height)}

  <g filter="url(#glow)">
    ${createContributionGrid(days)}
  </g>

  ${createEnemyShips(days)}

  ${createLasers()}

  ${createExplosion(150, 130, 0)}
  ${createExplosion(350, 145, 1.5)}
  ${createExplosion(570, 115, 3)}
  ${createExplosion(690, 155, 4.5)}

  ${createPlayerShip(width, height)}

  <g transform="translate(30 250)">

    <rect
      width="740"
      height="32"
      rx="8"
      fill="#07151d"
      stroke="#17333f"/>

    <circle
      cx="18"
      cy="16"
      r="5"
      fill="#39ff88">

      <animate
        attributeName="opacity"
        values="1;0.3;1"
        dur="1.2s"
        repeatCount="indefinite"/>

    </circle>

    <text
      x="32"
      y="21"
      font-family="Arial, sans-serif"
      font-size="10"
      font-weight="700"
      fill="#ffffff">

      SYSTEM ONLINE

    </text>

    <text
      x="175"
      y="21"
      font-family="Arial, sans-serif"
      font-size="10"
      fill="#7195a0">

      CONTRIBUTIONS POWER THE SHIP

    </text>

    <text
      x="710"
      y="21"
      text-anchor="end"
      font-family="Arial, sans-serif"
      font-size="10"
      fill="#39ff88">

      KEEP CODING 🚀

    </text>

  </g>

</svg>`;
}

async function main() {

  console.log(
    `🚀 Generating Space Shooter for ${USERNAME}...`
  );

  const calendar =
    await getContributions();

  const svg =
    createSvg(calendar);

  const output =
    path.join(
      process.cwd(),
      "assets",
      "space-shooter.svg"
    );

  fs.mkdirSync(
    path.dirname(output),
    {
      recursive: true
    }
  );

  fs.writeFileSync(
    output,
    svg,
    "utf8"
  );

  console.log(
    "✅ Space Shooter generated."
  );
}

main().catch(error => {

  console.error(error);

  process.exit(1);

});


============================================================
FILE: .github/workflows/update-space-shooter.yml
============================================================

name: 🚀 Update Ayushman's Space Shooter

on:

  schedule:
    - cron: "0 */12 * * *"

  workflow_dispatch:

permissions:
  contents: write

jobs:

  generate:

    runs-on: ubuntu-latest

    steps:

      - name: Checkout
        uses: actions/checkout@v4

      - name: Setup Node
        uses: actions/setup-node@v4
        with:
          node-version: 20

      - name: Generate Animation
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
        run: npm run generate

      - name: Commit Animation
        run: |

          git config user.name "github-actions[bot]"

          git config user.email "41898282+github-actions[bot]@users.noreply.github.com"

          git add assets/space-shooter.svg

          if git diff --cached --quiet; then
            echo "No changes."
          else
            git commit -m "🚀 Update contribution animation"
            git push
          fi


============================================================
FILE: README.md
============================================================

<div align="center">

# 🚀 AYUSHMAN'S SPACE SHOOTER

### 🛸 GitHub Contribution Mission

**Code • Commit • Contribute • Destroy Bugs**

<img
  src="https://raw.githubusercontent.com/Ayushman013-amp/github-space-shooter/main/assets/space-shooter.svg"
  width="100%"
  alt="Ayushman's Animated GitHub Space Shooter"
/>

### 🌌 Every Contribution Powers the Ship

</div>


---

## 👨‍💻 Ayushman013-amp

```text
🚀 SYSTEM       : ONLINE
🛸 SHIP         : ACTIVE
💻 CODING       : ACTIVE
🧠 LEARNING     : ACTIVE
🔥 CONTRIBUTING : ACTIVE
👾 BUGS         : DETECTED
💥 MISSION     : DESTROY BUGS
