# GoRank Product, Business, and Technical Blueprint

Created: 2026-05-10  
Status: Draft for founder, product, engineering, legal, and sales review  
Scope: Product strategy, MVP PRD, architecture, operations, pricing, GTM, and 30-day planning inputs

## Executive Summary

GoRank is a Brazil-first AI Brand Visibility Platform for companies that need to know whether they appear, get cited, and are recommended in AI-generated answers. The commercial promise is simple: "Faca sua marca aparecer nas respostas da IA." The product should avoid any guarantee of "ranking" inside LLMs. The defensible claim is evidence-backed optimization: monitor AI answers, diagnose why competitors win, recommend safe improvements, execute reviewable fixes, and measure before/after impact.

The fastest path to revenue is a hybrid B2B SaaS plus managed service: sell paid AI visibility audits and monthly optimization retainers to Brazilian SMBs, agencies, clinics, law firms, B2B SaaS, real estate, education, e-commerce, franchises, and local service businesses. From day one, the managed service should run on the same automated core that later becomes self-serve SaaS.

The initial vertical slice should be a client entering brand, domain, category, city/country, competitors, and business goals. GoRank generates 30 Brazilian Portuguese prompts, runs monitoring across a small set of compliant engines and search providers, extracts mentions/citations, crawls the site, generates 10 prioritized recommendations, and produces a PDF report. Optional execution creates a GitHub PR or CMS-ready draft, never an auto-published change.

## A. Research Synthesis

### Market Shift

Users increasingly ask AI systems category, comparison, local, and buying-intent questions that historically went to Google. AI answer engines synthesize responses, cite sources inconsistently, and may recommend brands without sending a click. That changes the optimization target from "rank on a blue-link SERP" to "be discoverable, understandable, citable, and trusted by retrieval and answer-generation systems."

This is not a replacement for SEO. It is an adjacent layer. Google says the same SEO fundamentals remain relevant for AI Overviews and AI Mode: crawlability, indexability, textual content, helpful content, internal links, page experience, structured data that matches visible text, and updated Business Profile or Merchant Center data where relevant. Google also says there are no special schema or "AI text files" required for AI features, so GoRank should treat llms.txt and other AI files as optional experiments, not guaranteed levers.

### Academic Evidence

The original GEO paper formalized "Generative Engine Optimization" as a black-box optimization framework and reported that visibility could improve by up to 40 percent in tested generative engine responses, with strong domain variance. The key implication is that GoRank should avoid universal rules and instead measure by industry, prompt type, language, engine, and source mix.

A later empirical GEO paper argues that AI search differs from Google because it leans heavily on earned/third-party authoritative sources, with engine-specific, language-specific, and phrasing-sensitive behavior. Treat this as strong directional evidence, but still not a deterministic ranking recipe.

A 2026 AgenticGEO preprint proposes adaptive agentic optimization and warns that static heuristics and single-prompt optimization overfit. For GoRank, this supports continuous monitoring, versioned recommendations, and evaluation loops rather than one-time "AI SEO checklist" work.

### Search and Crawler Documentation

OpenAI documents separate crawlers and fetchers: `OAI-SearchBot` is for ChatGPT search visibility, `GPTBot` is for foundation model training, and `ChatGPT-User` is user-triggered and not used for automatic web crawling. Perplexity documents `PerplexityBot` for surfacing websites in search results and `Perplexity-User` for user-triggered access. Google documents shared crawler infrastructure, `Google-Extended` as a robots.txt product token for Gemini Apps and Vertex AI training/grounding controls, and Googlebot/search controls for Search AI features.

This means crawler analytics are feasible if customers share logs or install a snippet/proxy integration, but crawler observations must be interpreted carefully. A visit from a crawler is not proof of future citation. A missing visit is not proof the brand cannot appear. Logs are a diagnostic signal, not a ranking metric.

### Competitor Landscape

The category already includes enterprise platforms, SEO-suite incumbents, startup GEO trackers, execution-heavy content workflow platforms, and free checkers. The common feature baseline is prompt monitoring, mention tracking, competitor comparison, sentiment/perception, citation/source tracking, reports, and some recommendations. The gap for GoRank is Brazil-first prompt intelligence, local visibility, Portuguese reporting, managed service workflow, and remediation through GitHub/CMS drafts.

### Current Best Practices Worth Productizing

Evidence-backed or strongly supported practices:

- Track AI visibility by prompt, engine, location, language, and time instead of treating "AI visibility" as one global score.
- Monitor competitors in the same prompt runs because relative inclusion matters more than absolute mentions.
- Extract citations and source domains because cited pages are often the visible evidence behind AI answers.
- Maintain search fundamentals: crawlability, indexability, internal links, canonical hygiene, sitemap, server health, and textual content.
- Improve entity clarity: consistent brand name, domain, legal name, category, products, locations, leadership, contact details, and "sameAs" references.
- Add structured data when it accurately matches visible page content and is supported by Google rich result documentation.
- Create useful pages for high-intent questions: category, use case, comparison, alternatives, pricing, FAQ, case studies, reviews, methodology, and local service pages.
- Improve third-party source coverage: credible directories, review platforms, media mentions, partner pages, industry lists, Google Business Profile, and local listings.
- Keep facts consistent across owned and third-party sources to reduce hallucinations.
- Measure before/after changes using frozen prompt sets and engine-specific snapshots.

Plausible but not proven:

- llms.txt may improve machine readability for some agents or developer-oriented documentation. It is a proposal, not a universal AI search inclusion mechanism.
- Lightweight machine-readable pages may help crawler parsing, but should not replace human UX or violate cloaking/search policies.
- Query fan-out modeling may help predict which subtopics and sources an engine uses, but each engine differs.
- Review volume, freshness, and reputation likely affect local and product recommendations, but the exact weights are opaque.
- Reddit/forum/community presence can matter in categories where engines frequently cite discussion sources, but it must be authentic and policy-compliant.

Speculative:

- Any fixed "LLM ranking factor" list.
- Claims that a specific schema type guarantees mention in ChatGPT, Gemini, Claude, Perplexity, Copilot, or Grok.
- Claims that adding a single AI file, hidden page, or prompt-targeted text block will reliably improve AI recommendations.
- Automated "entity injection" into many websites without quality editorial review.

Risky or avoid:

- Guaranteed ranking or guaranteed recommendations in LLMs.
- Scraping private or logged-in experiences in ways that violate terms.
- Cloaking content for bots while showing different claims to users.
- Fake reviews, review gating, review incentives that violate platform policies, or synthetic testimonials.
- Spammy programmatic pages, doorway pages, copied competitor comparison content, or unsubstantiated claims.
- Auto-publishing generated content without human approval.
- Auto-merging GitHub PRs.
- Manipulating forums, Wikipedia, Wikidata, or directories deceptively.

## B. Competitor Matrix

Snapshot date: 2026-05-10. Verify live pricing before publishing collateral.

