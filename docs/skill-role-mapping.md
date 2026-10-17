# Skill-to-Role Mapping and Recommendation Model

## 1. Purpose and source of truth

This document describes how the career guide's role data is represented and used. The canonical skill IDs, display names, categories, and role-to-skill mappings are maintained in [`../data/it_career_roles.json`](../data/it_career_roles.json). Role data must reference those IDs exactly; assessment labels should use the catalog display names rather than introducing alternative IDs.

Use lowercase `snake_case` IDs that remain stable if a display name changes. Similar-sounding skills remain separate when they describe different abilities, such as `databases` and `sql`, or `cloud_computing` and `linux`.

## 2. Role-skill fields

Each role's `required_skills` map uses a canonical skill ID and stores two separate values:

| Field | Meaning | Allowed values |
| --- | --- | --- |
| `required_level` | Proficiency expected for the role | Integer 1–5 |
| `importance_weight` | Relative influence of the skill on that role | Integer 1–5 |

These values answer different questions: a skill can have a high expected proficiency but moderate relative importance, or vice versa. Initial role levels are migrated from the existing role data. The starter importance weights are set to 1 because the previous data did not distinguish importance from proficiency; weights should be adjusted only after validation with role descriptions, local job evidence, or stakeholders. These initial values are provisional, not measured labor-market facts.

## 3. Skill assessment scale

Users rate their own proficiency using a consistent scale:

| Level | Description |
| --- | --- |
| 1 | No practical knowledge yet |
| 2 | Beginner: understands basic concepts or can complete simple tasks with guidance |
| 3 | Developing: can complete common tasks with some guidance |
| 4 | Proficient: can complete common tasks independently |
| 5 | Advanced: can solve complex tasks and explain or guide others |

Ratings must be integers from 1 through 5. A missing answer is not a rating and must be kept distinct from level 1. Avoid presenting self-assessment as an objective certification of ability.

## 4. Recommendation scoring

For role `r`, each required skill `s` has required level `L_s`, importance weight `W_s`, and a user rating `U_s` when answered.

For answered skills:

```text
attainment_s = min(U_s, L_s) / L_s
readiness_score_r = 100 * sum(attainment_s * W_s) / sum(W_s)
```

Only answered role skills contribute to the readiness numerator and denominator. Capping proficiency at the required level prevents extra proficiency in one skill from hiding a gap in another.

Assessment coverage is calculated independently:

```text
coverage_r = 100 * sum(W_s for answered role skills) / sum(W_s for all role skills)
```

If the user has not answered any required skill for a role, its coverage is 0% and its readiness score is unavailable because the readiness denominator is zero.

Only roles with at least 70% coverage are eligible for ranking. Under-covered roles are marked “insufficient assessment,” not assigned a misleading low score. Return up to five eligible roles, sorted by readiness descending and role name alphabetically for ties. If no role is eligible, ask for the unanswered skills needed to increase coverage.

Each result should explain its score with:

- Coverage percentage
- Assessed strengths that met or exceeded the requirement
- Assessed gaps, including current level, required level, and numeric difference
- Required skills not assessed, shown separately from confirmed gaps

Readiness is a transparent comparison against the current role catalog. It is not a probability of getting hired or a measure of overall employability.

## 5. Validation rules

Before scoring, validate that:

- Every role skill ID exists in the shared catalog.
- Each `required_level` and `importance_weight` is an integer from 1 to 5.
- Each submitted rating is either missing or an integer from 1 to 5.
- A role has at least one required skill and a positive total importance weight.

Invalid catalog data or user input should produce a visible validation error; it must not be silently coerced into a score.

## 6. Validation and refinement

The taxonomy and role requirements should be reviewed against:

- Common IT job titles and responsibilities in Sri Lanka
- Local job descriptions and hiring trends
- Undergraduate pathways and stakeholder feedback from students, advisors, and industry practitioners

Keep a record of evidence, review dates, and changes when local market sources are collected. Until that review takes place, label the initial role requirements and weights as provisional. Revisit role coverage and weight choices when new evidence becomes available.

## 7. Initial role coverage

The starter dataset currently contains roles across development, analytics, security, testing, design, infrastructure, support, management, consulting, and analysis. The JSON catalog is the authoritative list, including the role-to-skill details. Keep this document descriptive rather than maintaining a second numeric role matrix that can drift out of sync.

## 8. Future enhancements

- Add dated Sri Lankan market evidence for role requirements and skill weights.
- Add role-specific learning topics and milestones linked to canonical skill IDs.
- Consider interests or preferred sectors as separate recommendation signals, with transparent explanations.
- Reassess the scoring model only after collecting suitable evaluation feedback; do not introduce user-data-trained recommendations without a separate privacy and validation plan.
