# agent-fit

> Is an agent the right fit?

## Why agent-fit

Most organisations now have more AI ideas than they can build, and many of those ideas are labelled "agent" before anyone has checked that they need one.

- In June 2025, [Gartner predicted](https://www.gartner.com/en/newsroom/press-releases/2025-06-25-gartner-predicts-over-40-percent-of-agentic-ai-projects-will-be-canceled-by-end-of-2027) that over 40% of agentic AI projects will be cancelled by the end of 2027, because of escalating costs, unclear business value or inadequate risk controls. It also said that many use cases positioned as agentic today don't require an agentic implementation.
- Anthropic's guidance in [Building effective agents](https://www.anthropic.com/engineering/building-effective-agents) is to "find the simplest solution possible, and only increase complexity when needed", which "might mean not building agentic systems at all".

**agent-fit** puts that advice into practice. Anyone in your organisation can submit an idea in plain language. The system recommends the simplest approach that works: no AI, an AI-assisted step, a workflow, a single agent, or multiple agents. It then explains why, using rules you can read and change. The same conversation then continues as a **Solution Advisor**, which helps the person take the idea forward whichever way fits, and for ideas that need engineers, prepares a Word document for that meeting.

## What it does

agent-fit helps a person with no technical background turn an AI idea into a clear, complete plan for taking it forward, and teaches them how AI solutions work along the way. There is one user, the person with the idea, and one conversation that changes role as it goes: first an interviewer, then a Solution Advisor.

**The interviewer** (release 1) is a conversation that:

1. **Understands the person and their work.** It asks plain-language questions, one at a time, and adapts its wording to who it is talking to.
2. **Builds an idea card.** Each fact is recorded as stated, inferred or unknown, with the person's own words as evidence.
3. **Recommends the simplest approach that fits:** not AI, AI-assisted, workflow, single agent, multi-agent, or needs more information. It then points to a matching option on the reference stack, which in this project is the Microsoft stack (see [Where an idea lands](#where-an-idea-lands)).
4. **Explains the answer and the parts.** The brain (the model), the hands (its tools), memory and knowledge, the rules, and a person in charge, each tied to the person's own idea.
5. **Lets them try what-ifs.** "What if a person approved every step?" The answer and the reasons update.
6. **Checks readiness before moving on:** ready, ready with conditions, or not yet, with the gaps named.

**The Solution Advisor** (next release) continues in the same conversation, so nothing is asked twice. What it does depends on the lane:

| Lane | What the Solution Advisor does | What the person gets |
|---|---|---|
| 1. Not AI | Explains why, and what kind of tool fits | A short note on screen |
| 2. Ready-made agent | Names the product, what to check and who to ask | A short note on screen |
| 3 and 4. Self-serve | Walks through building it with the stack's low-code tools (Agent Builder or Copilot Studio in the Microsoft example) | A starter specification on screen |
| 5. Needs engineers | Drafts a design on the reference stack (Microsoft Agent Framework, Microsoft Foundry and Azure in this project), checks it with rules in code, then prepares the engineers' meeting | A **Word document** with the full context |

For lane 5 the Solution Advisor approves nothing. It reviews the design, says what is still needed, and asks the person to take it to the AI engineers team, who decide how it is built. The Word document gives the person everything they need for that meeting: their own description of the idea, the recommendation and the reasons, the proposed design and the alternatives considered, the design check results, open items with suggested owners, questions for the engineers, and a plain-language glossary.

## The journey

```mermaid
flowchart TD
    subgraph R1["Release 1: the interviewer"]
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
    K --> L{"Which lane?"}
    L -->|not AI, or not yet| M(["Clear next step"])
    L -->|ready-made agent| S(["Adopt it"])
    subgraph ADV["Next release: the Solution Advisor, same conversation"]
        T["Starter specification<br/>on screen"]
        U["Draft design on the<br/>reference stack<br/>(Agent Framework, Foundry, Azure)"] --> V["Design checks<br/>rules in code"]
        V --> W["Word document<br/>full context for the engineers"]
    end
    L -->|self-serve: the stack's low-code tools| T
    L -->|needs AI engineers| U
    W --> X(["You meet the AI engineers team"])
    classDef now fill:#e8f1fb,stroke:#0f6cbd,color:#0b2e4f
    classDef later fill:#fff4e0,stroke:#e0a800,color:#5c4200
    class A,B,C,D,E,F,G,H,I,J,K,L,M,S now
    class T,U,V,W,X later
```

## Where an idea lands

The lanes below describe the *kind* of solution an idea needs, and they do not depend on a vendor. To make them concrete, this project uses the **Microsoft stack as its worked example**: each lane is mapped to a Microsoft option. The same lanes can be mapped to any other stack by replacing that mapping, and the stack mapping is designed to be kept separate from the rules so that swapping it does not change how ideas are judged.

The order follows a widely given piece of advice: check for a ready-made product before building one. Microsoft's own [technology plan for AI agents](https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/ai-agents/technology-solutions-plan-strategy) does exactly this, asking first whether a ready-made agent meets the need and building only if none does.

| Lane | When it fits | Who builds | Microsoft example |
|---|---|---|---|
| **1. Not AI** | Fixed rules, or a report | Whoever owns the process | Regular code or automation |
| **2. Ready-made agent** | A ready-made product already does it | Nobody, just adopt it | A Microsoft 365 Copilot or product agent |
| **3. Light self-serve** | One person or a small team, answering questions from their own content | The submitter | Agent Builder |
| **4. Low-code** | A department or customer-facing agent, multi-step work, approvals, simple integrations, low risk | A business maker, with support | Copilot Studio |
| **5. Needs AI engineers** | Multi-agent, high risk, strict repeatability, heavy integration | The AI engineers team | Microsoft Agent Framework, Microsoft Foundry and Azure |

For lanes 3 and 4, the Microsoft example follows Microsoft's [comparison of Agent Builder and Copilot Studio](https://learn.microsoft.com/en-us/microsoft-365-copilot/extensibility/copilot-studio-experience): Agent Builder for individuals and small teams, Copilot Studio for wider audiences and more advanced capability and governance.

**Risk sets a ceiling on self-serve.** A high-risk answer, such as irreversible actions or sensitive data, can never land in lanes 3 or 4, so self-serve never becomes unsupervised AI.

*agent-fit is an independent project. It is not an official Microsoft tool, and product capabilities change on any stack, so each recommendation should link to its source and be checked before you build.*

## Design principles

- **Code decides, the model proposes.** The recommendation and the readiness check come from rules you can read and change. The model gathers evidence and writes the explanation. It never picks the verdict.
- **Never guess.** A missing answer stays unknown and becomes a named condition.
- **Input is data, not instructions.** Whatever a person types is never treated as a command.
- **The person stays in charge.** The person decides when to move on. The Solution Advisor advises and drafts, and approves nothing.
- **Label what is what.** In everything it produces, each statement is marked as decided by rules, proposed by the model, or unknown, so engineers can see at a glance what to trust.
- **Simple first.** The system leans toward the simpler option, and a simple answer counts as a good result.
- **Honest about the platform.** agent-fit itself is built on Microsoft Foundry and Azure. The solutions it recommends are stack-neutral, with Microsoft as the worked example, and a recommendation is never bent to fit a platform.

## What it does not do

- It does not approve anything or make the final build decision. For ideas that need engineers, the AI engineers team decides how it is built.
- It does not need to know about individuals. People describe the work, not the people in it, and it is designed to keep only the idea card and the generated documents, in your own Azure subscription.

## How we will know it works

- **Repeatable:** the same idea gives the same recommendation every time.
- **Not over-complicated:** it rarely recommends more than the idea needs.
- **Complete plans:** the AI engineers rarely have to send a document back with questions.
- **Understood:** after the conversation, a non-technical person can explain the answer in their own words.

## Technical design

agent-fit is built on **Microsoft Agent Framework (MAF)**, **Microsoft Foundry** and **Azure**, and it runs entirely in your Azure subscription. Models come from a Foundry deployment, the service is a container on **Azure Container Apps**, and all state lives in Azure services. Nothing depends on a model or a server running on someone's machine.

### Architecture

```mermaid
flowchart TD
    P(["Person with an idea"]) --> C["Chat client<br/>terminal or web"]
    C -->|Entra sign-in| ING["Container Apps ingress<br/>built-in Entra authentication"]
    ING --> API
    subgraph ACA["Azure Container Apps: one stateless container, managed identity"]
        direction TB
        API["FastAPI service<br/>one endpoint, one conversation per idea"]
        TURN["Interview turn<br/>MAF workflow: model steps and code steps"]
        ADV["Solution Advisor<br/>MAF workflow: draft, lint, document"]
        SK["Skills<br/>explanations, lane guides, glossary"]
        DEC["Decision functions<br/>evidence check, rules, design lint, Word builder"]
        API --> TURN
        TURN --> DEC
        ADV --> DEC
        TURN -->|lane 5| ADV
        SK -.-> TURN
        SK -.-> ADV
    end
    TURN --> M["Foundry model deployment<br/>guardrails on input and output"]
    ADV --> M
    ACA -->|managed identity| COS[("Azure Cosmos DB<br/>idea cards and conversations")]
    ACA -->|managed identity| BLOB[("Blob Storage<br/>generated documents")]
    ACA -.-> AI["Application Insights<br/>OpenTelemetry traces from MAF"]
    EV["Evaluation run in CI<br/>persona conversations"] -.->|calls the service| ING
    EV -.-> FE["Foundry evaluations<br/>and red teaming scan"]
```

### One conversation turn

Every turn is a short chain. Models do the language, and code makes every decision and every check. This is the prompt-chaining-with-gates pattern from Anthropic's [Building effective agents](https://www.anthropic.com/engineering/building-effective-agents).

```mermaid
flowchart LR
    A["Person's message"] --> B["MODEL<br/>extract facts<br/>structured output"]
    B --> C{"CODE<br/>evidence check<br/>is the quote in their words?"}
    C -->|rejected| Q["CODE<br/>ask a follow-up"]
    C -->|passed| D["CODE<br/>update the card<br/>status derived in code"]
    D --> E["CODE<br/>rules decide<br/>verdict, lane, readiness"]
    E --> F["MODEL<br/>write the reply and explanation<br/>from the decided facts"]
    F --> G{"CODE<br/>faithfulness check<br/>matches the verdict?"}
    G -->|no| F
    G -->|yes| H["Reply to the person"]
    Q --> H
    classDef model fill:#f3e8ff,stroke:#7e3fbf,color:#3b1763
    classDef code fill:#e8f1fb,stroke:#0f6cbd,color:#0b2e4f
    class B,F model
    class C,D,E,G,Q code
```

The model never sets a status or picks a verdict. In a trial of this pattern with a small model, the model returned a fact with no supporting quote, and the evidence check rejected it. That is why the check is code.

### Components

| Concern | Choice | Notes |
|---|---|---|
| **Agent runtime** | [Microsoft Agent Framework](https://learn.microsoft.com/en-us/agent-framework/overview/) workflows | Code steps are function executors with conditional and switch-case edges. Model steps are agents. |
| **Model** | A Foundry model deployment, called through `FoundryChatClient` with Entra sign-in and no keys | The deployment name is configuration. Start with Global Standard, and choose a Data Zone or regional type if processing location matters ([deployment types](https://learn.microsoft.com/en-us/azure/ai-foundry/foundry-models/concepts/deployment-types)). |
| **Model sizes** | A smaller model for interview turns, a stronger one for the advisor's design drafts | A hypothesis. The evaluations decide. |
| **Hosting** | [Azure Container Apps](https://learn.microsoft.com/en-us/azure/container-apps/overview), one container image | The app can scale to zero, and billing then stops for consumption ([billing](https://learn.microsoft.com/en-us/azure/container-apps/billing)). Setting a minimum of one replica keeps an instance always running, which avoids a cold start ([scaling](https://learn.microsoft.com/en-us/azure/container-apps/scale-app)). |
| **Service** | A FastAPI app that serves one endpoint and runs the MAF workflows | The stable `agent-framework-ag-ui` package provides a FastAPI endpoint for agents and workflows, and is a candidate for the protocol a web client would speak. |
| **Sign-in** | Container Apps [built-in authentication](https://learn.microsoft.com/en-us/azure/container-apps/authentication) with Microsoft Entra ID | Authentication happens at the platform edge, before a request reaches the app. |
| **Idea card and conversation** | Azure Cosmos DB, one document per idea holding the card and the transcript | Our own state, written with the stable `azure-cosmos` SDK. The service is stateless: each request loads the idea, runs one turn and saves it, so any replica can serve any turn. |
| **Documents** | Word files built in code with `python-docx`, stored in Blob Storage | Returned to the person through time-limited access. |
| **Explanations** | MAF [skills](https://learn.microsoft.com/en-us/agent-framework/agents/skills) (`SKILL.md`) | Versioned in the repo and loaded only when relevant. |
| **Content safety** | [Foundry guardrails](https://learn.microsoft.com/en-us/azure/ai-foundry/guardrails/guardrails-overview) on the model deployment, covering input and output | Agent-level controls, such as tool-call and tool-response checks, apply only to agents built in Foundry Agent Service, so they are not available here. Limits on what the agent may do are enforced in code. |
| **Prompt injection** | Code gates first: input is data and every extracted fact needs a verified quote | MAF's experimental `security` module is a candidate to add. |
| **Tracing** | OpenTelemetry from MAF, sent to Application Insights | Container Apps also sends console logs to Log Analytics ([log monitoring](https://learn.microsoft.com/en-us/azure/container-apps/log-monitoring)). |
| **Evaluations** | Persona conversations run in CI against the deployed service, graded by code on the outcome | Foundry's [built-in evaluators](https://learn.microsoft.com/en-us/azure/ai-foundry/concepts/evaluation-approach-gen-ai) grade explanation quality, and a red teaming scan runs before each release. |
| **Infrastructure** | The Azure Developer CLI (`azd`) with Bicep, using [Azure Verified Modules](https://azure.github.io/Azure-Verified-Modules/) where they exist | `azd` supports a `containerapp` host that deploys from an image or builds from source ([schema](https://learn.microsoft.com/en-us/azure/developer/azure-developer-cli/azd-schema)). |
| **Identity** | A managed identity on the container app, with least-privilege roles on each resource | The identity pulls the image from the registry without a password ([managed identity](https://learn.microsoft.com/en-us/azure/container-apps/managed-identity)) and calls the model, Cosmos DB and Blob Storage with role assignments. No keys or secrets in code. |

### Azure resources

| Resource | Purpose |
|---|---|
| Foundry resource and project | Model deployments and evaluations ([architecture](https://learn.microsoft.com/en-us/azure/ai-foundry/concepts/architecture)) |
| Model deployment | The model the service calls. The app's identity needs the Foundry User role on the Foundry resource ([roles](https://learn.microsoft.com/en-us/azure/ai-foundry/concepts/rbac-foundry)). |
| Container Apps environment and container app | Runs the service |
| Container Registry | The service's container image |
| Managed identity | Image pull and access to every other resource |
| Cosmos DB account | Idea cards and conversations, with a data-plane role for the identity |
| Storage account | Generated documents, with a data-plane role for the identity |
| Application Insights and Log Analytics | Traces, metrics and logs |

### Design decisions

1. **Container Apps, not a Foundry hosted agent.** We own the endpoint and the conversation state, which keeps the service portable and not tied to the hosted-agent region list or its preview-only controls. The cost is that we build and secure the endpoint ourselves, and we do not get agent-level guardrails.
2. **A stateless service.** All state lives in Cosmos DB, so replicas can be added, removed or restarted at any time, and the app can scale to zero between conversations.
3. **Cosmos DB for the card and transcript, not workflow checkpoints.** Each turn is one request and the person is the human in the loop, so no workflow needs to pause for days. MAF's Cosmos checkpoint storage and history provider are beta, and checkpoints use pickle, so they are added only if that changes.
4. **No search index, embeddings or Foundry Memory in release 1.** The card is the memory, and explanations are versioned files.
5. **Decision logic is plain Python functions.** The MAF code steps call them. That keeps the rules readable and lets the decision tests run with no model and no Azure, which is the only part of the project that runs without Azure.
6. **The interview starts as a workflow with code gates.** It becomes an agent that chooses its own next question only if the evaluations show it must.
7. **Conversations are graded on the outcome, not the path.** The card, verdict, lane and readiness must be right, and the order of questions can vary.

### Dependencies

| Package | Role | Maturity at time of writing |
|---|---|---|
| `agent-framework-core`, `agent-framework-foundry` | Workflows, agents, skills, Foundry client | Stable |
| `agent-framework-ag-ui` | FastAPI endpoint for agents and workflows (candidate) | Stable |
| `fastapi`, `uvicorn` | The web service | Stable |
| `azure-cosmos`, `azure-storage-blob`, `azure-identity` | State and sign-in | Stable |
| `azure-monitor-opentelemetry` | Sends traces to Application Insights | Stable |
| `azure-ai-evaluation` | Foundry evaluations | Stable |
| `python-docx`, `pydantic` | Word documents and typed contracts | Stable |

Pin every version, and re-run the evaluations on each upgrade, because MAF is releasing quickly.

### To validate during the build

- That the Foundry resource and project, the model deployment and the role assignments can all be created with Azure Verified Modules. The account module supports the `AIServices` kind with deployments and a project-management setting, but it is not confirmed that it creates the project itself.
- The least-privilege role that lets the app's managed identity call a model deployment through the project endpoint. The documented role is Foundry User.
- Which Foundry models, deployment types and quotas are available in the chosen region.
- Whether the `agent-framework-ag-ui` endpoint suits a workflow-based turn, or a thin FastAPI route of our own is simpler.
- Cold start time when the app has scaled to zero, and whether a minimum of one replica is worth its cost.
- Whether private networking is needed for Container Apps, Cosmos DB, Storage and the model endpoint in a regulated setting.

## Roadmap

1. **Release 1:** the interviewer, a conversation that ends in a confirmed idea card and a lane, deployed to your Azure subscription.
2. **Next:** the Solution Advisor in the same conversation: a starter specification on screen for the self-serve lanes, and for lane 5 a design on the reference stack with rule-based checks, plus the Word document for the AI engineers' meeting.
3. **Later:** an interactive visual experience, and a build brief that a human team or a supervised agent team can work from.