| Competitor | Positioning | Target Customer | AI Engines / Surfaces | Monitoring | Citation / Source Tracking | Recommendations | Execution / Remediation | Integrations | Pricing Snapshot | Strengths | Weaknesses / Gaps for GoRank |
|---|---|---|---|---|---|---|---|---|---|---|---|
| Profound | Enterprise AEO/GEO platform with monitoring, prompt volumes, agents, shopping, and AI bot analytics | Enterprise brands, AEO teams, content teams, PR/brand teams, agencies | ChatGPT, Perplexity, Claude, Gemini, Grok, Copilot, Meta AI, DeepSeek, Google AI Overviews, likely more | Strong: answer engine insights, prompt volumes, brand representation | Strong: citations and agent analytics | Strong: platform agents and AEO workflows | Content agents, but public details on GitHub/CMS PR execution are limited | Developer docs, integrations, enterprise workflows | Demo-led; public pricing page has limited detail | Category leader, broad coverage, enterprise credibility, bot analytics | Likely expensive and enterprise-heavy. Brazil SMB, Portuguese prompt intelligence, managed local service, and lightweight remediation can differentiate |
| Scrunch AI | AI customer experience and AI search visibility platform with Agent Experience Platform | Mid-market, enterprise, agencies | ChatGPT, Claude, Gemini, Perplexity, Google AI Mode/Overviews, Meta | Strong: prompts, topics, entities, competitors, personas, geo | Strong: citation analysis and AI traffic | Strong: optimization guidance and page audits | AXP serves AI-optimized structured pages | Data API, enterprise SSO, likely CMS/workflow integrations | Starter around $250 to $300/mo; Growth around $417 to $500/mo; Enterprise custom | Clear monitoring plus crawl/bot observability and agent-readable site layer | AXP may feel too technical or risky for SMBs. GoRank can focus on transparent, reviewable changes and Brazil-first managed service |
| Peec AI | AI search analytics for marketing teams and SEO agencies | SEO/content teams, agencies, brands | ChatGPT, AI Mode, AI Overviews, Copilot, Perplexity, Gemini, Grok | Strong: prompt tracking, flexible projects, daily/weekly tracking | Strong: top citations and source visibility | Moderate: recommendations and action are less central than analytics | Limited public evidence of PR/CMS remediation | API, Looker, MCP, SSO in higher tiers | Starter/Pro/Advanced; agency credit bundles | Clean UI, flexible credits, agency-oriented pricing | Less focused on Portuguese/local Brazil and hands-on execution |
| Otterly AI | AI search monitoring and optimization platform | Agencies, SMEs, marketing teams | ChatGPT, Google AI Overviews, Perplexity, Copilot; Gemini and AI Mode add-ons | Strong: daily prompt tracking, brand coverage, position, countries | Strong: link citation analysis | Strong: recommendations and GEO audits | Mostly reports/recommendations, not code/CMS execution | Looker Studio connector; agency partner workflows | Lite $29/mo, Standard $189/mo, Premium $489/mo plus add-ons | Accessible pricing, reports, multi-country support | Execution layer appears shallow. GoRank can win with managed service, Portuguese prompt packs, and remediation artifacts |
| AthenaHQ | AEO/GEO platform for AI search optimization | Businesses, multi-location brands, agencies, CMOs, SEO teams | 8+ major LLMs including ChatGPT, Perplexity, AI Overviews, AI Mode, Gemini, Claude, Copilot, Grok | Strong: tracking, local/location-level visibility, competitors | Strong: authority and citation intelligence | Strong: on/off-page GEO and blindspot detection | Content optimization; public details on code/CMS PRs limited | RBAC, likely enterprise integrations | Self-serve around $95 to $295/mo promo/listed; credit-based | Strong location story and broad engine list | Brazil-specific local workflows and managed execution still open |
| Ahrefs Brand Radar | AI visibility database inside a major SEO suite | SEO teams, agencies, brand marketers | AI Overviews, AI Mode, ChatGPT, Copilot, Gemini, Perplexity, Grok; YouTube, TikTok, Reddit signals | Strong: massive prompt database plus custom prompts | Strong: AI citations, sources, social/content surfaces | Moderate: insight-heavy rather than managed remediation | Ahrefs has Patches/SEO tools, but Brand Radar is mostly analytics | Ahrefs suite, custom prompts | Around EUR 358/mo selected platforms, EUR 654/mo all platforms | Huge SEO dataset, no-setup prompt index, incumbent trust | Not Brazil-first, likely too expensive/complex for SMB managed service |
| Semrush One / AI Visibility | Unified SEO plus AI visibility platform | SEO teams, agencies, brands, enterprises | Google, AI Overviews, ChatGPT, Gemini, Perplexity and other LLMs | Strong: prompt database, brand presence, sentiment, competitors | Strong: cited pages/topics | Strong: AI-powered recommendations | Existing SEO workflows; public code/CMS remediation not core | Semrush ecosystem, API/MCP by tier | Starter/Pro+/Advanced; exact plan prices vary | Massive SEO data, brand trust, AI plus SEO in one subscription | Incumbent breadth leaves room for verticalized managed service and remediation |
| Writesonic GEO | AI SEO and AI search visibility plus content platform | SMBs, content teams, agencies | ChatGPT in lower plan; more platforms by tier | Moderate/strong: prompts, answers, daily tracking, markets | AI bot analytics and visibility tracking | Stronger content/action center in higher tiers | Content generation and action center | SEO/content stack, data sources like SERP/Reddit | Starter $79/mo; Basic $199/mo; Growth $399/mo; Enterprise custom | Combines content creation with AI visibility | Content-first. GoRank can be diagnosis/execution-first and Brazilian Portuguese-first |
| SE Ranking / SE Visible | Standalone AI visibility plus broader SEO suite | Business owners, agencies, CMOs, SEO teams | ChatGPT, Gemini, AI Mode, AI Overviews, Perplexity | Strong: weekly updates, prompts, brand/sentiment/competitors | Sources listed as coming soon in FAQ; broader AI Search Toolkit tracks sources | Moderate | Reporting/export; execution not core | SE Ranking SEO ecosystem | Basic around $99/mo, Core $189/mo, Plus $355/mo for SE Visible | Accessible multi-brand tracking and standalone packaging | Limited Portuguese/language coverage in public positioning. Execution and managed service gaps |
| Azoma | Enterprise AI visibility and GEO for products/SKUs | Enterprise brands, e-commerce, retail/product companies | ChatGPT, Perplexity, Gemini, Rufus | Strong: product visibility, SOV, competitors, query logs | Strong: citation gap and mention gap | Strong: product content optimization | Generates/optimizes product content | Enterprise workflows | Custom, SKU/platform/market-based | Strong commerce focus, pilot model, product/SKU tracking | Less suited for Brazilian service businesses, legal, clinics, local SMBs |
| Limy | AI agent visibility and revenue optimization | Growth-stage/enterprise brands focused on agentic commerce | "All AI search engines"; ChatGPT/Gemini user prompts in public reporting | Strong: revenue, performance, narrative, perception | Agent/CDN fetch analysis | Up to 8 recs/mo on Growth; custom enterprise | Operational layer, content/agent optimization | CDN style integration implied | Growth $449/mo; Enterprise custom | Strong agentic-commerce angle and revenue attribution | Expensive, commerce/agent-centric, not SMB/Brazil/local-first |
| AirOps | AI search visibility plus content workflows and execution | Growth/content teams, enterprise brands | ChatGPT, Perplexity, Gemini; Google AI Overviews | Strong: prompts/pages, Page360, GA4, SEO plus AI | Strong: citations, topics, domains, Reddit/offsite | Strong: prioritized roadmap | Strong content workflow and publishing processes | CMS, SEO, AEO, social, project integrations | Solo/Pro free-start tiers; Enterprise custom | Execution-focused and proven content workflows | Less localized for Brazil, may be overbuilt for local service businesses |
| Quattr | AI-native SEO, AEO, and GEO platform with GIGA agent | Enterprise SEO/content teams | Google AI Overviews, ChatGPT, Claude, Perplexity, AI Mode, others | Strong: visibility, rank, share of voice, sentiment, competitors | Strong: citation and source selection | Strong: optimization, E-E-A-T intelligence, internal linking | Strong content optimization; public PR/CMS details limited | Enterprise SEO workflows | Demo-led/custom | Strong enterprise SEO/GEO workflow and content intelligence | Enterprise focus leaves room for SMB/agency managed-service wedge |
| Meev / Scope / SEObolt / AEO Rank Tracker / AI Visibility Index | Smaller/free or SMB AI visibility trackers | SMBs, founders, agencies, local businesses | Varies: ChatGPT, Claude, Gemini, Perplexity, Grok, AI Overviews | Basic to moderate | Varies | Varies | Some publish/content workflows | Varies | Free to low-cost to SMB tiers | Indicates demand for simple checkers | Many lack depth, trust, Brazil localization, and end-to-end execution |

## C. Evidence-Backed Strategy List

### Evidence-Backed

1. Monitor a frozen prompt set over time by engine, location, language, and persona.
2. Compare brand mention, recommendation, citation, and position against named competitors.
3. Analyze cited sources and source types by category and prompt intent.
4. Keep pages crawlable, indexable, internally linked, and available as text.
5. Ensure structured data matches visible content and follows Google feature guidelines.
6. Build entity clarity through consistent facts across owned and reputable third-party sources.
7. Create high-intent answerable content for comparison, alternatives, "best X", pricing, use case, FAQ, local, and category queries.
8. Strengthen credible third-party mentions, reviews, directories, partner pages, press, and expert sources.
9. Track AI crawler/fetcher logs as diagnostic evidence, not as a direct ranking guarantee.
10. Use before/after measurement and re-test prompts after each approved change.

### Plausible But Not Proven

1. llms.txt and markdown mirrors may help specific agents or workflows parse content.
2. Lightweight agent-readable page variants may improve extraction if implemented transparently and consistently with visible content.
3. Explicit comparison tables and concise factual summaries may improve extractability.
4. Category-specific original data, benchmarks, and methodology pages may attract AI citations.
5. Query fan-out simulation may predict adjacent sources an AI engine will cite.

### Speculative

1. Universal LLM ranking factors.
2. Guaranteed citation from any schema type.
3. "Prompt stuffing" pages that target AI systems rather than users.
4. Synthetic forum posts as a visibility strategy.
5. AI search volume estimates without observable query data or disclosed methodology.

### Risky / Avoid

1. Guaranteed LLM rankings or recommendations.
2. Fake reviews or deceptive reputation manipulation.
3. Cloaking or hidden bot-only claims.
4. Auto-publishing generated content.
5. Terms-violating scraping of consumer AI tools.
6. Manipulating Wikipedia/Wikidata/Reddit/forums without community value.
7. Medical/legal claims not reviewed by qualified humans.

## D. Product Positioning

### Primary Positioning

