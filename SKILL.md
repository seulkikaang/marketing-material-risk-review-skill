---
name: marketing-material-risk-review
description: Use when reviewing Korean marketing copy, visuals, campaigns, ads, landing pages, influencer content, packages, events, or videos before publishing to catch controversy, legal, brand-safety, and social-sensitivity risks using Korean cases and official review standards.
version: 1.1.0
author: Hermes Agent
license: MIT
platforms: [linux, macos, windows]
metadata:
  hermes:
    tags: [marketing, advertising, brand-safety, korean-law, review, social-media]
    related_skills: [goseumdochi-guard, buong-verifier, xurl]
---

# Marketing Material Risk Review

## Overview

This skill reviews Korean-market marketing materials before publication. It is not legal advice. It is a conservative pre-flight gate that flags copy, visuals, campaign mechanics, influencer posts, landing pages, packages, event names, and videos that may trigger public backlash, platform issues, or formal review.

Use the attached reference files as pattern memory, not as a definitive legal database. They are generalized from Korean marketing controversy patterns and should be checked against current official sources when legal or regulatory exposure is possible.

- `references/risk-taxonomy-ko.md` - Korean marketing risk taxonomy and review questions.
- `references/visual-forensic-protocol-ko.md` - visual/OCR/frame-level inspection protocol.
- `references/korean-case-reference-ko.md` - Korean controversy-pattern checkpoints for similar-case reasoning.

## When to Use

Use this skill when the user asks to review, lint, approve, or pre-check:

- ad copy, taglines, push messages, captions, hashtags, subtitles, thumbnails
- SNS images, card news, posters, packages, OOH, web banners, landing pages
- influencer/creator scripts, reviews, UGC campaigns, affiliate posts
- AI-generated images/videos, virtual models, product mockups, event mechanics
- Korean-market campaigns involving food, health, beauty, finance, public policy, children, history, gender, region, disaster, politics, environment, or public institutions

Do not use this as a final legal sign-off. If a regulated category is involved, mark it `LEGAL_REVIEW_REQUIRED` and name the relevant source.

## Required Inputs

Ask for missing fields only when they materially change the risk assessment. Otherwise proceed with explicit assumptions.

```yaml
material:
  copy: ""
  image_or_video_description: ""
  channel: "Instagram / YouTube / OOH / landing page / package / app push / etc."
  industry: ""
  target_audience: ""
  publication_country: "Korea"
  launch_date: ""
  claim_basis: "certification, test result, price basis, discount condition, sponsorship disclosure, etc."
  attachments: []
```

## Review Workflow

### 1. Scope and evidence gate

- Identify asset type: `copy`, `visual`, `video`, `package`, `event`, `SNS`, `landing`, `influencer`, `AI-generated`.
- Identify regulated domain: food/health, medicine, medical service, cosmetics, finance, alcohol, youth, privacy/event, environment, broadcast, article-style ad.
- Separate facts from interpretation. Do not claim intent. Use risk language such as `may be read as`, `could be interpreted as`, `requires evidence`, `similar to prior controversy pattern`.

### 2. Official source gate

Check the relevant current official source for the domain:

| Domain | Minimum check |
|---|---|
| All ads | 표시광고법: false, exaggerated, deceptive, unfair comparison, omission of material conditions |
| Influencer/review | Economic relationship is clear, near, readable, and not hidden in hashtags only |
| E-commerce/UX | No hidden auto-renewal, drip pricing, fake countdown, forced continuity, obstructive cancellation |
| Food/health | No disease prevention/treatment, medical-like effect, unsupported diet/immune/safety claim |
| Medical/pharma | No treatment guarantee, side-effect-free claim, illegal testimonial, unapproved efficacy |
| Cosmetics | No medicine-like regeneration/treatment/filler/Botox effect, no unsupported functional claim |
| Finance | Loss risk, fees, limits, conditions, and review marks are visible with comparable prominence |
| Broadcast/video | Truthfulness, dignity, fairness, youth protection, industry restrictions |
| Article-style/native | Ad label is clear; layout/title/byline does not disguise ad as journalism |
| Privacy/event | Purpose, items, retention period, third-party sharing, marketing opt-in are separated |
| Environment | Environmental claim is truthful, specific, substantiated, material, and not overgeneralized |

If any required official source applies and the material lacks proof, escalate to `LEGAL_REVIEW_REQUIRED`.

### 3. Brand-safety and social-sensitivity gate

Check these risk families:

1. **People and groups** - gender, age, disability, body, region, class, job, nationality, religion, family form, pregnancy, disease, victim status.
2. **Sexualization and minors** - child/teen model styling, school uniforms, body-framing, innuendo, voyeuristic camera angle, product texture scenes that can be sexualized.
3. **History, politics, disaster, death** - colonial history, national violence, democratization, war, disaster, suicide, mourning, public tragedy, deceased figures.
4. **Culture and national symbols** - East Sea/Sea of Japan, Dokdo, Rising Sun imagery, kimchi/paocai, national flags, religious icons.
5. **Visual symbols and memes** - hand gestures, numbers, hidden text, community-coded icons, extremist/sexual/hate symbols, logo lookalikes.
6. **Price, benefit, and scarcity** - free, zero, unlimited, lowest, today only, almost sold out, guaranteed, 100%, no-risk, safe.
7. **Environmental and ESG** - paper, eco, green, carbon-free, recyclable, biodegradable, clean, sustainable without precise scope.
8. **AI and synthetic content** - AI model/person disclosure, deepfake resemblance, fake expert, fake testimonial, real-person likeness.
9. **External production risk** - outsourced animation, employee cameo, creator collaboration, UGC, AI output, last-minute edits.

