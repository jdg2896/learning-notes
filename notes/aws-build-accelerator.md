# AWS Build Accelerator

Notes from the AWS Build Accelerator program for early-stage startups during my time with P33R Finance.

## Key Takeaways

- Leverage existing solutions for non-core pieces.
  - Authentication
  - Serverless
- Focus and scope the MVP

## 1 - Customers and Front-end

- Understand your customers
  - It's easier to make things people want than to make people want things
  - Insights, inferred
    - Survey tools
    - Customer interviews
    - Focus groups
    - A/B tests
  - Customer persona
    - Who are our customers?
    - What are their pain points?
    - Why are they trying to solve the pain?
    - How can we help them?
  - You're not selling, you're solving
  - UVP (Unique Value Proposition)
    - We help X do Y by doing Z
    - Focus on benefits, and reinforce with features
- Front-end development
  - Considerations
    - Start with an MVP
    - Build vs buy
      - Leverage existing tools/libraries
    - Avoid scope creep
  - Frameworks
    - Monolith
    - SPA
  - Best practices
    - Responsive, mobile-first design
    - Build for a global/diverse audience
    - Localization
    - TDD
      - Manual
      - Unit tests
      - Integration tests
      - End-to-end tests
    - Code
      - Tag commits
      - Code reviews
      - CI/CD
  - Testing
    - UX testing
    - Beta testing
    - A/B tests
  - Launches
    - Monitoring
      - What metrics to track (crucial)
      - Success metrics for features
    - CI/CD and versioning
  - Every line of code you write becomes technical debt
  - Iterate towards an MLP (Minimum Lovable Product)
    - Customer feedback
    - Allocate time to address issues
  - Aim for iteration, not perfection
  - Automate repetitive tasks

## 2 - Backend

### Backend Architecture

- Agility: innovation flywheel
  - New ideas
  - Experiment
  - Feedback and improvements
- Capability
  - Talent
  - Tools
  - Tech
- Workload: requirements

### Architectures

- Monolithic
- Microservices

### Modes of Compute

- VMs
- Containers
  - Data processing
  - App development
  - AI/ML
  - CI/CD
- Serverless
  - Event-driven
  - Unpredictable demand
  - IT automation
  - Data/stream processing
  - Web/mobile backends
  - IoT

## 3 - Security

### Common Identity Attacks

- Credential stuffing
- Man in the Middle (MITM)
- Phishing
- Brute force
- Dictionary
- Keylogger
- Password spraying

### Best Practices

- **Use trusted partners**
  - Leverage a 3rd-party provider for authentication and customer management
- **Encrypt everything (in transit and at rest)**
  - HTTPS/TLS
- **Scaling profile**
  - B2C
  - B2B
- **Access and permissions**
  - Audit logging
  - Separate employees from customer-facing apps
- **MFA**
  - Ease of integration
  - Pricing
  - Security
- **Associate everything to a user**
  - Understand how data relates to the user
  - GDPR
  - Auditing, logging, troubleshooting
- **API access**
  - Lifespan of credentials
    - Temporary
    - Long-lived
  - Recommended to not have long-lived credentials
- **Authorization and authentication**
  - Authentication
    - Login
  - Authorization
    - Roles
    - Permissions
- **Machine to machine communication**
  - Mutual TLS
  - Client credentials
- **Social logins**
  - Simplify registration and login

### Common Security Use Cases

- **End-user management**
  - Use an external provider
  - Secure and limit PII data
  - Use MFA
- **Employee management**
  - Separate employees from customers
  - Centralize employee data
  - Use separate back-office interfaces
  - Require MFA
- **Authorization for users**
  - RBAC
  - Login and auditing
  - Conduct periodic security reviews and penetration testing

### Services for a Secure Startup

- AWS
  - Cognito
- Other
  - Auth0
  - Okta
  - OneLogin
  - Clerk

Data security is part of the user experience.

## 4 - Customer Empathy

### Customer Empathy

- Customer voice
  - Reflect their voices in products
- Different types of customer interactions
  - Wow factor
  - Impulse click: frictionless buying
  - Meet customers where they're at
    - Customers have slow internet? Use mobile? Etc.
  - Convert unsatisfied customers into loyal customers
    - Promptly acknowledge customer feedback
    - Make every interaction personal
    - Help make it right (refunds, offers, etc.)

### Scaling Customer Interactions

- Be adaptable and iterate as needed
- Scale customer interaction channels
  - Chatbots
  - Cloud-based call center
  - Notifications (push, SMS, email)
  - Social channels

#### Chatbots (Amazon Lex)

- Realtime support
- Handle basic queries
- Personalize
- Maintain a conversational tone
- Iterate based on customer feedback and usage patterns

#### Omnichannel Communication (Amazon Connect)

- Seamless and consistent customer experience across all platforms
  - Phone
  - Email
  - Social media
  - Live chat
- Define a clear vision of how to interact with customers at different touchpoints

#### Realtime Text/Push Notifications (Amazon Pinpoint)

#### Email (Amazon SES)

#### Social Media (Amazon Kinesis Data Firehose, Amazon Comprehend)

- Faster brand recognition
- Customers connect with each other
- Integrate social media and websites
- AI-driven social media dashboard

### Capturing Customer Feedback

- Positive feedback
  - Can be published as customer testimonials (with permission)
  - Builds credibility and trust