GoRank helps companies monitor, diagnose, and improve how their brands appear in AI-generated answers.

### Portuguese Commercial Promise

Faca sua marca aparecer nas respostas da IA.

### Supporting Messages

- Sua marca aparece quando alguem pergunta no ChatGPT?
- Descubra quais concorrentes a IA recomenda no seu lugar.
- Monitore, diagnostique e melhore sua presenca nas respostas da IA.
- SEO para a era da IA, com diagnostico e execucao automatizada.
- Sem promessas falsas de ranking. Apenas evidencia, melhoria continua e execucao segura.

### English-Ready Positioning

Make your brand visible in AI answers. GoRank monitors AI search, explains why competitors win, and turns insights into safe, reviewable optimization work.

### Differentiation

- Brazil and Portuguese-first prompt intelligence.
- Local AI visibility for city/service searches.
- Managed service workflow for companies that want outcomes, not another dashboard.
- Recommendation-to-execution loop through GitHub PRs, CMS drafts, tickets, and reports.
- Explainable evidence and confidence scoring.
- Before/after measurement.

## E. PRD

### Problem

Companies do not know whether AI assistants mention, cite, or recommend them when customers ask category, comparison, local, or buying questions. They also do not know what to fix or whether changes worked.

### Users

- SMB owner or marketing lead.
- Agency account manager.
- SEO/content consultant.
- B2B SaaS marketer.
- Legal/clinic/local service operator.
- Internal GoRank consultant.

### Goals

- Show whether a brand appears in AI answers.
- Show which competitors appear instead.
- Identify prompts and intents that matter commercially.
- Extract citations and source influence.
- Diagnose technical, content, entity, citation, reputation, and local gaps.
- Recommend prioritized safe actions.
- Generate reviewable remediation artifacts.
- Produce client-ready reports.

### Non-Goals

- Guarantee rankings.
- Replace full SEO platforms in MVP.
- Build every AI engine integration.
- Auto-publish content.
- Scrape private or restricted surfaces.

### Core Jobs To Be Done

1. "Tell me if my brand appears when customers ask AI about my category."
2. "Tell me which competitors are winning and why."
3. "Tell me what sources the AI trusts."
4. "Tell me what to change first."
5. "Create the draft/PR/report so my team can approve and ship."
6. "Show whether visibility improved after changes."

### Product Modules

#### 1. Brand Onboarding

Fields:

- Brand name, legal name, domain, aliases.
- Description and canonical one-sentence brand fact.
- Category, industry, country, language.
- Products/services.
- Target audience and personas.
- Competitors and competitor domains.
- Target locations.
- Existing content channels.
- GitHub/CMS integrations.
- Business goals and conversion goals.
- Priority keywords, topics, and prompts.
- Compliance sensitivity: legal, medical, financial, regulated, low-risk.

MVP output:

- Workspace.
- Brand profile.
- Competitor list.
- Initial prompt set.
- Monitoring schedule.

#### 2. Prompt Discovery Engine

Prompt sources:

- Brand/category inputs.
- Competitors.
- Search keyword APIs.
- SERP People Also Ask / related searches where available.
- LLM-generated prompt variants.
- Internal Portuguese prompt templates.
- Consultant-entered prompts.

Prompt dimensions:

- Intent: commercial, informational, local, comparison, problem/solution, alternatives, reputation, pricing, service selection.
- Persona: buyer, procurement, patient, founder, homeowner, student, agency client.
- Market: Brazil, state, city, neighborhood.
- Language: pt-BR first, English later.
- Funnel: TOFU, MOFU, BOFU.
- Risk: medical/legal/financial sensitivity.

Examples:

- "Qual melhor clinica de dermatologia em Sao Paulo?"
- "Melhor software juridico para pequenos escritorios"
- "Quais empresas fazem automacao de WhatsApp para comercio local?"
- "Alternativas ao [concorrente] no Brasil"
- "Qual empresa contratar para [servico]?"
- "Melhor imobiliaria para comprar apartamento em [cidade]"
- "Clinica de [especialidade] confiavel perto de [bairro]"

MVP:

- Generate 30 prompts per brand.
- Allow manual edit/approval.
- Tag prompts with intent, location, persona, and priority.

#### 3. Monitoring Engine

Track:

- Brand mentioned or not.
- Competitors mentioned.
- Position/order in answer.
- Recommendation strength.
- Sentiment/perception.
- Citation/source URLs.
- Citation frequency.
- Answer summary.
- Model/provider/engine.
- Prompt.
- Region/language.
- Timestamp.
- Raw answer and normalized structured extraction.
- Screenshot/evidence where applicable and compliant.
- Answer volatility.
- Hallucinations or incorrect facts.

MVP engines:

- OpenAI API/search-capable model where terms permit, with clear label that API responses may differ from consumer ChatGPT.
- Perplexity API/Sonar where feasible.
- Google Search/SERP API for AI Overviews where provider terms permit.
- Manual evidence capture for unsupported engines.

Avoid in MVP:

- Terms-violating browser automation against consumer AI tools.
- Claims that API outputs equal consumer app outputs.

#### 4. Metrics

AI Visibility Score:

- Weighted composite of mention rate, recommendation strength, average position, citation share, prompt priority, and competitor gap.
- Must always show component metrics so the score is explainable.

Other metrics:

- Share of Answer.
- Share of Mentions.
- Share of Recommendations.
- Average Position.
- Citation Share.
- Competitor Gap.
- Sentiment Score.
- Source Authority Score.
- Prompt Coverage Score.
- Entity Clarity Score.
- Content Gap Score.
- Technical GEO Score.
- Local AI Visibility Score.
- Change over time.
- Before/after improvement.

MVP scoring:

- Keep formula transparent and conservative.
- Do not compare across unrelated industries until benchmark data exists.

#### 5. Citation / Source Intelligence

Track:

- URLs cited by AI engines.
- Domains cited for competitors.
- Source types: owned site, competitor site, directory, review platform, media, government, academic, Reddit/forum, YouTube, Wikipedia/Wikidata, marketplace, local listing.
- Missing source coverage.
- High-authority opportunities.
- Source freshness and crawlability.
- Whether source facts align with brand profile.

MVP:

- Source table with frequency, engine, prompts, competitors, source type, and opportunity notes.

#### 6. AI Crawler Analytics

Feasibility:

- Detect AI crawlers from server logs, CDN logs, or a customer-side snippet/proxy endpoint.
- User agents: OAI-SearchBot, GPTBot, ChatGPT-User, PerplexityBot, Perplexity-User, ClaudeBot/Claude-SearchBot where documented, Googlebot, Google-Extended token implications, Bingbot/Copilot-related crawlers where documented.
- Verify official IP ranges where providers publish them.

Product:

- Show pages visited by crawler/fetcher.
- Show crawl gaps for important pages.
- Show blocked/allowed rules in robots.txt.
- Recommend WAF/CDN allow-list changes for verified bots where appropriate.

MVP:

- Optional log upload CSV.
- Basic user-agent detection.
- "Diagnostic only" disclaimer.

#### 7. Site / GEO Technical Audit

Checks:

- robots.txt.
- sitemap.xml and sitemap index.
- llms.txt presence and quality, marked experimental.
- Schema.org structured data: Organization, LocalBusiness, Product, FAQPage, Article, BreadcrumbList, Review/AggregateRating where appropriate.
- Canonicals.
- Metadata.
- Headings.
- Internal links.
- Crawl depth.
- Thin/duplicate/outdated content.
- Missing comparison, alternatives, category, use-case, FAQ, local pages.
- Brand/entity explanation.
- NAP consistency for local businesses.
- Author/expertise signals.
- Citation/source pages.
- Machine readability and text extraction.
- Broken links and 4xx/5xx.
- JS-rendered critical content.

MVP:

- Crawl up to 250 pages per domain.
- Focus on homepage, product/service pages, about, contact, blog, top pages from sitemap.

#### 8. Diagnosis Engine

For every weak prompt:

- State whether the brand is missing, low-positioned, uncited, negatively framed, or factually wrong.
- Compare competitors appearing in the answer.
- Identify likely signals: content coverage, source coverage, reviews, local listings, entity clarity, technical accessibility, third-party authority.
- Attach evidence: prompt run IDs, answer excerpts, citations, audit findings, competitor pages.
- Avoid overclaiming: use "likely", "observed", "needs validation", and confidence.

#### 9. Recommendation Engine

Each recommendation includes:

- Title.
- Type: technical, content, citation, reputation, local, schema, integration, PR, CMS.
- Affected URL/file.
- Reason.
- Evidence.
- Expected impact.
- Confidence.
- Effort.
- Priority score.
- Implementation steps.
- Risk level.
- Auto-executable flag.
- Human approval requirement.
- Success metric.
- Re-test plan.

Priority score:

`priority = impact * confidence * prompt_value * competitor_gap / effort`

#### 10. Remediation / Execution Engine

Supported outputs:

- GitHub PR generation.
- CMS draft generation.
- Markdown export.
- Linear/Jira ticket.
- Content brief.
- Schema markup suggestion.
- FAQ draft.
- Metadata improvement.
- llms.txt draft.
- robots/sitemap recommendation.
- Internal linking suggestion.
- Comparison page draft.
- Alternatives page draft.
- Category page draft.
- Local landing page draft.
- Citation outreach target.
- Review generation strategy.
- Brand fact consistency correction.

Rules:

- Never auto-merge PRs.
- Never auto-publish content.
- Human approval required for all external publication.
- PR descriptions explain GEO rationale.
- Keep full audit trail.

#### 11. GitHub App

Flow:

1. Install app.
2. Select repository.
3. Grant least-privilege access.
4. Detect framework: Next.js, Astro, static HTML, WordPress theme, etc.
5. Scan safe files.
6. Create branch.
7. Apply changes.
8. Open PR.
9. Add checklist and rationale.
10. Link to prompts and diagnosis.
11. Track merge status.
12. Re-run monitoring after merge.

MVP:

- GitHub App can be simulated by manual repo connection/export if app approval is too slow.
- Generate a patch/PR for one simple change: JSON-LD Organization schema, metadata, FAQ block, or llms.txt.

#### 12. CMS

Initial:

- WordPress export/draft via REST API.
- Webflow draft/export.
- Shopify later.

MVP:

- Generate CMS-ready Markdown/HTML drafts and copy blocks.
- Direct publishing postponed.

#### 13. Reporting

Report sections:

- Executive summary.
- Current AI visibility.
- Competitor comparison.
- Top winning prompts.
- Top lost prompts.
- Source/citation analysis.
- Technical audit findings.
- Priority recommendations.
- Completed fixes.
- Before/after changes.
- Next action plan.
- White-label agency version.
- Appendix with prompts and evidence.

MVP:

- HTML report export plus PDF print.

#### 14. Alerts

Alert when:

- Brand disappears from high-value prompt.
- Competitor overtakes brand.
- Negative sentiment increases.
- Important citation changes.
- New competitor appears.
- AI answer hallucinates wrong brand fact.
- Technical issue detected.
- AI crawler blocked or not visiting key pages.

MVP:

- Email alerts for high-value prompt loss, competitor overtakes, and hallucinated fact.

## F. MVP Scope

30-day shippable MVP:

1. Workspace and brand onboarding.
2. Competitor entry.
3. Prompt generation: 30 pt-BR prompts.
4. Prompt library with tags and approval.
5. Monitoring runs for 2 to 3 supported sources.
6. Raw answer storage.
7. Mention, competitor, position, sentiment, citation extraction.
8. Basic visibility score.
9. Competitor comparison.
10. Citation/source table.
11. Site crawler and technical audit.
12. Recommendation generation.
13. HTML/PDF report.
14. Free AI Brand Visibility Checker landing flow.
15. Internal managed-service dashboard.
16. Manual execution workflow with Markdown/CMS drafts and optional GitHub patch/PR prototype.

MVP constraints:

- Semi-automated monitoring is acceptable.
- Some engines can be "manual evidence" only.
- No billing automation if it slows sales. Use Stripe payment links or invoices.
- No self-serve multi-tenant billing complexity beyond data model readiness.

## G. System Architecture

### Principles

- API-first.
- Multi-tenant from day one.
- Durable workflows for long-running monitoring/audit/report jobs.
- Provider-agnostic LLM abstraction.
- Evidence-first data storage.
- Human approval before publication.
- Compliance-aware integrations.

### Stack

Frontend:

- Next.js, React, TypeScript.
- Tailwind and shadcn/ui.
- Dashboard-first SaaS UX.

Backend:

- Python, FastAPI.
- PostgreSQL.
- Redis.
- Temporal for durable workflows.
- pgvector for embeddings initially; Qdrant if vector workload grows.
- Docker Compose for MVP.

AI Layer:

- Provider abstraction.
- LiteLLM-compatible routing.
- Structured outputs with JSON schemas.
- Prompt/version management.
- Evals for extraction and recommendation quality.
- Cost tracking per workspace and run.

Data Providers:

- OpenAI, Anthropic, Google/Gemini, Perplexity where APIs and terms allow.
- SERP APIs for Google AI Overview monitoring where allowed.
- Search Console and GA4 later.
- Crawling for public owned/competitor pages.

### Logical Components

- Web app.
- FastAPI app.
- Auth/tenant service.
- Monitoring service.
- Prompt service.
- Extraction service.
- Crawl/audit service.
- Recommendation service.
- Report service.
- Execution service.
- Integration service.
- Cost/usage service.
- Admin/managed-service console.

### Data Flow

1. User creates workspace and brand.
2. Prompt workflow generates candidate prompts.
3. User approves prompt set.
4. Monitoring workflow runs prompts by engine/region/language.
5. Extraction agent normalizes answers into mentions, citations, sentiment, and competitor data.
6. Crawler audits owned site and selected competitor/source pages.
7. Diagnosis engine joins prompt evidence, citations, audit findings, and competitor signals.
8. Recommendation engine ranks actions.
9. Report workflow renders client report.
10. Execution workflow creates draft/PR/ticket after approval.
11. Re-test workflow compares before/after.

## H. Database Schema

PostgreSQL core tables. Use UUID primary keys, `created_at`, `updated_at`, soft delete where needed, and `organization_id` or `workspace_id` on tenant-scoped tables.

```sql
users (
  id uuid primary key,
  email text unique not null,
  name text,
  role text,
  locale text default 'pt-BR',
  created_at timestamptz not null
);

organizations (
  id uuid primary key,
  name text not null,
  plan text,
  billing_email text,
  country text,
  created_at timestamptz not null
);

organization_members (
  organization_id uuid references organizations(id),
  user_id uuid references users(id),
  role text not null,
  primary key (organization_id, user_id)
);

workspaces (
  id uuid primary key,
  organization_id uuid references organizations(id),
  name text not null,
  type text not null, -- internal, client, agency_client
  status text not null
);

brands (
  id uuid primary key,
  workspace_id uuid references workspaces(id),
  name text not null,
  legal_name text,
  domain text not null,
  description text,
  category text,
  industry text,
  country text,
  language text,
  products_services jsonb,
  target_audience jsonb,
  target_locations jsonb,
  business_goals jsonb,
  conversion_goals jsonb,
  canonical_facts jsonb,
  compliance_sensitivity text
);

competitors (
  id uuid primary key,
  brand_id uuid references brands(id),
  name text not null,
  domain text,
  notes text
);

ai_engines (
  id uuid primary key,
  slug text unique not null,
  name text not null,
  provider text,
  surface_type text, -- api, search_api, manual, browser_automation
  terms_status text,
  supports_citations boolean default false,
  supports_region boolean default false
);

prompts (
  id uuid primary key,
  brand_id uuid references brands(id),
  text text not null,
  language text not null,
  country text,
  region text,
  city text,
  intent text,
  persona text,
  funnel_stage text,
  priority int default 3,
  status text not null, -- draft, approved, paused
  generated_by text,
  version int default 1
);

prompt_runs (
  id uuid primary key,
  workspace_id uuid references workspaces(id),
  brand_id uuid references brands(id),
  prompt_id uuid references prompts(id),
  ai_engine_id uuid references ai_engines(id),
  run_type text not null, -- scheduled, manual, retest, free_checker
  region text,
  language text,
  status text not null,
  started_at timestamptz,
  completed_at timestamptz,
  cost_usd numeric(12,6),
  error text
);

answers (
  id uuid primary key,
  prompt_run_id uuid references prompt_runs(id),
  raw_text text not null,
  normalized_summary text,
  answer_hash text,
  screenshot_url text,
  metadata jsonb
);

mentions (
  id uuid primary key,
  answer_id uuid references answers(id),
  entity_type text not null, -- brand, competitor, source, product
  entity_id uuid,
  entity_name text not null,
  position int,
  recommendation_strength numeric(5,2),
  sentiment numeric(5,2),
  context text,
  is_hallucinated boolean default false
);

sources (
  id uuid primary key,
  workspace_id uuid references workspaces(id),
  url text not null,
  domain text not null,
  title text,
  source_type text,
  authority_score numeric(5,2),
  first_seen_at timestamptz,
  last_seen_at timestamptz,
  unique (workspace_id, url)
);

citations (
  id uuid primary key,
  answer_id uuid references answers(id),
  source_id uuid references sources(id),
  url text not null,
  cited_text text,
  citation_position int,
  supports_brand boolean,
  supports_competitor boolean
);

visibility_scores (
  id uuid primary key,
  brand_id uuid references brands(id),
  period_start date,
  period_end date,
  engine_slug text,
  prompt_filter jsonb,
  ai_visibility_score numeric(6,2),
  share_of_mentions numeric(6,2),
  share_of_recommendations numeric(6,2),
  average_position numeric(6,2),
  citation_share numeric(6,2),
  sentiment_score numeric(6,2),
  component_scores jsonb
);

audits (
  id uuid primary key,
  brand_id uuid references brands(id),
  audit_type text not null, -- site, crawler_logs, source, competitor
  status text not null,
  started_at timestamptz,
  completed_at timestamptz,
  summary jsonb
);

audit_findings (
  id uuid primary key,
  audit_id uuid references audits(id),
  severity text not null,
  finding_type text not null,
  url text,
  title text not null,
  evidence jsonb,
  recommendation_hint text
);

recommendations (
  id uuid primary key,
  brand_id uuid references brands(id),
  title text not null,
  type text not null,
  affected_url text,
  affected_file text,
  reason text not null,
  evidence jsonb not null,
  expected_impact text,
  confidence numeric(5,2),
  effort numeric(5,2),
  priority_score numeric(8,2),
  risk_level text,
  auto_executable boolean default false,
  approval_required boolean default true,
  success_metric text,
  retest_plan text,
  status text not null
);

executions (
  id uuid primary key,
  recommendation_id uuid references recommendations(id),
  execution_type text not null, -- github_pr, cms_draft, markdown, ticket
  status text not null,
  external_url text,
  branch_name text,
  pull_request_number int,
  generated_artifact jsonb,
  approved_by uuid references users(id),
  approved_at timestamptz
);

github_integrations (
  id uuid primary key,
  workspace_id uuid references workspaces(id),
  installation_id text,
  repository_full_name text,
  permissions jsonb,
  status text not null
);

cms_integrations (
  id uuid primary key,
  workspace_id uuid references workspaces(id),
  provider text not null,
  site_id text,
  status text not null,
  credentials_ref text
);

reports (
  id uuid primary key,
  workspace_id uuid references workspaces(id),
  brand_id uuid references brands(id),
  report_type text not null,
  period_start date,
  period_end date,
  status text not null,
  html_url text,
  pdf_url text,
  summary jsonb
);

alerts (
  id uuid primary key,
  workspace_id uuid references workspaces(id),
  brand_id uuid references brands(id),
  alert_type text not null,
  severity text not null,
  title text not null,
  evidence jsonb,
  status text not null,
  triggered_at timestamptz
);

tasks (
  id uuid primary key,
  workspace_id uuid references workspaces(id),
  brand_id uuid references brands(id),
  recommendation_id uuid references recommendations(id),
  title text not null,
  status text not null,
  assignee_id uuid references users(id),
  due_date date,
  external_ref text
);

subscriptions (
  id uuid primary key,
  organization_id uuid references organizations(id),
  plan_code text not null,
  billing_provider text,
  billing_customer_id text,
  status text not null,
  current_period_start date,
  current_period_end date
);

usage_costs (
  id uuid primary key,
  workspace_id uuid references workspaces(id),
  organization_id uuid references organizations(id),
  cost_type text not null,
  provider text,
  units numeric(14,4),
  cost_usd numeric(12,6),
  metadata jsonb,
  occurred_at timestamptz not null
);
```

