# Day 3: How Modern LLMs and AI Agents Work

> **Part of my AI Engineering learning journey**

Most people use AI to ask questions, generate text, or write code. As an AI Engineer, however, a more important question is:

**What happens behind the interface, what are different LLMs trained to do, and how do we choose the right model for the right problem?**

Day 3 was a theoretical exploration of modern frontier models, AI agents, and the emerging AI ecosystem. Instead of writing a complete application, the Udemy lecture by Ed Donner focused on model capabilities, limitations, and how models can collaborate.

## Table of Contents

1. [Types of LLMs](#1-types-of-llms)
2. [Choosing the Right Type of Model](#2-choosing-the-right-type-of-model)
3. [Frontier Models and the AI Ecosystem](#3-frontier-models-and-the-ai-ecosystem)
4. [What Makes Frontier Models Powerful](#4-what-makes-frontier-models-powerful)
5. [Knowledge Distillation](#5-knowledge-distillation)
6. [Limitations of LLMs](#6-limitations-of-llms)
7. [AI Agents](#7-ai-agents)
8. [Deep Research](#8-deep-research)
9. [AI Image Generation](#9-ai-image-generation)
10. [Coding Agents](#10-coding-agents)
11. [Multi-Agent Systems](#11-multi-agent-systems)
12. [Key Takeaways](#12-key-takeaways)

---

## 1. Types of LLMs

Not every language model is trained to behave in the same way. Four important categories are base models, chat models, reasoning models, and hybrid models.

### 1.1 Base Models

A **base model** is trained primarily to predict the next token from the sequence of tokens it has already received.

For example:

```text
Input:  "The capital of Germany is..."
Output: "Berlin."
```

The model is completing a text sequence; it has not necessarily been adapted to follow instructions or behave like a conversational assistant.

Predictive text on a smartphone is a simplified version of next-token prediction:

```text
How are...
  - you
  - things
  - they
```

After the user selects a suggestion, the model predicts the next word again.

**Best suited for:**

- Custom model training
- Specialized downstream applications
- Developing a model with a particular new purpose

### 1.2 Chat Models and Instruction Models

A **chat model** has additional training that enables it to follow instructions and participate in structured conversations.

A typical interaction consists of three parts:

| Component | Purpose |
|---|---|
| System prompt | Defines the assistant's role, behavior, and restrictions |
| User prompt | Contains the user's request or question |
| Assistant response | Contains the model's generated answer |

A practical example:

```text
System: You are an experienced cybersecurity analyst.
        Explain technical concepts in simple language.

User:   What is SQL injection?

Assistant: A structured explanation of SQL injection,
           how it works, and how to prevent it.
```

The system prompt establishes *who the AI should be*, while the user prompt defines *what the AI should do*.

#### Reinforcement Learning from Human Feedback

**Reinforcement Learning from Human Feedback (RLHF)** uses human preferences to improve model responses.

For example, both answers below may be technically correct:

- **Answer A:** Technically correct but confusing
- **Answer B:** Technically correct, clear, and helpful

Human raters can indicate that Answer B is preferable. This feedback can then be used to train or tune the model to favor clearer and more useful responses.

RLHF is one of the approaches historically used to turn language models into more helpful assistants.

### 1.3 Reasoning Models

**Reasoning models** are trained or configured to spend more computation working through difficult problems before producing a final answer.

Example:

```text
You have three boxes.
One contains only apples, one contains only oranges,
and one contains both.
All labels are incorrect.

What is the minimum number of fruits you need to pick
to identify all the boxes?
```

The model must work through constraints systematically rather than simply generate a plausible response.

Reasoning models are particularly useful for:

- Mathematics
- Logic
- Complex planning
- Multi-step analysis
- Difficult coding problems

#### Chain-of-Thought Prompting

**Chain-of-thought prompting** encourages a model to approach a problem in smaller, structured steps.

Instead of asking:

```text
Calculate the total cost.
```

Ask:

```text
Break this problem into smaller steps.
Identify the relevant values.
Calculate the total.
Explain the result.
```

The goal is to make the model's problem-solving process more structured. It does not guarantee that every intermediate statement is correct, so important results should still be verified.

### 1.4 Hybrid Models

Modern **hybrid models** can dynamically adjust how much reasoning effort they use.

| Request | Likely reasoning effort |
|---|---|
| "Hello, how are you?" | Low |
| "Design a payment-processing architecture that handles millions of transactions." | High |

A hybrid model can return quickly for simple questions and allocate more computation to complex tasks.

This is related to the concept of a **reasoning budget**: the amount of computational effort allowed for a task.

Budget forcing, including an experiment described in the S1 research paper, inserts words such as `"wait"` into a reasoning sequence to encourage the model to reconsider its intermediate reasoning. This demonstrates that reasoning effort can be influenced by training and inference configuration.

---

## 2. Choosing the Right Type of Model

More reasoning does not automatically mean a better experience. Model choice should match the problem.

| Model type | Best for |
|---|---|
| Base model | Custom training and specialized behavior |
| Chat model | Conversations, content generation, and quick answers |
| Reasoning model | Complex problem-solving, mathematics, and logical tasks |
| Hybrid model | Applications that need both fast responses and deeper reasoning |

### Example: AI-Powered Customer Support

- A **chat model** can answer frequently asked questions.
- A **reasoning model** can investigate a complicated customer complaint.
- A **hybrid model** can select a response strategy based on message complexity.

> **Engineering principle:** Do not automatically select the most powerful or expensive model. Select the model that fits the task, latency requirements, budget, and expected output.

---

## 3. Frontier Models and the AI Ecosystem

A **frontier model** is generally a highly capable model near the leading edge of current AI development. A **foundation model** is a broadly trained model that can be adapted to many downstream applications.

Major model developers discussed in the lecture include:

| Organization | Model families |
|---|---|
| OpenAI | GPT family and open-weight models such as GPT-OSS |
| Anthropic | Claude family |
| Google | Gemini family |
| xAI | Grok family |
| DeepSeek | DeepSeek family |

Different models have different strengths:

- Long-context reasoning
- Multimodal understanding
- Speed and efficiency
- Complex reasoning
- Coding
- Cost-effective deployment

There is no single model that is automatically the best choice for every application. Evaluation and comparison matter.

---

## 4. What Makes Frontier Models Powerful

### 4.1 Synthesizing Information

**Synthesis** means collecting information from multiple sources, understanding relationships, identifying themes and differences, and producing one coherent explanation.

Suppose five cybersecurity articles discuss:

1. Ransomware
2. Phishing
3. Cloud vulnerabilities
4. AI-powered attacks
5. Security regulations

Reading the articles gives separate pieces of information. An LLM can synthesize them into an overview:

> Modern organizations face an increasingly interconnected threat landscape. Ransomware and phishing remain major attack vectors, while cloud misconfiguration and AI-assisted attacks introduce additional risks. Organizations therefore need stronger identity management, continuous monitoring, and security awareness.

Useful applications include market research, competitor analysis, financial report analysis, research summaries, and cybersecurity threat intelligence.

### 4.2 Fleshing Out a Skeleton

An effective way to use an LLM is to build a solution progressively.

For example:

```text
I want to build an AI-powered customer support application.
Give me the main components and architecture.
```

The model may suggest:

- User interface
- Authentication system
- Backend API
- LLM integration
- Knowledge base
- Database
- Logging and monitoring

That structure is the **skeleton**. The user can then ask the model to expand one component:

```text
Explain document ingestion, text chunking, embeddings,
vector storage, and retrieval for the knowledge base.
```

The model adds technical details, implementation steps, dependencies, challenges, and design decisions. This is **fleshing out**.

Rather than requesting a complete solution immediately, this approach builds the solution one layer at a time.

### 4.3 Generating and Improving Content

Frontier models can generate:

- Emails and business proposals
- Technical documentation
- Presentations
- Project plans
- Product descriptions
- Marketing strategies
- Technical explanations

For example, a small coffee shop could ask for a limited-budget marketing plan targeting university students in Germany. The model provides a starting point that can be challenged, revised, and refined.

This makes the model a collaborative tool for developing ideas rather than only an answer generator.

### 4.4 Coding and Software Development

Modern LLMs can:

- Generate code
- Explain unfamiliar codebases
- Identify bugs
- Refactor implementations
- Write unit tests
- Suggest architectural improvements
- Generate documentation

Coding systems can also operate through iterative development loops:

```text
Understand the task
        ↓
Inspect the existing code
        ↓
Generate an implementation
        ↓
Run tests
        ↓
Identify errors
        ↓
Modify the implementation
        ↓
Run tests again
```

This is much closer to an actual software development workflow and is an important step toward agentic AI.

---

## 5. Knowledge Distillation

**Knowledge distillation** is a technique in which a smaller model, called the **student**, learns behavior from a larger model, called the **teacher**.

```text
Teacher model
      ↓
Generate answers for selected questions
      ↓
Answers become training examples
      ↓
Smaller student model learns similar behavior
```

Think of it as a senior engineer teaching a junior engineer through examples, explanations, and feedback.

### Benefits

A distilled model may offer:

- Lower inference costs
- Faster responses
- Lower memory requirements
- Easier deployment
- Better suitability for resource-constrained environments

### Trade-Off

Distillation does not guarantee that the student retains every capability of the teacher. It is a trade-off among capability, model size, speed, deployment cost, and accuracy.

> **Important:** Distillation is not simply the same thing as making a model run faster or compressing model weights; knowledge distillation specifically involves transferring behavior or learned knowledge.

---

## 6. Limitations of LLMs

LLMs are powerful, but they are not perfect.

### 6.1 Knowledge Cutoff

A model is trained using information available during its training process. It does not automatically learn that a real-world service, package, or API has changed.

For example, a model trained before a new Python library release might recommend:

- An outdated function
- An incorrect package version
- An API that no longer exists

Modern AI products can use tools such as web search to retrieve fresh information, but the model itself remains separate from those tools.

### 6.2 Hallucinations

A **hallucination** occurs when an LLM produces information that appears convincing but is incorrect, fabricated, or unsupported.

For example:

```text
User:  Which Python library supports function XYZ?

Model: Recommend Library ABC and provide an example.

Result: The library is installed, but function XYZ does not exist.
```

A language model generates likely continuations of text; it is not inherently a database that verifies every statement against reality.

**Validation is essential.** A confident answer is not necessarily a correct answer.

### 6.3 Over-Reliance on AI-Generated Code

An LLM can identify an error and generate a plausible fix without understanding the root cause correctly. The fix may work around the symptom while leaving the underlying problem unresolved.

LLMs are best treated as extremely capable junior analysts:

**The model can:**

- Research
- Write
- Generate code
- Analyze information
- Suggest solutions

**A human or a deterministic system must still:**

- Verify the output
- Challenge assumptions
- Check the implementation
- Identify incorrect conclusions
- Align the work with the actual objective

---

## 7. AI Agents

Traditional interactions with an LLM look like this:

```text
User asks a question → Model generates an answer
```

An **AI agent** can pursue a goal by planning steps, using tools, observing results, and adjusting its actions.

### Example: Finding a Restaurant

A request may have very specific requirements:

- British cuisine
- Banoffee pie on the menu
- Availability at 9 PM
- A reservation for four people

Instead of merely suggesting restaurants, an agent could:

1. Interpret the request
2. Search for suitable restaurants
3. Open their websites
4. Examine menus
5. Interact with a reservation platform
6. Check availability
7. Return a suitable result

The agent is not only telling the user what to do. It uses tools to perform parts of the task.

### Agentic AI

**Agentic AI** refers to systems designed to pursue goals through actions, tool usage, planning, and iterative execution.

A simplified workflow is:

```text
Goal → Plan → Act → Observe → Adjust → Complete
```

---

## 8. Deep Research

**Deep Research** is an agentic workflow that conducts extensive research instead of returning a quick answer.

The process may include:

- Identifying relevant research questions
- Searching multiple sources
- Reading and analyzing information
- Comparing findings
- Producing a structured report
- Including references for verification

The work may continue in the background while the user performs other tasks.

### Business Applications

- Competitor research
- Market analysis
- Product research
- Technical research
- Investment research
- Internal business reporting

The results still need to be checked against reliable sources.

---

## 9. AI Image Generation

AI products can convert natural-language instructions into visual outputs. For example:

> "Draw an image showing how many rainbows it takes to jump from Hawaii to 17."

The model interprets the request and generates an image.

Image generation can support:

- Marketing asset creation
- Product concept visualization
- Design prototyping
- Educational illustrations
- Creative content

An AI product does not necessarily have to return text. It can generate different types of output depending on the model and available tools.

---

## 10. Coding Agents

### Claude Code Example

A task might be:

> Read the Day 1 and Day 2 notebooks, understand the existing project, and implement the Day 2 website-summarization challenge using a local Llama model.

A coding agent could:

- Read the existing notebooks
- Understand the previous implementation
- Identify the challenge requirements
- Create a Python module such as `solution.py`
- Configure communication with Ollama
- Use a local model such as Llama 3.2
- Implement the website-summarization workflow

The developer can then run the script and validate the result.

### Traditional Code Generation vs. Coding Agents

| Traditional code generation | AI-assisted coding agent |
|---|---|
| The user provides a specific instruction | The user provides an objective |
| The model returns a code snippet | The agent inspects the project |
| The user integrates the code | The agent can modify files |
| Limited project context | Project-wide context |
| The user runs commands separately | The agent can execute and inspect commands |

Coding agents make project context especially important. The agent must understand the existing structure accurately and the developer must still review changes, run tests, and validate behavior.

---

## 11. Multi-Agent Systems

Edward Donner's **Outsmart** demonstration placed four LLMs in a competitive game.

Each model represented a player:

- Alex
- Blake
- Charlie
- Drew

Every player started with 12 coins. During each turn, players could:

- Transfer coins
- Exchange messages
- Negotiate
- Form alliances
- Cooperate or compete
- Strategize against other players

The models could explain their strategies and decisions as the game progressed.

### Business Simulation

The same concept can apply to a business simulation:

| Agent | Objective |
|---|---|
| Sales Manager | Maximize revenue |
| Financial Analyst | Minimize expenses and manage budgets |
| Operations Manager | Optimize delivery and efficiency |

The agents exchange information, evaluate proposals, and contribute to a shared outcome. This is the basic idea behind a **multi-agent AI system**.

> The strategies and inner thoughts displayed in a game are generated model outputs. They should not automatically be interpreted as a transparent recording of the model's actual internal reasoning.

---

## 12. Key Takeaways

AI Engineering is more than calling an LLM API. It requires selecting, integrating, orchestrating, and validating AI capabilities to solve real problems.

### Concepts to Remember

| Concept | Core idea |
|---|---|
| Base model | Predicts the next token |
| Chat model | Follows conversational instructions |
| Reasoning model | Allocates computation to complex problem-solving |
| Hybrid model | Adapts between fast responses and deeper reasoning |
| Knowledge distillation | Transfers useful behavior from a larger model to a smaller one |
| Information synthesis | Connects information from multiple sources |
| Skeleton and fleshing out | Turns an initial structure into a detailed plan |
| AI agent | Uses tools and actions to pursue a goal |
| Deep Research | Conducts multi-step research and produces a report |
| Coding agent | Understands and modifies an existing codebase |
| Multi-agent system | Coordinates agents with different roles or objectives |

Instead of building one giant AI system that does everything, applications can distribute responsibilities across different models and tools.

### The Engineer's Responsibility Is Changing

AI can accelerate:

- Code generation
- Research
- Project inspection
- Debugging
- Multi-step task execution

But engineering judgment determines whether that execution is correct.

The engineer must still understand:

- The code
- The problem
- The architecture
- The model's limitations
- How to validate the output
- Which model or tool belongs in the application

For me, Day 3 was about developing a broader perspective. Becoming an AI Engineer is not only about learning another framework or API. It is about understanding the entire ecosystem: models, reasoning, inference, tools, agents, orchestration, and the problems they can solve.

---

#AIEngineering #ArtificialIntelligence #LLM #GenerativeAI #AIEngineeringJourney #OpenAI #Claude #Gemini #DeepSeek #AgenticAI #AIResearch #MachineLearning #SoftwareEngineering #LearningInPublic #BuildInPublic #CyberSecurity #Business
