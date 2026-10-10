# AI Cybersecurity and Governance Notes (Columbia)

## Module 1: Cybersecurity Primer

There were already big data breaches prior to AI. AI accelerated and increased the attack surface.

> “The companies and countries that treat AI security as an afterthought are not moving faster. They are moving faster toward the moment when they will have to slam the brakes aggressively.” - Neil Daswani (AI Attacks)

### 1.1 Mega-Breach Patterns Overview

Timeline:

- 1970s cybersecurity early research
- mega data breaches started after internet commercialization in the 1990s
- 2003: Data Breach Notification Act in CA
- 2004: CardSystems 40 million credit card number breach via SQL injection
- 2013+: mega-breaches (Target, JPM Chase, OPM, Yahoo!, Meta, Equifax, etc…)

### 1.2 Root Causes of Breaches

Category of Root Causes:

- Managerial
  - Prioritization of Cybersecurity
  - Investment in Cybersecurity
  - Execution of Cybersecurity Initiatives
- Technical
  - Account Takeover
  - Malware (Malicious Software)
  - Software and Supply Chain Vulnerabilities

### 1.3 Early Mega-Breaches

Types of mega-breaches:

- Supply Chain Breaches
- Lack of MFA

#### Target (2013)

- 40+ Million credit card records stolen
- Attack:
  - Fazio Mechanical Services breached.
  - Fazio Mechanical Services and Target network linked.
  - Target employee directory accessed and targeted via phishing attacks
  - Malware installed in POS, then credit card stolen on a Black Friday sale

#### JPM Chase (2014)

- 70 million customer names and email addresses
- Annual Charity Marathon website breached via employees who used the same password as with corporate accounts
- Small number of servers without 2FA/MFA.
- Attackers can make targeted phishing attempts because of the customer list

#### OPM (2015)

- 21.5M background checks, 5.6M fingerprints stolen
- Risk for government employees and potentially CIA agents

### 1.4 Tech Mega-Breaches

#### Yahoo (2016)

- 3 Billion Yahoo Email Accounts
- Attack:
  - Phishing
  - Reverse engineer Yahoo site authentication:
    - reverse engineered how Yahoo generates authentication cookies
- Disclosed before Verizon acquisition ($350M price drop)

#### Equifax (2017)

- 145 million names, SSNs, DOB, etc.
- Attack:
  - Apache Struts had a vulnerability, which was not fixed in time
  - Gained visibility on 60 databases
- $575M settlement

#### CapitalOne (2019)

- 100M US SSNs, 1M Canadian SSNs
- Attack:
  - Aggressive use of AWS (Cloud)
  - Former AWS employee attacked and stole data.
- $100M - $150M cost

Security breaches are really expensive.

### 1.5 Nation-State Breaches

#### SolarWinds Data Breach (2020)

- Provided software used by US Govt Agencies and other companies
- Attack:
  - Russian adversary planted sophisticated backdoor into Orion product
  - Build system / CI/CD, routine deployment enabled backdoor attack
  - Cyber Espionage
- Federal Agencies required to have SBOM

#### Colonial Oil Pipeline Data Breach (2021)

- Attack:
  - stole VPN password from dark web and planted ransomware
  - same password used on corporate systems, no 2FA/MFA
- Solutions:
  - Monitor dark web for stolen credentials
  - Use 2FA

### 1.6 Ransomware

- Modern Ransomware: National Security Threat
- Double Extortion:
  - exfiltration of data
  - Re-encrypt data, then copy, export, and hold data elsewhere
  - Blackmails victims
- Targets and encrypts online backups:
  - Have offline backups

Orgs don’t employ cybersecurity hygiene, root causes are both managerial and technical.

## Module 2: AI Primer

### 2.1 Brief History of AI

- 1940-50s: Alan Turing (Turing Test)
- 1955: McCarthy, Coined term Artificial Intelligence
- 1960s: ML, Neural Networks, Eliza, Robotics (Shakey), SHRDLU
- 1970s-1980s: AI Winter, Expert Systems, rule-based…
- 1990s-2000s: ML Renaissance, IBM Deep Blue, Brute force search, beat Kasparov, Google ML for Ads
- 2010: Deep Learning Neural Network Renaissance
- 2016: Google DeepMind
- 2017: Google Brain: Attention is all you need, transformer architecture
- 2020: Google AlphaFold
- 2022: ChatGPT 3.5, GenAI Revolution

### 2.2 What is AI and ML?

Neural Networks:

- takes input signals (words, images, etc.), goes through math activation functions to decide what signal/output to pass to next layer.
- training, backpropagation
- testing/execution

AI is based on ML.

### 2.3 Pyramid of AI

Pyramid:

- agentic AI
  - execute multi-step workflows, interact with other software tools, autonomy
  - autonomous agents, research, implement and ship code, etc.
- generative AI
  - LLM
  - generate reports, summarizing, etc.
- traditional ML
  - classifiers/predictions
  - fraud detection, algorithmic recommendations

### 2.4 AI Capabilities and Risks

The higher the autonomy, the higher the risk. ML is least autonomous, Agentic AI has highest autonomy.

Threats:

- ML: training data poisoning, model theft, model evasion, overfitting
- GenAI: hallucinations, prompt injection (direct), jailbreaks
- AgenticAI: prompt injection (indirect), jailbreaks, untraceability

## Module 3: Multimodal GenAI Risks

### 3.1 Deepfakes

Types:

- Text-based
- Audio-based
- Video-based

Concerns:

- Generated Content
- Synthetic Media
- Distinguish Reality

### 3.2 AI Hallucinations

- generate convincing but false information, resulting in disinformation or bad business decisions.

Why hallucinating?

- trained on both correct and incorrect data
- no real-world understanding, just patterns from what’s available on the internet
- confidence level not provided in output

LLMs just try to predict the text, no real world understanding.

Don’t trust LLM/RAG, provide facts/list of sources.

### 3.3 Adversarial Attack and HITL

Adversarial Example:

- Modifying example/training data (Stop sign vs Speed Limit 40 after few modifications to original stop sign image)

Mitigation Techniques:

- Add HITL (Human in The Loop) for critical AI workflows.
- Technical Techniques:
  - Adversarial Training
  - Ensemble Models - check consensus (similar to blockchain)

HITL Claude Usage Policy:

- When using products/services, should have qualified professional to review content/decision:
  - Legal
  - Healthcare
  - Finance
  - Journalism
  - Cybersecurity

### 3.4 Agentic AI

- agents can take actions on behalf of user, in multiple steps. (zero shot vs multiple shot)
- multiple agents (with distinct role) can collaborate to do more complex tasks
- AI agents can behave like employees/teammates

AI Stack:

- Semiconductors
- Cloud Infrastructure
- Foundational Models
- Agentic Orchestration Layer (Harness?)
- Applications

Agentic Design Patterns:

- Reflection
- Tool Use (includes web browser, dynamic code generation, etc.)
- Reasoning / Planning (multi-shot)
- Multi-Agent Collaboration

MCP, proposed by Anthropic.

- Interact with tools and repositories/applications

A2A Protocol, proposed by Google.

- Secure Collaboration
- Task and State Management
- UX Negotiation
- Capability Discovery

## Module 4: Agentic AI Risks

### 4.1 Agentic AI Risks

Shadow AI:

- build central inventory of AI systems used
- AI BOM (Bill of Materials)

AI Agent Risks: Top 10 OWASP

1. Authorization and Control Hijacking
2. Critical Systems Interaction
3. Goal and Instruction Manipulation
4. Impact and Blast Radius
5. Memory and Context Manipulation
6. Orchestration and Multi-Agent Exploitation
7. Supply Chain and Dependency Attacks
8. Untraceability
9. Checker “out-of-the-loop” Vulnerability
10. Alignment Faking Vulnerability

### 4.2/3 Jailbreaks Part 1/2

**Jail** - set of rules that constrain a system’s behavior

**Jailbreak** - user works around the rules to have the system behave in a way that’s outside the original rules

Types of Jailbreaks:

- Encoding/Obfuscation
- Payload Splitting
- Refusal Suppression
- Role Playing
- Authority Spoofing
  - trick/socially engineer AI models
- Etc.

### 4.4 Prompt Injection

- direct
  - similar to SQL injection
  - user input to prompt
- indirect
  - agent might read emails, search websites, etc. with malicious prompts

Use HITL for agents that will do sensitive actions.

## Module 5: Breaches on and with AI

### 5.1 Model Extraction and Distillation

#### Model Extraction

- training models can cost hundreds of millions of dollars.
- attacker steals model by querying the model enough times
  - Carlini (2020) - exponential number of queries (relative to number of neurons on the network)
  - Shamir (2024) - polynomial number of queries

#### Model Distillation

- student model (DeepSeek) learns from teacher model
- jailbroken DeepSeek responds with using OpenAI as teacher model.

### 5.2 Model Leakage

