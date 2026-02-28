# NinePlagues

> **Status:** This project is incomplete and not actively maintained.

**Live site:** [https://their-holiness.github.io/NinePlagues/](https://their-holiness.github.io/NinePlagues/)

---

## What Is NinePlagues?

NinePlagues is a quiz that diagnoses your **spiritual illnesses** — nine fundamental ways people get stuck, disconnected, or distracted in life — and suggests practices to address them. It is part of the [Evolutionist](https://evolution.faith/ninefold-vaccine/) philosophical and spiritual tradition.

Think of it like a personality test, but instead of telling you *what kind of person you are*, it tells you *what's getting in your way* and *what to do about it*.

## How to Take the Quiz

1. Go to the [live site](https://their-holiness.github.io/NinePlagues/).
2. Click **"Click here to start!"** and read the brief instructions.
3. You'll be presented with **58 statements**. For each one, respond with how much you agree or disagree — from **Strongly Agree** to **Strongly Disagree**. If a statement doesn't make sense to you, choose **Don't Know / Don't Understand** to skip it.
4. At the end, you'll receive a results page showing your score on all nine plague axes, a visual breakdown, and a diagnosis with suggested remedies.

Answer honestly — there are no right or wrong answers.

---

## Table of Contents

- [The Nine Axes](#the-nine-axes)
- [How Scoring Works](#how-scoring-works)
- [Diagnostic Categories](#diagnostic-categories)
- [Project Structure](#project-structure)
- [Technical Architecture](#technical-architecture)
- [Origins and Lineage](#origins-and-lineage)
- [License](#license)
- [Contact](#contact)

---

## The Nine Axes

The quiz measures you on nine axes. Each axis runs from a **plague** (a spiritual illness) to its **opposite virtue** (the healthy counterpart). Your score on each axis is a percentage: higher means more plagued, lower means more liberated on that dimension.

The nine plagues are organized into three groups of three:

### Domicide (Disconnection)

Plagues of severance from one's environment, self, and world.

| Plague | Description | Opposite Virtue |
|--------|-------------|-----------------|
| **Alienation** | Disconnection from other people. Considered the worst plague because it prevents the sufferer from seeking help. | Collectivism |
| **Angst** | Disconnection from oneself; inner conflict and disharmony. | Plannedness |
| **Absurdity** | Disconnection from the world; the feeling that existence is meaningless. | Constructivism |

### Foolishness (Distraction)

Plagues of misdirected attention and undisciplined focus.

| Plague | Description | Opposite Virtue |
|--------|-------------|-----------------|
| **Forgetting** | Forgetting wonder; attempting to satisfy spiritual needs with material things. | Idealism |
| **Spiralling** | Over-focusing on a single thing (e.g., an ideology, a substance) to the detriment of everything else. | Particularism |
| **Drowning** | Inability to think through actions; oscillating between paralysis and impulsivity. | Industriousness |

### Entrapment (Stagnation)

Plagues of rigidity and resistance to growth.

| Plague | Description | Opposite Virtue |
|--------|-------------|-----------------|
| **Foreign Entrapment** | Applying frameworks that worked in one context to situations where they do not apply. | Apoliticism |
| **Ego Entrapment** | Clinging to a fixed self-image as a defense mechanism, preventing genuine change. | Secularity |
| **Empathic Entrapment** | Inability or unwillingness to inhabit and explore perspectives other than one's own. | Historicism |

---

## How Scoring Works

Each of the 58 questions has weighted effects on one or more plague axes. Your responses are scored on a scale from Strongly Agree (+1.0) to Strongly Disagree (-1.0), with Neutral at 0. Raw scores are normalized to a 0–100 percentage:

```
percentage = 100 * (maxPossibleScore + rawScore) / (2 * maxPossibleScore)
```

- **50%** = neutral on that axis
- **Above 50%** = presence of that plague
- **Below 50%** = leaning toward the opposite virtue

Questions are presented in randomized order each time you take the quiz. After completion, the deployed site optionally offers an anonymous demographic survey before showing results.

### Results Page

Your results page shows:

- Nine color-coded horizontal bars — one per axis, with the plague on one end and its opposite virtue on the other
- Your percentage score on each axis
- A **diagnosis** — the closest matching archetype (see below)
- **Triadic totals** — aggregate scores for Domicide, Foolishness, and Entrapment
- A shareable canvas-rendered image of your full profile

---

## Diagnostic Categories

The quiz matches the user's nine-dimensional profile to the nearest archetype using Euclidean distance:

| Diagnosis | Profile |
|-----------|---------|
| **Noble** | Liberated from all plagues (low scores across every axis) |
| **Moderately Plagued** | Moderate levels across the board |
| **Extremely Plagued** | High levels of all plagues |
| **Homeless** | Dominated by Domicide plagues (alienation, angst, absurdity) |
| **Foolish** | Dominated by Foolishness plagues (forgetting, spiralling, drowning) |
| **Entrapped** | Dominated by Entrapment plagues (foreign, ego, empathic entrapment) |

Each diagnosis category also links to suggested therapeutic practices (see `Prescription.js`), ranging from community involvement and meditation to perspective-taking exercises.

---

## Project Structure

```
NinePlagues/
├── index.html              Landing page with plague descriptions
├── instructions.html       Quiz instructions
├── quiz.html               Quiz engine (question rendering, scoring, navigation)
├── feedback.html           Optional post-quiz demographic survey
├── results.html            Results display and canvas visualization
├── credits.html            Image attribution
├── style.css               Stylesheet (Montserrat + Roboto, responsive layout)
├── questions.js             58 quiz questions with plague-axis effect weights
├── questions_feedback.js   Demographic survey question definitions
├── ideologies.js           Diagnostic archetype definitions and stat templates
├── results_dat.js          Axis labels, value names, and color mappings
├── Prescription.js         Treatment recommendations per plague and triad
├── icon.png                Favicon
├── values.svg              Compass visualization asset
├── value_images/           SVG icons for each plague and its opposite virtue
│   ├── alienation.svg
│   ├── angst.svg
│   ├── absurdity.svg
│   ├── forgetting.svg
│   ├── spiralling.svg
│   ├── drowning.svg
│   ├── foreign.svg
│   ├── ego.svg
│   ├── empathic.svg
│   └── ... (opposite virtue icons)
├── LICENSE                 MIT License
└── .gitignore
```

---

## Technical Architecture

- **Stack:** Vanilla HTML5, CSS3, and JavaScript. No build tools or frameworks.
- **Dependencies:** jQuery (DOM manipulation), js-cookie (optional demographic tracking), Google Fonts (Montserrat, Roboto).
- **State management:** `sessionStorage` holds quiz answers during a session; results are passed between pages via URL query parameters.
- **Visualization:** HTML5 Canvas API renders a shareable results image entirely client-side.
- **Diagnosis algorithm:** Euclidean distance in 9-dimensional space between the user's score vector and each archetype's template vector. The closest archetype is assigned as the diagnosis.
- **Analytics:** Google Analytics (UA-99715444-5). Demographic data collection is opt-in with three tiers: full survey + results, results only, or nothing recorded.

---

## Origins and Lineage

NinePlagues is a fork of [AltValues](https://altvalues.github.io/) (itself derived from [8values](https://8values.github.io/) and SexValues), repurposed from political/social value mapping to spiritual diagnosis. The quiz engine, scoring mechanism, and results visualization architecture are inherited from this lineage, with the axes, questions, and interpretive framework replaced entirely.

---

## License

MIT License (inherited from 8values). See [LICENSE](LICENSE) for details.

---

## Contact

- Email: immanuelleleonhart@gmail.com
- Discord: [discord.gg/swv7gz7ZEK](https://discord.gg/swv7gz7ZEK)
- Twitter: [@their_holiness](https://twitter.com/their_holiness)
- GitHub: [their-holiness/NinePlagues](https://github.com/their-holiness/NinePlagues)
