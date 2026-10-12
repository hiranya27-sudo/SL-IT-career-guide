# Skill-to-Role Mapping and Data Analysis

## 1. Objective

This document defines the initial skill taxonomy and maps common IT roles to required competencies. It supports the recommendation logic for the career guidance system.

## 2. Core Skill Categories

The system will evaluate users across the following categories:

- Programming Fundamentals
- Web Development
- Databases
- Networking and Systems
- Data Analysis / Data Science
- Cybersecurity
- Cloud and DevOps
- UI/UX Design
- Software Testing
- Problem Solving and Communication

## 3. Career Roles and Skill Focus

### 3.1 Software Engineer

Key skills:

- programming
- data structures
- web development
- databases
- problem solving
- testing

### 3.2 Web Developer

Key skills:

- HTML/CSS/JavaScript
- frontend frameworks
- backend development
- APIs
- database usage
- UI/UX awareness

### 3.3 Data Analyst

Key skills:

- Excel / data tools
- SQL
- statistics
- data visualization
- problem solving
- communication

### 3.4 Data Scientist

Key skills:

- Python/R
- machine learning
- statistics
- data cleaning
- analytics
- experimentation

### 3.5 Cybersecurity Analyst

Key skills:

- networking
- security fundamentals
- operating systems
- scripting
- ethical hacking awareness
- risk analysis

### 3.6 QA Engineer

Key skills:

- testing concepts
- documentation
- bug analysis
- automation basics
- communication
- software understanding

### 3.7 Cloud / DevOps Engineer

Key skills:

- Linux
- cloud platforms
- automation
- networking
- scripting
- CI/CD and deployment

### 3.8 UI/UX Designer

Key skills:

- design thinking
- prototyping
- user research
- visual design
- wireframing
- usability

### 3.9 Network Engineer

Key skills:

- networking
- troubleshooting
- routing/switching
- security basics
- system administration

### 3.10 IT Support Specialist

Key skills:

- troubleshooting
- customer communication
- operating systems
- hardware and software support
- documentation
- problem solving

### 3.11 Database Administrator

Key skills:

- SQL
- database design
- backup and recovery
- performance tuning
- data security
- indexing and query optimization

### 3.12 Project Manager

Key skills:

- project management
- leadership
- communication
- risk management
- time management
- stakeholder coordination

### 3.13 Business Analyst

Key skills:

- requirement gathering
- process analysis
- stakeholder communication
- business logic
- documentation
- data interpretation

### 3.14 Systems Administrator

Key skills:

- operating systems
- networking
- scripting
- troubleshooting
- system monitoring
- security fundamentals

### 3.15 Mobile App Developer

Key skills:

- mobile programming
- UI/UX for mobile
- API integration
- app testing
- database connectivity
- performance optimization

### 3.16 AI / Machine Learning Engineer

Key skills:

- Python
- machine learning
- statistics
- data preprocessing
- model evaluation
- deployment basics

### 3.17 IT Consultant

Key skills:

- technology advisory
- business analysis
- communication
- problem solving
- project management
- strategic thinking

### 3.18 System Analyst

Key skills:

- requirements analysis
- system design
- process mapping
- technical documentation
- SQL
- communication and problem solving

## 4. Recommendation Logic Idea

A simple weighted matching approach can be used:

- Each user rates their skill level from 1 to 5.
- Each role has required skill weights.
- The score for a role is calculated as:

  role_score = sum(skill_level × weight)

- The system ranks roles by score.
- A skill gap is identified where user_skill < required_skill.

## 5. Example Role Weight Table

| Role                           | Programming | Web Dev | Database | Networking | Data/Analytics | Security | Design | Testing |
| ------------------------------ | ----------- | ------- | -------- | ---------- | -------------- | -------- | ------ | ------- |
| Software Engineer              | 5           | 4       | 4        | 2          | 2              | 2        | 1      | 3       |
| Web Developer                  | 4           | 5       | 4        | 2          | 1              | 1        | 3      | 2       |
| Data Analyst                   | 2           | 2       | 4        | 1          | 5              | 1        | 1      | 1       |
| Data Scientist                 | 4           | 1       | 3        | 1          | 5              | 1        | 1      | 1       |
| Cybersecurity Analyst          | 3           | 1       | 2        | 5          | 2              | 5        | 1      | 2       |
| QA Engineer                    | 2           | 2       | 2        | 1          | 1              | 2        | 1      | 5       |
| Cloud/DevOps Engineer          | 3           | 2       | 3        | 4          | 1              | 3        | 1      | 2       |
| UI/UX Designer                 | 1           | 3       | 1        | 1          | 1              | 1        | 5      | 1       |
| Network Engineer               | 2           | 1       | 1        | 5          | 1              | 3        | 1      | 1       |
| IT Support Specialist          | 1           | 1       | 2        | 4          | 1              | 2        | 1      | 3       |
| Database Administrator         | 2           | 1       | 5        | 2          | 2              | 3        | 1      | 1       |
| Project Manager                | 1           | 1       | 2        | 1          | 2              | 1        | 1      | 2       |
| Business Analyst               | 2           | 1       | 3        | 1          | 4              | 1        | 1      | 2       |
| Systems Administrator          | 2           | 1       | 2        | 4          | 1              | 3        | 1      | 2       |
| Mobile App Developer           | 4           | 3       | 3        | 1          | 1              | 1        | 3      | 2       |
| AI / Machine Learning Engineer | 5           | 1       | 3        | 1          | 5              | 1        | 1      | 1       |
| IT Consultant                  | 2           | 1       | 2        | 2          | 2              | 1        | 1      | 2       |
| System Analyst                 | 2           | 2       | 3        | 2          | 3              | 1        | 1      | 2       |

## 6. Data Analysis Notes

- The role taxonomy should remain flexible and expandable.
- Skills should reflect both technical and soft skills, since IT careers depend on communication and problem solving.
- The system should emphasize student-friendly results instead of highly advanced role complexity.
- Local relevance should be improved by adapting role names and skill priorities to the Sri Lankan job market context.

## 7. Proposed Future Enhancements

- Add local salary and demand indicators.
- Include preferred job sectors (e.g., fintech, software, telecom, government, startups).
- Add personality or interest-based filtering.
- Add adaptive recommendation logic using actual user responses over time.

## 8. Week 3–4 Outcome

The project now has a base requirement specification and an initial skill-role matrix. This is the foundation for system design and recommendation engine implementation in the next phase.