Vector tables:

```sql
documents (
  id uuid primary key,
  workspace_id uuid references workspaces(id),
  source_id uuid references sources(id),
  url text,
  title text,
  content text,
  content_hash text,
  metadata jsonb
);

document_chunks (
  id uuid primary key,
  document_id uuid references documents(id),
  chunk_index int,
  content text,
  embedding vector(1536),
  metadata jsonb
);
```

## I. API Design

Base path: `/api/v1`

Auth/workspaces:

- `POST /auth/login`
- `POST /auth/logout`
- `GET /me`
- `GET /organizations`
- `POST /organizations`
- `GET /workspaces`
- `POST /workspaces`
- `GET /workspaces/{workspace_id}`

Brands:

- `POST /workspaces/{workspace_id}/brands`
- `GET /brands/{brand_id}`
- `PATCH /brands/{brand_id}`
- `POST /brands/{brand_id}/competitors`
- `GET /brands/{brand_id}/competitors`
- `PATCH /competitors/{competitor_id}`

Prompts:

- `POST /brands/{brand_id}/prompts/generate`
- `GET /brands/{brand_id}/prompts`
- `POST /prompts`
- `PATCH /prompts/{prompt_id}`
- `POST /prompts/{prompt_id}/approve`
- `POST /prompts/bulk-approve`

Monitoring:

- `POST /brands/{brand_id}/monitoring/runs`
- `GET /brands/{brand_id}/monitoring/runs`
- `GET /prompt-runs/{run_id}`
- `GET /prompt-runs/{run_id}/answer`
- `POST /brands/{brand_id}/monitoring/retest`

Answers/mentions/citations:

- `GET /brands/{brand_id}/answers`
- `GET /answers/{answer_id}`
- `GET /brands/{brand_id}/mentions`
- `GET /brands/{brand_id}/citations`
- `GET /brands/{brand_id}/sources`
- `GET /sources/{source_id}`

Audits:

- `POST /brands/{brand_id}/audits/site`
- `POST /brands/{brand_id}/audits/crawler-logs`
- `GET /brands/{brand_id}/audits`
- `GET /audits/{audit_id}`
- `GET /audits/{audit_id}/findings`

Recommendations:

- `POST /brands/{brand_id}/recommendations/generate`
- `GET /brands/{brand_id}/recommendations`
- `GET /recommendations/{recommendation_id}`
- `PATCH /recommendations/{recommendation_id}`
- `POST /recommendations/{recommendation_id}/approve`
- `POST /recommendations/{recommendation_id}/reject`

Executions:

- `POST /recommendations/{recommendation_id}/executions`
- `GET /brands/{brand_id}/executions`
- `GET /executions/{execution_id}`
- `POST /executions/{execution_id}/submit`
- `POST /executions/{execution_id}/mark-complete`

Reports:

- `POST /brands/{brand_id}/reports`
- `GET /brands/{brand_id}/reports`
- `GET /reports/{report_id}`
- `GET /reports/{report_id}/download`

Integrations:

- `GET /workspaces/{workspace_id}/integrations`
- `POST /integrations/github/install`
- `POST /integrations/github/repositories`
- `POST /integrations/wordpress/connect`
- `POST /integrations/webflow/connect`
- `DELETE /integrations/{integration_id}`

Alerts:

- `GET /brands/{brand_id}/alerts`
- `PATCH /alerts/{alert_id}`
- `POST /alerts/{alert_id}/resolve`

Free checker:

- `POST /free-checker/leads`
- `POST /free-checker/runs`
- `GET /free-checker/runs/{run_id}`
- `POST /free-checker/runs/{run_id}/book-demo`

Admin/managed service:

- `GET /admin/workspaces`
- `GET /admin/tasks`
- `POST /admin/tasks`
- `PATCH /admin/tasks/{task_id}`
- `POST /admin/reports/{report_id}/approve`

## J. Workflow Design

Temporal workflows:

### Brand Onboarding Workflow

Input: brand form, competitors, goals.  
Steps: validate domain, normalize brand facts, create workspace records, generate prompts, schedule first monitoring, schedule site audit.  
Output: onboarding status, initial prompt drafts.

### Prompt Generation Workflow

Input: brand, category, location, competitors, goals.  
Steps: template expansion, LLM variants, dedupe, classify intent/persona/location, assign priority, human review queue.  
Output: prompt drafts.

### Monitoring Workflow

Input: prompt set, engines, region/language.  
Steps: cost estimate, run prompts, store raw answers, extract mentions/citations/sentiment, compute metrics, detect alerts.  
Output: prompt runs, answers, metrics.

### Citation Extraction Workflow

Input: answer.  
Steps: parse provider citations, extract URLs, normalize domains, classify source type, crawl metadata, link to sources.  
Output: citations and source records.

### Site Audit Workflow

Input: domain.  
Steps: fetch robots/sitemap, crawl selected pages, extract metadata/schema/content, run checks, create findings.  
Output: audit and findings.

### Recommendation Generation Workflow

Input: weak prompts, citations, audit findings, competitor evidence.  
Steps: diagnose gaps, generate candidate recs, score priority, apply risk guardrails, create approval tasks.  
Output: recommendation list.

### GitHub PR Workflow

Input: approved recommendation and repo.  
Steps: install/verify permissions, detect framework, create branch, apply patch, run static checks if possible, open PR, attach rationale.  
Output: PR URL and execution record.

### Report Generation Workflow

Input: brand, period, report type.  
Steps: aggregate metrics, generate narrative, render HTML, export PDF, create approval queue.  
Output: report.

### Alert Workflow

Input: metric deltas and events.  
Steps: evaluate thresholds, dedupe, create alert, send email/Slack.  
Output: alert record.

### Re-Test Workflow

Input: executed recommendation.  
Steps: wait configurable period, rerun affected prompts/audits, compare before/after, update recommendation status.  
Output: impact evidence.

## K. Agent Architecture

