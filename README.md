# NinePlagues

**A spiritual diagnostic quiz built on a nine-axis framework of existential ailments.**

NinePlagues is a browser-based self-assessment tool that attempts to diagnose spiritual and psychological afflictions according to a philosophical system rooted in [Evolutionist](https://evolution.faith/ninefold-vaccine/) thought. Users answer 58 statements on a Likert scale and receive a scored profile across nine dimensions of spiritual illness, along with a diagnosis and suggested remedial practices.

> **Status:** This project is incomplete and not actively maintained. It is hosted as a GitHub Pages site.

**Live site:** [https://their-holiness.github.io/NinePlagues/](https://their-holiness.github.io/NinePlagues/)

---

## Table of Contents

- [The Nine Plagues](#the-nine-plagues)
- [How the Quiz Works](#how-the-quiz-works)
- [Diagnostic Categories](#diagnostic-categories)
- [Project Structure](#project-structure)
- [Technical Architecture](#technical-architecture)
- [Origins and Lineage](#origins-and-lineage)
- [License](#license)
- [Contact](#contact)

---

## The Nine Plagues

The philosophical framework identifies nine spiritual illnesses organized into three triads:

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

## How the Quiz Works

### Flow

1. **Landing page** (`index.html`) — Overview of the system and plague descriptions.
2. **Instructions** (`instructions.html`) — Brief explanation of how to answer.
3. **Quiz** (`quiz.html`) — 58 statements presented in randomized order. Each is answered on a five-point scale:
   - Strongly Agree (+1.0)
   - Agree (+0.5)
   - Neutral (0.0)
   - Disagree (-0.5)
   - Strongly Disagree (-1.0)
   - A sixth option, "Don't Know / Don't Understand," skips the question entirely.
4. **Feedback** (`feedback.html`) — Optional anonymous demographic survey (only on the deployed site).
5. **Results** (`results.html`) — Scored profile with a canvas-rendered visualization, diagnosis, and triadic analysis.

### Scoring

Each question has weighted effects on one or more plague axes. Raw scores are normalized to a 0–100 percentage scale using the formula:

```
percentage = 100 * (maxPossibleScore + rawScore) / (2 * maxPossibleScore)
```

A score of **50%** is neutral. Scores above 50% indicate the presence of that plague; scores below 50% indicate its opposite virtue.

### Results Visualization

The results page generates an HTML5 Canvas image displaying:

- Nine horizontal bars, one per plague axis, color-coded by triad
- The user's percentage on each axis
- The plague name on one end and its opposing virtue on the other
- A textual diagnosis (closest matching archetype)
- Aggregate scores for each triad (Domicide, Foolishness, Entrapment)

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