- Negative feedback
  - Opportunity to learn, adapt, and adjust your approach to better meet customer expectations
- Different tools give different types of feedback
  - Trustpilot
  - Yelp
  - Zendesk
- Well-crafted surveys
  - SurveyMonkey
  - Typeform
- Convenience is key
  - Make it easy for customers to provide feedback

## 5 - Scalable Architecture

### Building Scalable Distributed Architectures

#### Loosely Coupled vs Tightly Coupled

- If a process can be async, decouple it

#### Orchestration vs Choreography

- **Orchestration**
  - actions in a specific order
  - Saga pattern
    - undo each step after a failure
    - Step Functions
- **Choreography**
  - independent microservices
  - services can be independent from each other
  - event broker
    - Kinesis Data Streams

#### Queueing and Event-Driven Architecture

- SQS
- EventBridge
- SNS

## 6 - Database

### Modern Application Requirements

- Performance
- Scale
- Availability

### Best Practices

1. Understand app requirements
   - functional
   - non-functional
2. Define your Entity-Relationship Diagram
3. Write down your data access patterns
4. Model your primary key structure
5. Fulfill secondary access patterns
6. Experiment and optimize as needed
7. Choose a data store and implement a gateway

### Database Dimensions and Data Models

#### Data Dimensions

- **Shape**
  - Tabular
  - Key-value
  - Document
  - Graph
- **Size**
  - Partitions
- **Compute**
  - Throughput
  - Latency
  - Processing capabilities
    - CPU-intensive
    - Memory-intensive

#### Data Model

- Scaling a relational DB
  - Scaling up: vertical scaling
  - Scaling out: horizontal scaling
- Federation
- Sharding
- Purpose-built DBs

## 7 - Best Practices

- Build something functional that adds value to customers, especially for early-stage startups
  - Don't over-engineer or over-innovate
  - Adopt the right tools for the job
- Software engineers are hired to unlock business value, not to solve cool problems. Being able to do both is better.

### Engineering Decisions

- Practice making decisions
  - Document wins and failures

#### Version Control

- How do you manage the growing number of versions?
- Use a VCS and GitHub

#### Code Organization

- CI/CD
  - Test automation

### Common Engineering Situations

- Hosted source control
- Use AI-assisted tools responsibly
- Avoid knowledge silos
  - Spread knowledge to multiple developers
  - Use RFCs (Request for Comments)
  - Use ADRs (Architecture Decision Records)
- Specialist vs generalist
  - Generalists in early-stage startups
  - Specialists in later-stage startups

### Potential Services

- There's no one-size-fits-all solution
- There are no silver bullets

## 8 - Gen AI

- AI/ML and the benefits of Gen AI
- Defining your Gen AI use case
- Selecting the right foundation model
- Exploring Gen AI services

## 9 - Leveraging Vendors

### Build vs Buy

- Don't reinvent the wheel
- Reduce risk by using an existing solution

### Become a Great Buyer

- **Operational Excellence**: consider differentiation, switching cost, and criticality
- **Security**: consider compliance attestations in the short to long term
- **Reliability**: consider reputation, funding, and existing traction
- **Performance**: consider product use patterns, frequency of need, scalability
- **Cost Efficiency**: consider vendor costs in your pricing model

## 10 - Innovating Iteratively Post-Launch

### Objectives

- Understand the significance of **customer service** in your software business.
- Collect and synthesize **customer feedback** to create a product roadmap.
- Identify the mechanisms to incorporate the right **customer metrics** at scale.

### Emphasis on Service and Customer Experience

- Frictionless onboarding
- Time to value
- Loyalty and community

### Agility and Operational Efficiency

- **Build**: core product or feature
- **Test**: test with customers and get feedback
  - surveys
  - focus groups
  - behavior analysis
- **Iterate**

### Key Areas to Focus on When Building

- Are you building the right thing?
- Are you building it the right way?
- Are you operating it the right way?

### Are You Building the Right Thing?

#### Business Growth and Customer Success

- Double down on **working features**.
- Cut losses elsewhere.

#### Product Development and Customer Feedback

- Identify customers
  - Narrow down the customer persona
- Collect data from social media

#### Sales and Marketing and Customer Discovery

- Customer feedback can give you ideas
- Look at sources of data

#### Check-in

- Do you have a mechanism or process to collect feedback?
- Do you review customer feedback when building the product roadmap?
- Do you review support tickets when building the product roadmap?

### Are You Building It the Right Way?

- Impact on engineering workload
- Design for cost optimization
- Create self-powering feedback loops

#### Check-in

- Can your users report product issues and feature requests?
- Can you attribute feature usage patterns at the customer level?
- Can you attribute infrastructure costs at the customer level?

### Are You Operating It the Right Way?

- Systematize root cause analysis
  - think of disruptive solutions
- Feedback for operational control
  - availability
  - mean time to detect issues
  - mean time to fix issues
  - failed deployments
- Unit economics should remain stable

#### Check-in

- Are you providing free-form feedback options in your SaaS application?
- Do you have a repository of feedback that you look into during roadmap building?

### Key Takeaways

- Don't forget the "service" in software-as-a-service
- Prioritize customer agility and promote active customer feedback loops
- Operating the software application is a business function
- Incorporate cost optimization and feedback collection during design
- Create mechanisms to review costs and customer feedback