All agents must produce structured outputs, cite internal evidence IDs, track cost, and fail closed when confidence is low.

| Agent | Responsibility | Inputs | Outputs | Tools | Guardrails | Failure Modes | Human Approval |
|---|---|---|---|---|---|---|---|
| Prompt Research Agent | Generate and classify prompts | Brand, category, competitors, locations, personas | Prompt drafts with tags and priorities | LLM, templates, keyword/search APIs | No offensive or regulated unsafe prompts; pt-BR localization | Generic prompts, duplicates, wrong intent | Required before monitoring |
| LLM Monitoring Agent | Run prompts and collect answers | Approved prompts, engines | Raw answers and run metadata | Provider APIs, SERP APIs, manual capture | Respect terms, rate limits, cost caps | Engine errors, API/app mismatch | Not for collection, yes for unsupported manual evidence |
| Citation Extraction Agent | Extract URLs and source mentions | Raw answer | Citations, source records | Parser, LLM extractor, crawler | Do not invent citations | Missed citations, URL canonical issues | No |
| Competitor Intelligence Agent | Compare competitors | Prompt runs, competitor domains, source data | Competitor gap analysis | Crawler, search APIs, LLM | Public data only | Overclaiming causality | Review for reports |
| Site Audit Agent | Audit website | Domain, sitemap | Audit findings | Crawler, schema parser, Lighthouse-like checks | Respect robots, rate limits | JS rendering gaps, blocked pages | No |
| Technical GEO Agent | Diagnose technical visibility | Audit findings, crawler logs | Technical recommendations | Parsers, docs rules | Mark llms.txt experimental | False positives | Yes before execution |
| Content Gap Agent | Find missing content | Weak prompts, site content, competitor pages | Content briefs/drafts | Crawler, vector search, LLM | No legal/medical claims without review | Thin/generic content | Yes |
| Reputation/Review Agent | Find reputation gaps | Reviews/directories, local data | Review strategy, listings gaps | Search APIs, directory data | No fake/incentivized reviews | Missing platform data | Yes |
| Local Visibility Agent | Analyze city/local prompts | GBP/local listings, NAP, prompt runs | Local recommendations | Search APIs, crawler | Respect healthcare/legal ad rules | NAP mismatch false positives | Yes |
| Recommendation Prioritization Agent | Score actions | Diagnostics, effort, goals | Ranked recs | Scoring model, LLM | Explain confidence and risk | Bad priority weights | Consultant review |
| GitHub Remediation Agent | Create code/content PRs | Approved rec, repo | Branch/PR | GitHub App, code parser | No auto-merge, minimal diff | Framework misdetection | Required |
| CMS Draft Agent | Create CMS drafts | Approved rec, CMS | Draft/export | WordPress/Webflow APIs | No auto-publish | Formatting issues | Required |
| Report Agent | Build reports | Metrics, recs, evidence | HTML/PDF report | Renderer, LLM | No unsupported guarantees | Overconfident narrative | Consultant approval |
| QA/Evaluation Agent | Evaluate extraction/recs | Samples, expected outputs | Eval scores, failure cases | Eval harness | Block low-quality recommendations | Weak test set | Internal |
| Cost Control Agent | Enforce budget | Workspace plan, queued jobs | Allow/deny/throttle | Usage DB | Hard budget caps | Over-throttling | Admin override |

## L. Dashboard UX Spec

Design style:

- Modern SaaS dashboard, not a marketing hero inside the app.
- Dense, scannable, professional.
- Portuguese-first.
- Clear evidence cards and action lists.
- Avoid decorative clutter.
- Every score must reveal components.

Screens:

### Login / Onboarding

- Email/password or magic link.
- Workspace/client selector.
- Guided brand setup wizard.

### Brand Setup

- Brand profile.
- Competitors.
- Locations.
- Goals.
- Prompt priorities.
- Integrations.

### Prompt Library

- Table of prompts with intent, persona, location, priority, status.
- Generate prompts.
- Approve/pause/bulk edit.
- Prompt quality warnings.

### Monitoring Dashboard

- AI Visibility Score.
- Mention rate by engine.
- Recommendation share.
- Competitor comparison.
- Trend charts.
- High-value prompt status.
- Recent alerts.
- Top actions.

### Prompt Detail

- Prompt text and metadata.
- Engine snapshots.
- Raw answer.
- Mention order.
- Competitors.
- Citations.
- Sentiment.
- History and volatility.
- Re-test button.

### Competitor Comparison

- Share of mentions/recommendations.
- Average position.
- Source overlap.
- Winning prompt clusters.
- Content/source gaps.

### Citation / Source Graph

- Source domains by influence.
- Source type filters.
- Brand vs competitor citations.
- Opportunity list.

### Diagnosis Page

- Weak prompt clusters.
- Likely causes.
- Evidence panel.
- Related audit findings.
- Recommended actions.

### Recommendations / Action Center

- Prioritized recommendations.
- Type, impact, confidence, effort, risk.
- Approval workflow.
- Create PR/draft/ticket.
- Track status.

### GitHub PRs / Execution

- Connected repos.
- Open PRs.
- Branch status.
- Checklist.
- Re-test after merge.

### Reports

- Report builder.
- Monthly report archive.
- PDF/export.
- White-label toggle.

### Alerts

- Alert inbox.
- Severity, affected prompt, evidence.
- Resolve/snooze/create task.

### Settings / Integrations

- Team members.
- Billing.
- API keys.
- GitHub/CMS/Slack/email.
- Data retention.

### Managed Service Admin

- Client pipeline.
- Onboarding status.
- Monthly report due dates.
- Consultant tasks.
- Approval queues.
- Package/plan status.

### Free Checker Landing Flow

- Public form.
- Progress state.
- Mini-report.
- Lead capture and booking CTA.

## M. Landing Page Spec / Copy

### Page Goal

Convert Brazilian leads into free checker submissions, paid audit bookings, and demo calls.

### Hero

Headline:

Faca sua marca aparecer nas respostas da IA

Subheadline:

Descubra se sua empresa aparece quando clientes perguntam no ChatGPT, Gemini, Perplexity e Google AI. Veja quais concorrentes sao recomendados no seu lugar e receba um plano claro para melhorar sua presenca.

Primary CTA:

Ver minha visibilidade na IA

Secondary CTA:

Agendar diagnostico

Trust line:

Monitoramento, diagnostico e execucao segura. Sem promessas falsas de ranking.

### Product Explanation

GoRank mostra como a IA enxerga sua marca. Monitoramos perguntas reais do seu mercado, comparamos concorrentes, extraimos fontes citadas, auditamos seu site e transformamos os achados em acoes priorizadas.

### How It Works

1. Informe sua marca, site, categoria e concorrentes.
2. Geramos perguntas que seus clientes fariam para a IA.
3. Rodamos o monitoramento nas principais experiencias de IA e busca.
4. Mostramos quem aparece, quem e citado e por que.
5. Criamos um plano de melhoria com drafts, tarefas ou PRs revisaveis.
6. Re-testamos para medir o antes e depois.

### Example Report

Sections:

- Sua visibilidade atual.
- Concorrentes mais recomendados.
- Perguntas em que voce perde.
- Fontes que influenciam as respostas.
- Problemas tecnicos e de conteudo.
- Top 10 acoes recomendadas.

### Competitor Comparison Copy

Sua empresa pode estar bem no Google e invisivel nas respostas da IA. GoRank mostra quando a IA recomenda concorrentes, quais fontes sustentam essas respostas e o que voce pode fazer para competir.

### Use Cases by Vertical

- Juridico: "Qual escritorio contratar para direito trabalhista em Sao Paulo?"
- Clinicas: "Melhor clinica de dermatologia em Belo Horizonte"
- SaaS B2B: "Melhor software de automacao de WhatsApp no Brasil"
- Imobiliarias: "Imobiliaria confiavel em Curitiba"
- Educacao: "Melhor curso de ingles online para adultos"
- E-commerce: "Melhores marcas de [categoria] no Brasil"
- Franquias: "Melhor franquia para investir ate R$ X"

### Free Checker Section

Title:

Teste gratis: sua marca aparece nas respostas da IA?

Fields:

- Marca.
- Website.
- Categoria.
- Concorrentes.
- Cidade/pais.
- Email.

CTA:

Gerar mini relatorio

### Pricing / Demo

Cards:

- Diagnostico de Visibilidade IA.
- Monitoramento Mensal.
- Otimizacao Done-for-you.
- Plano para Agencias.

### Blog / GEO Academy

Content pillars:

- O que e GEO?
- SEO vs GEO vs AEO.
- Como a IA escolhe fontes.
- Como medir visibilidade no ChatGPT.
- Guia de AI visibility para advogados, clinicas, imobiliarias, SaaS e e-commerce.
- Estudos de benchmark por setor no Brasil.

### Lead Capture

CTAs:

- Free checker.
- Paid audit.
- Demo.
- Agency partnership.
- Download benchmark report.

