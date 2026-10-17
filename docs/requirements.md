# Requirements Specification

## 1. Project overview

The Sri Lankan IT Career Guide is a decision-support system that helps students, graduates, and job seekers explore IT career paths using their skills, academic background, interests, and experience. It compares a user's self-assessment with a catalog of IT roles, explains the strongest matches, identifies skill gaps, and suggests learning steps. Recommendations are guidance, not a guarantee of employability.

## 2. Problem statement

Many students and graduates in Sri Lanka are unsure which IT career paths align with their current abilities and interests. They may also lack a clear understanding of the competencies associated with different roles and how to develop them. The system addresses this by providing understandable, explainable recommendations and role-based learning guidance.

## 3. Project goals

- Help users explore suitable IT career paths.
- Compare current self-assessed proficiency with role requirements.
- Highlight strengths and missing or underdeveloped skills.
- Suggest a structured learning path.
- Keep role information relevant to the Sri Lankan IT market.

## 4. Target users

- Undergraduate students
- Recent graduates
- IT job seekers
- Academic advisors and career counselors
- People exploring technology careers

## 5. Scope

The initial version will use a rule-based weighted scoring model, a curated role catalog, and a shared skill catalog. It will support profile assessment, explainable role matching, skill-gap analysis, and learning guidance.

Out of scope for the initial version:

- Social login or user authentication
- Live job-board integration
- Machine-learning recommendations trained on user data
- Large-scale enterprise deployment

## 6. Functional requirements

### FR1: User profile creation

The system shall collect the profile fields needed for recommendations:

- Academic level
- Field of study or specialization
- Interests
- Experience level
- Preferred career categories

A name shall be optional and shall not affect recommendation scores.

### FR2: Skill assessment

The system shall let users assess the canonical skills in the shared skill catalog using an integer scale from 1 to 5. The interface shall show the meaning of every scale point:

| Level | User-facing description |
| --- | --- |
| 1 | No practical knowledge yet |
| 2 | Beginner: understands basic concepts or can complete simple tasks with guidance |
| 3 | Developing: can complete common tasks with some guidance |
| 4 | Proficient: can complete common tasks independently |
| 5 | Advanced: can solve complex tasks and explain or guide others |

Users may leave a skill unanswered. Unanswered skills shall be represented as missing data, not as level 0 or level 1. The interface shall distinguish “not assessed” from “assessed as level 1.”

### FR3: Role and skill catalog management

The system shall maintain a shared skill catalog and a role catalog. Each skill shall have a stable canonical ID, display name, and category. Each role shall have a name, category, description, and required skills. Every role-skill entry shall store separately:

- `required_level`: expected proficiency, integer 1–5
- `importance_weight`: relative contribution to that role, integer 1–5

All IDs referenced by roles shall exist in the skill catalog. Catalog additions or edits shall not require changes to the scoring formula.

### FR4: Career recommendation

For each role, the system shall calculate:

- **Readiness score:** weighted proficiency attainment as a percentage from 0 to 100.
- **Assessment coverage:** the percentage of that role's total importance weight for which the user supplied a valid rating.

For an answered skill `s`, attainment is `min(user_level_s, required_level_s) / required_level_s`. Readiness is the weighted mean of attainment over answered role skills, multiplied by 100. Skills rated above the role's required level are capped at full attainment.

Coverage is `sum(importance_weight for answered role skills) / sum(importance_weight for all role skills) * 100`.

The system shall rank only roles with at least 70% assessment coverage. Roles below that threshold shall be marked “insufficient assessment” and shall not be presented as fully comparable recommendations. It shall show up to five eligible matches, sorted by readiness score descending and then role name alphabetically for ties.

Each match shall include its readiness score, assessment coverage, strongest contributing skills, and the skills with the largest gaps. Scores are estimates based on self-reported skills, not predictions of hiring outcomes.

### FR5: Skill-gap analysis

