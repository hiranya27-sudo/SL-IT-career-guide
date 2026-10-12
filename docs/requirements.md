# Requirements Specification

## 1. Project Overview
The Sri Lankan IT Career Guide helps users choose a suitable IT career path by evaluating their current skills, interests, and academic background. The system compares this information to common IT job roles in Sri Lanka and highlights missing skills and recommended next steps.

## 2. Problem Statement
Students and graduates often struggle to decide which IT career path matches their ability and interest. Many do not know which skills are required for different roles, and they are unaware of how their current knowledge compares with the local job market.

## 3. Target Users
- Undergraduate students
- Recent graduates
- Career seekers in Sri Lanka
- Academic advisors and career counselors

## 4. Functional Requirements
### FR1: User profile creation
The system shall allow users to create a profile with:
- name
- academic level
- specialization or field of study
- interests
- experience level
- preferred career areas

### FR2: Skill assessment
The system shall let users rate their knowledge in key skill areas such as:
- programming
- databases
- networking
- web development
- data analysis
- cybersecurity
- cloud computing
- UI/UX design
- testing
- problem solving

### FR3: Career recommendation
The system shall compare the user profile and skills with defined IT career roles and recommend the most suitable role(s).

### FR4: Skill-gap analysis
The system shall identify missing or weak skills required for the recommended career path and present them in a clear summary.

### FR5: Learning roadmap
The system shall suggest a learning or skill-building path to help the user improve toward a target career.

### FR6: Career insights
The system shall present simple career insights such as:
- estimated job-fit score
- strongest career matches
- skill strengths
- recommended next actions

## 5. Non-Functional Requirements
### NFR1: Usability
The interface should be easy for students and graduates to use without technical expertise.

### NFR2: Performance
The recommendation should be generated quickly after the user submits assessment data.

### NFR3: Maintainability
The system should allow future expansion to add more roles, skills, and scoring rules.

### NFR4: Scalability
The system should accommodate more users and more career categories as the project grows.

### NFR5: Reliability
The recommendation logic should be consistent and produce valid results for different user inputs.

## 6. Business/Project Requirements
- The system should be relevant to the Sri Lankan IT market.
- The recommendation engine should support common local career pathways.
- The design should be practical and suitable for an undergraduate final-year project.

## 7. User Stories
- As a student, I want to assess my skills so I can understand which IT career suits me.
- As a graduate, I want to see my skill gaps so I can plan my learning.
- As a counselor, I want to view recommended career paths so I can guide students better.

## 8. Assumptions
- The project will begin with a rule-based or scoring-based recommendation model.
- Career roles will be represented using a set of common skills and weights.
- Initial data can be based on local job market trends and common academic pathways.

## 9. Deliverables for Weeks 3–4
- Requirements document
- Skill model and role taxonomy
- Sample data structure for recommendation logic
- Initial project structure and documentation