- Mistral model leaked from customer uploading to HuggingFace from USB stick.
- ChatGPT: Some users see other users’ prompts. In-memory DB, race conditions, DB connection not reset.

### 5.3 Attacks on AI Agents

#### SalesForce ForcedLeak (2025)

- researcher exfiltrated CRM data
  - LLM trust boundary flaw: no separation between trusted instructions and untrusted data
  - one domain expired.
- Prevent by sanitizing input from untrusted sources, least privilege for agent

#### SalesForce PipeLeak (2026)

- Silent exfiltration of CRM data to attacker-controlled addresses
- Prevent by adding allowlist of emails, prevent data exfiltration

### 5.4 Attacks with AI Systems

- adversary uses AI as part of an attack

#### $25M Video Call (2024)

- Target finance employee at Arup
- Phishing email lured to fake Zoom call
- Call included real colleagues plus deepfaked CFO
- Deepfake CFO approved $25M wire transfer
- Employee authorized 15 transfers to multiple accounts

#### Anthropic AI agent used to attack and breach companies

- automated 80-90% of attacks

#### Vulnerability Discovery via LLM and AI

- Google Big Sleep
- Claude Mythos

## Module 6: AI Governance and Regulation

### 6.1 AI Governance Frameworks

- ISO 42001
  - AIMS (Artificial Intelligence Management System)
  - Anthropic certified
  - Complementary to ISO 27001, SOC2, PCI, HIPAA, etc.
- Google SAIF (Secure AI Framework) / CoSAI
  - address AI-specific risks
    - model theft
    - training data poisoning
    - prompt injection
    - extraction of confidential information from training data
  - Risk Map
    - Data
    - Infrastructure
    - Model
    - Application
  - Donated framework to CoSAI (Coalition for Secure AI)

### 6.2 Technical Threats and Agent Controls

- BIML-78 (Berryville Institute of Machine Learning) Risks
  - 78 security risks
  - Extended to 81 risks specific to LLMs
  - LLMs are black boxes, hard to trace back risks.
  - top 10 and 23 critical foundational model risks, harmful model behavior can occur without adversarial prompting
- AIUC-1 (AI Agent Safety, Security, and Reliability)
  - standard for AI agents
  - enterprise risk dimensions
    - security
    - safety
    - reliability
    - accountability
    - data and privacy
    - societal risk
  - technical testing, audits of AI policies and operational guardrails
  - standard updated quarterly, with contributions from Stanford, MIT, MITRE, Cisco, Cloud Security Alliance

### 6.3 AI Regulation: FTC and EU AI Act

#### FTC questions

- clear and accurate claims and disclosures
  - are you exaggerating what your AI product can do?
  - are you promising that your AI product does something better than a non-AI product?
  - does the product use AI at all?
  - are you aware of the risks?

#### EU AI Act

- applies to developers, deployers, distributors, and importers
  - providers based outside EU:
    - if system available on EU market
    - output generated is used in the EU
- Risk-based approach

### 6.4 AI State Legislation and Federal Orders

- Colorado Anti-Discrimination in AI Act
  - first passed dedicated AI law
  - High Risk AI Systems
    - education, employment, financial, lending, healthcare, etc.
  - June 2026
- CA AI Training Data Transparency Act (AB 2013)
  - Transparency on data sources, total volume, IP status
- CA Frontier AI Act (SB 53)
  - requires safety frameworks and incident reporting for high-compute models
- AI Transparency Act (SB 942)
  - watermarking and detection tools for AI-generated content by August 2026
- Executive Order 14365
  - National framework, prevent/dissuade states from passing onerous legislation, wanting American AI to win against Chinese AI.

### 6.5 Summary

- A lot of things that can go wrong with AI, lots of vulnerabilities
- Lots of laws and regulations being passed.
- Want to move fast, but moving fast without mitigating risks, will have to slam brakes.
  - German Autobahn can go as fast as they want, small set of well-designed rules.

## Conclusion

- Historical breach root causes still applicable, and amplified by AI
- AI increases the threat surface, adversaries weaponize it, AI systems are high-value targets
- Examples of Threats:
  - prompt injection
  - model extraction
  - Shadow AI
- Standards and Regulations, governance and regulatory frameworks
  - ISO 42001
  - SAIF
  - AIUC-1
  - EU AI Act
  - SB 53
- Speed is the goal, but safety infrastructure must be built before you open the throttle, otherwise, you may need to slam the brakes

> “There is no arrival. There is no flying saucer. The technology is already embedded in infrastructure, already answering customer service queries and drafting legal briefs and writing code and conducting espionage campaigns.” - Neil Daswani (AI Attacks)