For an assessed skill below the role's required level, the system shall show the current level, required level, and gap (`required_level - user_level`). An unanswered required skill shall be shown as “not assessed,” not as a confirmed gap. Skills meeting or exceeding the required level shall be identified as strengths.

### FR6: Learning roadmap

The system shall use identified skill gaps to suggest learning topics, milestones, or next actions in a logical order. Roadmap items shall be associated with a skill and a target role. An unassessed skill shall prompt assessment before the system treats it as a learning gap.

### FR7: Career insights

The system shall present:

- Eligible career matches and readiness scores
- Assessment coverage for each match
- Skills that contribute most strongly to each match
- Assessed strengths and skill gaps
- Recommended next actions

If no role reaches the assessment-coverage threshold, the system shall explain that more assessment answers are needed and identify the relevant unanswered skills.

### FR8: Extendability

The system shall support adding roles, skills, and scoring rules without major redesign. Catalog validation shall detect unknown skill IDs and out-of-range levels or weights before recommendation calculation.

## 7. Non-functional requirements

### NFR1: Usability

Assessment labels and result explanations shall be understandable to students and graduates without specialist knowledge.

### NFR2: Performance

On the target development environment, calculating recommendations for one profile against up to 100 roles and 100 skills shall complete within 2 seconds, excluding network latency.

### NFR3: Maintainability

The skill catalog, role catalog, and scoring logic shall be separated. Role or skill data changes shall not require rewriting the scoring formula.

### NFR4: Scalability

The data model shall permit additional roles, skill categories, and profiles without changing the role-skill representation.

### NFR5: Reliability

Identical valid assessment data and catalog versions shall produce identical scores, coverage, rankings, and gap results. Invalid ratings shall produce a visible validation error and shall not be silently converted into a score.

### NFR6: Relevance

Role data shall be reviewed for practical IT careers and Sri Lankan market expectations. Unvalidated role levels and importance weights shall be identified as provisional.

## 8. Business and project requirements

- Recommendations should support common career pathways in Sri Lanka.
- The MVP should be understandable and feasible as an undergraduate final-year project.
- Results should explain their basis and limitations.
- The system should be useful as an MVP while remaining open to future improvement.

## 9. User stories

- As a student, I want to assess my skills so I can explore IT careers that may suit me.
- As a graduate, I want to see assessed strengths and skill gaps so I can prioritize learning.
- As a counselor, I want to review suggested career paths so I can support students.
- As a job seeker, I want a recommendation that reflects my current experience and interests.

## 10. Assumptions

- The first recommendation model will be rule-based and explainable.
- Role requirements and importance weights will be curated and reviewed, rather than inferred from user data.
- User skill ratings are self-reported and are not formal certifications.
- Initial role data will be based on common IT careers and expectations relevant to Sri Lanka.

## 11. Acceptance criteria for the recommendation MVP

- Accept integer skill ratings from 1 through 5; reject values outside that range and non-integer values with a visible validation message.
- Preserve unanswered skills as missing; never silently treat them as level 0 or 1.
- Produce a 0–100 readiness score and 0–100 coverage value for each role with at least one answered required skill.
- Exclude roles with less than 70% coverage from the ranked recommendation list and identify them as insufficiently assessed.
- Return no more than five eligible roles in deterministic order.
- For every returned role, show score, coverage, assessed strengths, gaps with current and required levels, and unanswered required skills separately.
- With no eligible role, explain why and list unanswered assessment skills needed to reach sufficient coverage.
- Repeated runs using the same profile and catalog produce identical output.
- Complete the scoring calculation within 2 seconds for up to 100 roles and 100 skills in the target development environment.

## 12. Initial project deliverables

- Requirements specification
- Canonical skill catalog
- Role-to-skill dataset with separate proficiency requirements and importance weights
- Recommendation scoring and validation logic
- Documentation of the model, assumptions, and limitations
