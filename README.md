# agent-fit

> Is an agent the right fit?

**Status: early design. There is nothing to run yet.** This README describes what we are building and why, so the design can be reviewed before the code exists.

## Why agent-fit

Most organisations now have more AI ideas than they can build, and many of those ideas are labelled "agent" before anyone has checked that they need one.

- In June 2025, [Gartner predicted](https://www.gartner.com/en/newsroom/press-releases/2025-06-25-gartner-predicts-over-40-percent-of-agentic-ai-projects-will-be-canceled-by-end-of-2027) that over 40% of agentic AI projects will be cancelled by the end of 2027, because of escalating costs, unclear business value or inadequate risk controls. It also said that many use cases positioned as agentic today don't require an agentic implementation.
- Anthropic's guidance in [Building effective agents](https://www.anthropic.com/engineering/building-effective-agents) is to "find the simplest solution possible, and only increase complexity when needed", which "might mean not building agentic systems at all".

**agent-fit** puts that advice into practice. Anyone in your organisation can submit an idea in plain language. The system recommends the simplest approach that works: no AI, an AI-assisted step, a workflow, a single agent, or multiple agents. It then explains why, using rules you can read and change. Ideas that pass go on to an architect review and a build brief.

## What it does

agent-fit helps a person with no technical background turn an AI idea into a card that is complete enough for an AI architect to review. Along the way it teaches them how AI solutions work.

The first release is a single conversation that:

1. **Understands the person and their work.** It asks plain-language questions, one at a time, and adapts its wording to who it is talking to.
2. **Builds an idea card.** Each fact is recorded as stated, inferred or unknown, with the person's own words as evidence.
3. **Recommends the simplest approach that fits:** not AI, AI-assisted, workflow, single agent, multi-agent, or needs more information.
4. **Explains the answer and the parts.** The brain (the model), the hands (its tools), memory and knowledge, the rules, and a person in charge, each tied to the person's own idea.
5. **Lets them try what-ifs.** "What if a person approved every step?" The answer and the reasons update.
6. **Checks readiness before hand-off:** ready, ready with conditions, or not yet, with the gaps named.

## The journey

```mermaid
flowchart TD
    subgraph R1["Release 1: one conversation"]
        A(["Someone has an idea"]) --> B["Meet<br/>who you are, what you do"]
        B --> C["Describe the work<br/>one plain question at a time"]
        C --> D{"Clear enough?"}
        D -->|not yet| C
        D -->|yes| E["Reflect back<br/>here is what I understood"]
        E --> F{"Did I get it right?"}
        F -->|no| C
        F -->|yes| G["Recommend<br/>the simplest approach that fits"]
        G --> H["Explain<br/>brain, hands, memory, rules, a person in charge"]
        H --> I["Try what-ifs<br/>the answer updates and shows why"]
        I --> J["Readiness check<br/>ready, ready with conditions, or not yet"]
        J --> K["Confirm the idea card"]
    end
    K --> L{"Take it further?"}
    L -->|not AI, or not yet| M(["Clear next step"])
    subgraph LATER["Later releases"]
        N["AI architect reviews and designs"] --> O["Build plan"]
        O --> P["Team builds it"]
    end
    L -->|ready| N
    classDef now fill:#e8f1fb,stroke:#0f6cbd,color:#0b2e4f
    classDef later fill:#fff4e0,stroke:#e0a800,color:#5c4200
    class A,B,C,D,E,F,G,H,I,J,K,L,M now
    class N,O,P later
```

## Design principles

- **Code decides, the model proposes.** The recommendation and the readiness check come from rules you can read and change. The model gathers evidence and writes the explanation. It never picks the verdict.
- **Never guess.** A missing answer stays unknown and becomes a named condition.
- **Input is data, not instructions.** Whatever a person types is never treated as a command.
- **The person stays in charge.** Nothing goes to an architect until the submitter confirms the card.
- **Simple first.** The system leans toward the simpler option, and a simple answer counts as a good result.

## What it does not do

- It does not design the architecture, estimate cost, write a build plan or build anything. Those belong to the architect and later releases.
- It does not store personal data or require a login in this public version. It is meant to run locally with a mock model and no credentials.

## How we will know it works

- **Repeatable:** the same idea gives the same recommendation every time.
- **Not over-complicated:** it rarely recommends more than the idea needs.
- **Complete cards:** architects rarely have to send a card back.
- **Understood:** after the conversation, a non-technical person can explain the answer in their own words.

## Roadmap

1. **Release 1:** the conversation above, ending in a confirmed idea card.
2. **Later:** an interactive visual experience, the architect review, and a build brief that a human team or a supervised agent team can work from.