## Faculty Spotlight - Dr. Junfeng Yang, PhD

### Part 1: Introduction to Professor Yang’s Research

- hardening AI systems
- defeating AI-powered attacks
- using AI to solve classic security problems

Interview:

- started PhD research in 2001
- professor in 2015
- Use AI more, learn more of AI’s weaknesses, know distinction when to trust AI answers, when to take AI answers with a grain of salt.

#### References

- Machine unlearning: Y. Cao and J. Yang, “Towards Making Systems Forget with Machine Unlearning,” 2015 IEEE Symposium on Security and Privacy, San Jose, CA, USA, 2015, pp. 463–480, doi: 10.1109/SP.2015.35. <https://doi.org/10.1109/SP.2015.35>
- AI supply chain – model loading: R. J. Sofaer, Y. David, M. Kang, J. Yu, Y. Cao, J. Yang, and J. Nieh, “RogueOne: Detecting Rogue Updates via Differential Data-flow Analysis Using Trust Domains,” Proceedings of the IEEE/ACM 46th International Conference on Software Engineering (ICSE ‘24), Lisbon, Portugal, 2024, Article 101, doi: 10.1145/3597503.3639199. <https://doi.org/10.1145/3597503.3639199>
- AI supply chain – compiler backdoors: S. Chen, J. Peng, Y. He, J. Yang, and B. Ray, “Your Compiler is Backdooring Your Model: Understanding and Exploiting Compilation Inconsistency Vulnerabilities in Deep Learning Compilers,” arXiv:2509.11173, 2025. <https://doi.org/10.48550/arXiv.2509.11173>
- Jailbreaking via diversified attacks: W. Zhao, D. Ben-Levi, W. Hao, J. Yang, and C. Mao, “Diversity Helps Jailbreak Large Language Models,” arXiv:2411.04223, 2024. <https://doi.org/10.48550/arXiv.2411.04223>
- AI-generated text detection: C. Mao, C. Vondrick, H. Wang, and J. Yang, “Raidar: geneRative AI Detection viA Rewriting,” arXiv:2401.12970, 2024. <https://doi.org/10.48550/arXiv.2401.12970>
- AI-generated video detection: Q. Liu, P. Shi, Y.-Y. Tsai, C. Mao, and J. Yang, “Turns Out I'm Not Real: Towards Robust Detection of AI-Generated Videos,” arXiv:2406.09601, 2024. <https://doi.org/10.48550/arXiv.2406.09601>
- AI-generated audio detection: Z. Zhang, W. Hao, A. Sankoh, W. Lin, E. Mendiola-Ortiz, J. Yang, and C. Mao, “I Can Hear You: Selective Robust Training for Deepfake Audio Detection,” The Thirteenth International Conference on Learning Representations (ICLR), 2025. <https://doi.org/10.48550/arXiv.2411.00121>
- Real-world AI-generated phishing/spam study: W. Hao, V. Tran, V. Rideout, Z. Wang, A. Dasbach-Prisk, M. H. Afifi, J. Yang, E. Katz-Bassett, G. Ho, and A. Cidon, “Do Spammers Dream of Electric Sheep? Characterizing the Prevalence of LLM-Generated Malicious Emails,” Proceedings of the 2025 ACM Internet Measurement Conference (IMC ‘25), 2025, doi: 10.1145/3730567.3732922. <https://doi.org/10.1145/3730567.3732922>

### Part 2: Columbia Engineering Industry Collaborations

- big tech sponsoring research
- university main goal is cutting-edge research that can be disseminated, publish research papers.
- donations are “no strings attached”.
- Sponsored research project: specific problem, private data protection if included in research.
- Focus on impact, results (PhD journey)

### Part 3: Deep Dive into AI Jailbreaking

- red teaming before AI agent deployment
- safety training, safety rules in jail, attackers try to break jail
- to find jailbreaking prompts, hire security engineers (old, traditional, costly, slow)
  - more automated techniques, use another LLM to jailbreak main LLM
  - dagger tool
    - local synonym swaps
    - global diversification changes
- post deployment, guardrails

### Part 4: Detecting AI Generated Content

- security in general is not about being perfect, security is about raising the bar, creating more friction for the attackers to launch attacks
- defense-in-depth, detecting signals, used along with other systems
- humans have individuality, creativity, AI predicts the next token based on training data
- AI security is not purely academic, has a lot of connections to production AI agents. Tied to day-to-day operations, specific business use cases.
