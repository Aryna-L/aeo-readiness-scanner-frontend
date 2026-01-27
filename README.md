AEO Readiness Scanner

Analyzes any webpage and generates a 0-100 score based on AEO factors. Identifies gaps and provides prioritized recommendations.

How Scoring Works (100 Points Total)

| Component | Points | What It Checks |
| --- | --- | --- |
| **Schema Markup** | 15 | Presence of valid JSON-LD structured data |
| **FAQ Structure** | 10 | Dedicated FAQ sections with Q&A pairs |
| **Question Headers** | 10 | H2/H3 tags formatted as questions |
| **Header Hierarchy** | 10 | Proper H1-H6 structure (one H1, no skipped levels) |
| **Answer Coverage** | 40 | Direct answers in opening paragraphs |
| **Content Depth** | 15 | Paragraph count and substance |

Why These Weights?

Answer Coverage = 40% because research shows answer quality is the single biggest factor in AI citations. You can have perfect schema and structure, but if you don't directly answer questions, AI engines won't cite you.

Schema = 15% because it helps AI understand content structure and extract information reliably.

Everything else = 45% because structure, headers, and FAQs make content easier to parse but don't guarantee citations.

How It Actually Works

Technical Process

```
1. User provides URL → Backend fetches HTML
2. Cheerio parses DOM structure
3. Six scoring functions analyze different aspects:
   - findSchemaScripts() → looks for <script type="application/ld+json">
   - findFAQSections() → checks for FAQ headings and question marks
   - countQuestionHeaders() → filters H2/H3 for "?" or question words
   - validateHeaderHierarchy() → ensures proper H1-H6 usage
   - evaluateAnswerQuality() → checks first paragraph patterns
   - countContentDepth() → filters paragraphs > 50 characters
4. Weighted calculation combines scores
5. Recommendation engine prioritizes issues

```

Schema Detection

What counts:

- Valid JSON-LD with `@context` and `@type`
- Common types: Article, FAQPage, HowTo, Product, LocalBusiness, Organization, Person

Scoring:

- 0 schemas = 0 points
- 1 schema = 10 points
- 2+ schemas = 15 points

Answer Coverage Logic

Pattern matching for definitions:

- "is a", "is an", "refers to", "means", "defined as"
- "involves", "includes", "consists of"

Checks for:

- First paragraph length (50-300 chars = good)
- Definition patterns in opening
- Multiple substantial paragraphs (>100 chars)
- Examples mentioned
- Lists or structured data

This is the simplest part of the tool but weighted highest because it matters most.

When to Use

✅ Use Scanner for:

- Quick page evaluation (3 seconds)
- Batch analysis (multiple URLs)
- Monthly monitoring
- Identifying obvious gaps

❌ Don't use Scanner for:

- Understanding why content isn't cited (use Auditor Pro)
- Generating specific content fixes
- Competitive analysis (requires manual testing)

Interpreting Scores

85-100: Excellent—ready for AI platform testing

70-84: Good—fix 1-2 gaps

60-69: Fair—missing key elements

Below 60: Poor—needs major restructuring

Common pattern: Pages scoring in 60s usually have some schema but weak answer coverage (scoring 20-25/40 instead of 35+/40).