## N. Free Checker Spec

### Inputs

- Brand.
- Website.
- Category.
- Competitors.
- Country/city.
- Email.
- Optional phone/WhatsApp.

### Processing

- Generate 5 to 10 prompt samples.
- Run 1 to 2 compliant engines or search providers.
- Extract brand/competitor mentions.
- Extract citations where available.
- Run shallow homepage audit.
- Compute initial score.

### Output

- Mini AI Visibility Score.
- Sample prompts.
- Brand mentioned/not mentioned.
- Competitors appearing.
- Example answer snippets.
- Source/citation examples.
- Top 3 suspected gaps.
- CTA: book paid audit/demo.

### Lead Rules

- Store free checker runs separately from paid monitoring.
- Rate-limit by domain/email/IP.
- Make methodology clear: sample only, not exhaustive.
- Invite manual expert review.

## O. Managed Service Operating Model

### Roles

- Founder/sales lead: discovery, closing, partnerships.
- AI visibility consultant: onboarding, prompts, diagnosis, reports.
- Technical implementer: site audits, PRs, schema, CMS drafts.
- Content strategist: briefs, comparison pages, FAQs, local pages.
- Account manager: monthly cadence, approvals, renewal.

### Client Workflow

1. Lead via free checker/outbound/referral.
2. Qualification call.
3. Paid audit invoice.
4. Onboarding form.
5. Prompt and competitor approval.
6. Monitoring and site audit.
7. Consultant review.
8. Report delivery call.
9. Retainer proposal.
10. Monthly monitoring and action loop.

### Internal Consultant Dashboard

- Client status.
- Missing onboarding data.
- Prompt approval queue.
- Audit status.
- Recommendation approval.
- Execution status.
- Monthly report due dates.
- Renewal risk.

### Packages

- Starter AI Visibility Audit: one-time baseline.
- Monthly Monitoring: recurring visibility tracking.
- Monitoring + Recommendations: tracking plus prioritized action plan.
- Done-for-you Optimization: tracking, recommendations, drafts/PRs, monthly report.
- Agency White-Label: multi-client dashboard, white-label reports, pitch audits.

### Operational Playbook

Weekly:

- Review alerts.
- Check high-priority prompt losses.
- Update tasks.
- Execute approved drafts/PRs.

Monthly:

- Re-run full monitoring.
- Refresh site audit deltas.
- Generate report.
- Hold client review.
- Select next 3 actions.

Quarterly:

- Benchmark against industry.
- Refresh prompt set.
- Review competitors.
- Adjust package and goals.

## P. Pricing Model

Brazil-friendly, service-led pricing. Exact pricing should be validated with first 10 customers.

### One-Time Audit

- Starter AI Visibility Audit: R$ 1.500 to R$ 3.000.
- Advanced Audit with competitor/source analysis: R$ 3.500 to R$ 7.500.
- Agency prospect audit bundle: R$ 800 to R$ 1.500 per client when bought in packs.

USD equivalent for global later:

- $300 to $600 starter audit.
- $700 to $1,500 advanced audit.

### Monthly Monitoring

- Starter Monitoring: R$ 490 to R$ 990/mo.
  - 1 brand, 30 prompts, 2 engines, monthly report.
- Growth Monitoring + Recommendations: R$ 1.500 to R$ 3.500/mo.
  - 1 brand, 75 to 150 prompts, 3 engines, recommendations, alerts.
- Done-for-you Optimization: R$ 4.000 to R$ 10.000/mo.
  - Monitoring, reports, drafts/PRs, content briefs, monthly execution.

### Agency

- Agency Starter: R$ 2.500 to R$ 5.000/mo for 5 clients.
- Agency Growth: R$ 7.500 to R$ 15.000/mo for 15 to 25 clients.
- White-label custom: from R$ 20.000/mo.

### Future SaaS-Only Tiers

- Free checker.
- Solo: $49 to $99/mo.
- SMB: $149 to $299/mo.
- Agency: $499 to $999/mo.
- Enterprise: custom.

Pricing principle:

- Managed service should subsidize learning and dataset creation.
- SaaS pricing later should be usage-based on prompt checks, engines, brands, and report seats.

## Q. 30-Day Implementation Plan Summary

See companion plan: `docs/superpowers/plans/2026-05-10-gorank-30-day-mvp.md`.

Milestones:

- Week 1: Repo foundation, schema, onboarding, prompt generation.
- Week 2: Monitoring, extraction, metrics, prompt dashboard.
- Week 3: Site audit, recommendations, reports, free checker.
- Week 4: managed service workflow, execution artifacts, pilot hardening.

## R. Epics and User Stories

### Epic 1: Brand Onboarding

- As a user, I can create a workspace so that each client/brand is isolated.
- As a user, I can enter brand, domain, category, location, competitors, and goals so that GoRank can generate relevant monitoring.
- As a consultant, I can edit canonical brand facts so that reports can detect hallucinations.

### Epic 2: Prompt Discovery

- As a user, I can generate pt-BR prompts by category and intent.
- As a user, I can approve or pause prompts.
- As a consultant, I can add manual prompts from discovery calls.

### Epic 3: Monitoring

- As a user, I can run approved prompts against supported engines.
- As a user, I can view raw answer evidence.
- As a user, I can see whether my brand and competitors were mentioned.

### Epic 4: Metrics

- As a user, I can see AI Visibility Score and components.
- As a user, I can compare competitors by prompt cluster.
- As a user, I can track visibility changes over time.

### Epic 5: Citation Intelligence

- As a user, I can see which sources were cited.
- As a consultant, I can classify sources and identify opportunities.
- As a user, I can see citation overlap with competitors.

### Epic 6: Site Audit

- As a user, I can audit my website for crawlability, schema, content gaps, and entity clarity.
- As a consultant, I can link audit findings to recommendations.

### Epic 7: Recommendations

- As a user, I can see prioritized actions with impact, confidence, effort, and risk.
- As a user, I can approve/reject recommendations.
- As a consultant, I can create tasks from recommendations.

### Epic 8: Reports

- As a user, I can generate an executive report.
- As an agency, I can export a white-label report.
- As a consultant, I can include completed fixes and next actions.

### Epic 9: Free Checker

- As a prospect, I can enter brand details and receive a mini visibility report.
- As the GoRank team, we capture qualified leads.

### Epic 10: Execution

- As a user, I can generate a CMS-ready draft.
- As a developer, I can receive a GitHub PR with a clear rationale.
- As a consultant, I can track execution and re-test after shipping.

## S. First Vertical Slice Plan

Recommended first vertical: Brazilian law firm or clinic.

Why:

- High-value leads.
- Local intent matters.
- Buyers ask trust/comparison questions.
- Website quality varies widely.
- Managed service willingness is higher than micro-SMB.

Flow:

1. Client enters brand, domain, city, practice/specialty, competitors.
2. GoRank generates 30 prompts:
   - 10 local commercial.
   - 8 comparison/alternatives.
   - 6 informational with buyer intent.
   - 4 reputation/trust.
   - 2 branded fact-check prompts.
3. Runs monitoring across selected engines/providers.
4. Extracts brand/competitor mentions and citations.
5. Audits website.
6. Generates top 10 recommendations.
7. Produces PDF report.
8. Generates one execution artifact:
   - Organization/LocalBusiness schema PR.
   - FAQ section draft.
   - Local service page brief.
   - llms.txt draft marked experimental.
9. Re-tests affected prompts after approval and publication.

Success criteria:

- Client sees at least one competitor insight they did not know.
- Report identifies at least 5 actionable fixes.
- Client agrees to retainer or paid implementation.

## T. Risk Register

| Risk | Severity | Likelihood | Mitigation |
|---|---:|---:|---|
| Overclaiming LLM ranking guarantees | High | Medium | Strict positioning, report disclaimers, sales training |
| Terms violations from scraping consumer tools | High | Medium | API-first, legal review, manual evidence where needed |
| API outputs differ from consumer app outputs | Medium | High | Label source clearly, support evidence screenshots/manual runs |
| High LLM/SERP cost | Medium | High | Cost caps, prompt sampling, caching, batch schedules |
| Poor extraction quality | High | Medium | Structured schemas, eval set, human QA for reports |
| Generic recommendations | High | Medium | Evidence-required recommendations and consultant review |
| Brazil-specific prompt quality weak | High | Medium | Build prompt library from interviews and audits |
| Legal/medical content risk | High | Medium | Human expert review, no unverified claims |
| Customer expects instant visibility lift | Medium | High | Set expectations: probability, monitoring, before/after |
| Competitors move fast | Medium | High | Differentiate with localization and execution |
| Multi-tenant data leak | Critical | Low/Medium | Tenant-scoped DB, tests, RBAC, audit logs |
| GitHub permissions too broad | High | Medium | Least privilege, repo selection, no write until approval |
| Generated PR breaks site | High | Medium | Small diffs, framework detection, tests, no auto-merge |
| Free checker abuse | Medium | High | Rate limits, email validation, quotas |
| SEO spam perception | High | Medium | Quality policy, no spam automation, transparent evidence |