### 4. Visual forensic gate

For images and videos, never judge only the overall impression.

- Inspect hands, logos, icons, object placement, background text, uniforms, maps, flags, dates, numbers, stickers, and microcopy.
- For video, request frame captures at 0.5-1 second intervals or at scene changes when possible.
- OCR visible text and review it separately from the caption.
- If a gesture or symbol resembles a contested code, write `visual_similarity_risk`; do not label it as intentional unless the material explicitly states it.
- If an official logo, institution mark, religious sign, military/police symbol, or political emblem is altered or used in satire/commercial context, mark `LEGAL_REVIEW_REQUIRED`.

### 5. Similar-case retrieval

Use the reference files to find generalized Korean controversy patterns by:

- year and industry
- asset type
- risk categories
- phrases such as `무료`, `최저가`, `무첨가`, `친환경`, `안심`, `100%`, `공식`, `선택한`, `건강`, `다이어트`, `협찬`, `AI`, `손모양`

Report only the closest 2-4 similar cases. Do not overload the user with the whole database.

## Verdict Rules

Return one of four verdicts:

| Verdict | Use when |
|---|---|
| `PASS` | No material risk found, required disclosures/evidence are present, and no regulated category gap remains |
| `REVISE` | Risk is fixable by copy, disclosure, layout, targeting, or visual adjustment before launch |
| `HIGH_RISK` | Likely backlash, discrimination/sexualization/history/disaster sensitivity, serious misleading claim, or unsafe visual pattern |
| `LEGAL_REVIEW_REQUIRED` | Regulated domain, official logo/institution/privacy/finance/medical/food/green claim, or legal substantiation gap |

Severity hints:

- `CRITICAL`: stop publication. Legal/regulatory exposure, minors/sexualization, disease/medical claim, privacy misuse, official institution misuse, national tragedy/political violence risk.
- `HIGH`: likely public backlash or brand trust damage. Gender/region/job/body mockery, greenwashing, hidden sponsorship, misleading discount, controversial symbol.
- `MEDIUM`: ambiguity or missing context. Needs stronger disclosure, evidence, or alternative wording.
- `LOW`: wording clarity issue with low controversy probability.

## Output Template

```markdown
## Marketing Material Risk Review

Verdict: PASS / REVISE / HIGH_RISK / LEGAL_REVIEW_REQUIRED
Severity: CRITICAL / HIGH / MEDIUM / LOW

### Findings
| status | location | issue | why it matters | evidence/source |
|---|---|---|---|---|
| FAIL/REVIEW/OK | copy line / visual area / frame | ... | ... | official source or similar case |

### Similar Korean Cases
1. `pattern/source` - similarity and difference.
2. `pattern/source` - similarity and difference.

### Required Fixes
1. ...
2. ...
3. ...

### Safer Alternatives
- Option A: ...
- Option B: ...
- Option C: ...

### Final Gate
- [ ] Official-source gate checked
- [ ] Disclosure/evidence checked
- [ ] Visual forensic gate checked
- [ ] Sensitive-date/history/disaster check completed
- [ ] Legal review requested if needed
```

## Safer Rewrite Rules

- Replace absolute claims with scoped, evidenced claims: `100% 안전` → `시험 조건에서 확인된 범위 내 ...`.
- Move conditions next to the main claim, not below the fold: `최저가` must include comparison basis, date, exclusions.
- For influencer content, put disclosure near the first claim and in the visible caption/video overlay.
- For green claims, specify object and scope: product, package, ingredient, operation, lifecycle stage.
- For public-interest campaigns, center affected people and purpose. Avoid party imagery that conflicts with disease, disaster, or victim contexts.
- For humor, remove jokes aimed at protected or vulnerable groups, victims, regions, families, occupations, disease, or death.
- For visual ambiguity, regenerate or redesign rather than explaining intent after publication.

## Common Pitfalls

1. **Intent defense.** “We did not mean it” does not reduce launch risk. Review likely interpretation.
2. **Single-frame blindness.** Videos can fail because of one frame, hand pose, subtitle, or background object.
3. **Disclosure hidden in hashtags.** Sponsorship disclosure must be easy to notice, not buried.
4. **Green words without scope.** Eco-friendly, carbon-free, paper, natural, biodegradable require exact scope and evidence.
5. **Regulated category understatement.** Food, cosmetics, finance, medical, medicine, privacy, and article-style ads need official-source gates.
6. **Public campaign mismatch.** A good cause can still fail if execution looks like spectacle, mockery, or self-promotion.
7. **Reference-case overfitting.** Use prior cases as warning patterns, not as proof that a new material is unlawful.

## Verification Checklist

- [ ] Inputs and assumptions are stated.
- [ ] Official-source gate applied where relevant.
- [ ] At least 2 similar-case patterns checked when risk is `REVISE` or worse.
- [ ] Visual/video material was inspected beyond overall impression.
- [ ] Findings use cautious language and do not infer intent.
- [ ] The verdict includes concrete fixes, not just criticism.
- [ ] `LEGAL_REVIEW_REQUIRED` is used for regulated/legal uncertainty instead of giving legal advice.