## U. What Not To Build In MVP

- Full billing/subscription system.
- Enterprise SSO.
- Deep BI/report builder.
- Browser automation farm.
- Every AI engine.
- Fully automated CMS publishing.
- Auto-merge GitHub PRs.
- Large-scale backlink/link-building module.
- Review solicitation automation.
- Wikipedia/Wikidata editing workflows.
- Complex vector knowledge graph.
- Public benchmark database before enough data exists.
- Mobile app.
- Full white-label agency portal beyond report branding.
- Real-time monitoring for all prompts.
- Proprietary AI search volume model.

## V. Questions / Unknowns To Validate

### Customer and GTM

1. Which first vertical pays fastest: law firms, clinics, B2B SaaS, agencies, real estate, or education?
2. Do SMBs understand "AI visibility" enough to buy, or should the first offer be "paid audit" only?
3. What price point closes in Brazil without long education?
4. Do agencies want white-label reports or API/data access first?
5. Which outbound angle converts best: "your competitors appear in ChatGPT" vs "free AI visibility score"?

### Product

1. Which engines matter most for Brazilian buyers today?
2. How different are API answers from consumer app answers for target categories?
3. Which prompts produce repeatable enough signals for monthly reporting?
4. What evidence format makes clients trust the report?
5. Which recommendations are easiest to approve and ship?

### Technical

1. Which SERP/API providers can legally and reliably monitor Google AI Overviews in Brazil?
2. Which crawler logs can customers realistically provide?
3. Can GitHub PR generation be useful across common Brazilian SMB stacks?
4. Should MVP use pgvector or Qdrant?
5. Which extraction eval metrics correlate with consultant trust?

### Evidence

1. Which source types influence AI answers in Portuguese local categories?
2. How often do citations overlap with classic Google top results?
3. Do comparison/alternatives pages improve AI mentions for Brazilian SMBs?
4. Does llms.txt provide any measurable benefit for non-developer SMB websites?
5. Which review platforms are cited by AI engines in Brazil?

## Go-To-Market Plan

### Initial 3 Verticals

1. Law firms.
2. Clinics/healthcare providers.
3. B2B SaaS/agencies.

Rationale:

- High customer value.
- Clear commercial prompts.
- Competitor visibility matters.
- Content/site improvements are feasible.
- Managed service budgets exist.

### First 10 Customers Plan

1. Build 50-account target list by vertical.
2. Run lightweight manual/free checker samples for top prospects.
3. Send personalized outbound:
   - "A IA esta recomendando [competitor] quando perguntamos sobre [category] em [city]. Quer ver o relatorio?"
4. Offer paid audit at founder-led discount.
5. Deliver high-quality report within 5 business days.
6. Convert to 3-month retainer.
7. Publish anonymized benchmark/case study.

### Founder-Led Sales Script

Opening:

"Hoje muitos clientes nao pesquisam so no Google. Eles perguntam para ChatGPT, Gemini, Perplexity e Google AI qual empresa contratar. O problema e que a maioria das empresas nao sabe se aparece nessas respostas."

Problem:

"Nos medimos perguntas reais do seu mercado, vemos se sua marca aparece, quais concorrentes sao recomendados, quais fontes a IA usa e quais ajustes aumentam sua chance de ser mencionada e citada."

No guarantee:

"Nao prometemos ranking garantido em IA. O que entregamos e diagnostico com evidencia, execucao segura e acompanhamento antes/depois."

Offer:

"O primeiro passo e um Diagnostico de Visibilidade IA. Voce recebe um relatorio com prompts, concorrentes, fontes citadas, problemas do site e 10 acoes priorizadas."

### Channels

- Free checker landing page.
- LinkedIn founder content.
- Cold email/WhatsApp to vertical lists.
- SEO/GEO academy in Portuguese.
- Benchmark reports by vertical.
- Partnerships with SEO/web agencies.
- Webinars for agencies.
- "AI visibility audit" productized service marketplaces.

### Validation Experiments

1. 10 customer discovery interviews.
2. 5 paid audits.
3. 3 managed service pilots.
4. 1 free checker waitlist campaign.
5. 1 benchmark report.
6. 1 agency partnership test.

## Security and Compliance

### Multi-Tenant Isolation

- Tenant-scoped rows with `organization_id`/`workspace_id`.
- Enforce access in service layer and database policies where possible.
- Audit tests for cross-tenant access.

### Secrets

- Store provider API keys and integration tokens in a secrets manager.
- Never store raw OAuth tokens in application tables.
- Rotate secrets.

### GitHub

- Minimal permissions.
- Repository selection.
- No auto-merge.
- No secrets exfiltration.
- Redact sensitive files from analysis.

### Audit Logs

Track:

- Login.
- Integration connect/disconnect.
- Prompt run.
- Report generation.
- Recommendation approval/rejection.
- Execution artifact creation.
- External publication status.

### Rate Limits and Cost Controls

- Workspace quotas.
- Engine-specific rate limits.
- Free checker abuse protection.
- Daily cost caps.

### Data Retention

- Configurable retention by plan.
- Free checker data retained for lead follow-up with consent.
- Delete client data on request where legally required.

### Legal / ToS

- Use official APIs whenever possible.
- Use SERP/data providers with compliant terms.
- Crawl public web respectfully.
- Avoid restricted/private content.
- Document unsupported engine monitoring as manual or experimental.

### Ethical Policy

- No deceptive manipulation.
- No spammy content automation.
- No fake reviews.
- No black-hat SEO.
- No hidden bot-only claims.
- Human approval for external publication.

## Moat Strategy

Data moat:

- Proprietary prompt sets by vertical, language, region, and persona.
- Longitudinal answer/citation snapshots.
- Competitor and source benchmarks.
- Recommendation effectiveness data.
- Before/after impact data.

Workflow moat:

- Managed service playbooks encoded into product.
- PR/CMS execution patterns.
- Agency white-label distribution.

Brand moat:

- Portuguese GEO academy.
- Brazil benchmark reports.
- Case studies.
- Free checker dataset loop.

## Research Sources

Primary and authoritative sources used in this blueprint:

- Profound: `https://www.tryprofound.com/`
- Scrunch: `https://scrunch.com/` and `https://scrunch.com/pricing`
- Peec AI: `https://peec.ai/` and `https://peec.ai/pricing`
- Otterly AI: `https://otterly.ai/` and `https://otterly.ai/pricing`
- AthenaHQ: `https://athenahq.ai/`
- Ahrefs Brand Radar: `https://ahrefs.com/brand-radar`
- Semrush One and AI visibility docs/news: `https://www.semrush.com/one/`, `https://www.semrush.com/kb/1626-ai-visibility-features`, `https://investors.semrush.com/news/news-details/2025/Semrush-Launches-Semrush-One-Empowering-Marketers-to-Win-Every-Search-in-the-AI-Era/default.aspx`
- Writesonic pricing: `https://writesonic.com/pricing`
- SE Visible: `https://visible.seranking.com/` and `https://help.seranking.com/hc/en-us/articles/22266372506524-SE-Visible-FAQ`
- Azoma: `https://www.azoma.ai/enterprise`
- Limy: `https://www.limy.ai/` and `https://limy.ai/pricing`
- AirOps: `https://www.airops.com/ai-search-visibility`
- Quattr: `https://www.quattr.com/features/generative-engine-optimization`
- Google AI features and website guidance: `https://developers.google.com/search/docs/appearance/ai-overviews`
- Google crawler documentation: `https://developers.google.com/crawling/docs/crawlers-fetchers/overview-google-crawlers`
- Google common crawlers and Google-Extended: `https://developers.google.com/crawling/docs/crawlers-fetchers/google-common-crawlers`
- Google structured data introduction and feature docs: `https://developers.google.com/search/docs/appearance/structured-data/intro-structured-data`
- OpenAI crawlers: `https://developers.openai.com/api/docs/bots`
- Perplexity crawlers: `https://docs.perplexity.ai/docs/resources/perplexity-crawlers`
- llms.txt proposal: `https://llmstxt.org/`
- GEO paper: `https://arxiv.org/abs/2311.09735`
- "Generative Engine Optimization: How to Dominate AI Search": `https://arxiv.org/abs/2509.08919`
- AgenticGEO: `https://arxiv.org/abs/2603.20213`

## Spec Self-Review

- Completeness scan: no unresolved markers remain.
- Scope check: this blueprint intentionally covers the complete product/business/technical concept, but MVP execution is separated into a 30-day plan.
- Ambiguity check: unsupported AI engine monitoring is explicitly marked API/search-provider/manual, not assumed automated.
- Evidence check: strategies are separated into evidence-backed, plausible, speculative, and risky/avoid.
- Safety check: no guarantee of LLM rankings; no auto-publish or auto-merge in MVP.
