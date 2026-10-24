# API Archaeology

**Working with APIs you don't understand (yet)**

Talk given at [DevFest Venezia 2026](https://gdg.community.dev/gdg-venezia/) — 24 October 2026, Campus Scientifico Ca' Foscari, Mestre.

Most developers love building new APIs. Far fewer know how to work with existing ones, especially when documentation is missing, behaviour is unclear, and the original authors are no longer around. This talk is about reconstructing, validating and safely evolving an API you inherited — not about clean design from scratch.

---

## Slides

📄 [`slides/api-archaeology-devfest-venezia-2026.pdf`](slides/api-archaeology-devfest-venezia-2026.pdf)

💬 Were you in the room? [Rate the talk on OpenFeedback](https://openfeedback.io/BLKfpVftjylgOi1Dssd3/2026-10-24/1300983) — feedback is how the next version gets better.

---

## The six layers

The talk is structured like a dig: each layer only makes sense once the one above it does.

| Layer | What it answers |
| --- | --- |
| 1 · The dig site | Why most of our work happens in code we didn't write |
| 2 · Survey the surface | How to get oriented without reading everything |
| 3 · The toolkit | What to actually open, query and run |
| 4 · Handle with care | How to know what you'll break before you break it |
| 5 · Grow the new around the old | How to modernise without a rewrite |
| 6 · Field report | A real migration: Express on Node 6 → AWS Lambda |

---

## Your field guide

The six things worth remembering:

1. **Survey the surface first.** Use cases before code. What the system is *for* constrains what the code can mean.
2. **Trace flows, park the unknowns.** Follow one request end to end. Write down what you don't understand instead of stopping to chase it.
3. **Wait for the click, then dig.** There's a moment when the shape of the system snaps into place. Deep diving before it is wasted effort.
4. **Prove it with tests.** Characterization tests record what the code *does*, bugs included — not what it should do.
5. **Never fix an island.** A change that looks local rarely is. Follow the data out of your endpoint before you touch it.
6. **Grow the new around the old.** Additive before subtractive, one slice of traffic at a time.

### Five questions before any change

1. **Who consumes this?** Frontends, other services, scripts, that forgotten cron job.
2. **What does it return today, exactly?** Fields, order, nulls, status codes, error shapes.
3. **What else reads or writes this data?** Other endpoints, batch jobs, reports, triggers.
4. **Is today's behaviour covered by a test?** If not, write a characterization test first.
5. **How do I roll back?** A feature flag, a revert plan, a way to undo data changes.

### Finding the consumers nobody remembers

When question 1 has no answer, don't guess — measure:

- Identify callers from **auth**: API key, client id, token claims.
- **Count usage per field**, per consumer. Half the payload is usually always null; the other half is somebody's contract.
- Ship **deprecation logging** on the field you want to change, then wait a month and read it.
- Know the share of traffic you **cannot attribute** to anyone. That number is your real risk budget.

---

## Resources

**On not rewriting**

- Joel Spolsky, [*Things You Should Never Do, Part I*](https://www.joelonsoftware.com/2000/04/06/things-you-should-never-do-part-i/) (2000) — the Netscape rewrite, and why old code is ugly for reasons.
- Martin Fowler, [*Strangler Fig Application*](https://martinfowler.com/bliki/StranglerFigApplication.html) — described in 2004 as "Strangler Application"; the [original text](https://martinfowler.com/bliki/OriginalStranglerFigApplication.html) is still worth reading.

**On working with what's there**

- Michael Feathers, *Working Effectively with Legacy Code* (Prentice Hall, 2004) — the source of characterization tests.
- [Hyrum's Law](https://www.hyrumslaw.com/) — with enough consumers, every observable behaviour becomes somebody's dependency.
- [Chesterton's fence](https://en.wikipedia.org/wiki/Wikipedia:Chesterton%27s_fence) — don't remove what you can't explain the purpose of.

**Tools mentioned**

- Log aggregation queries (CloudWatch Logs Insights, Loki, Datadog — the dialect doesn't matter) to inventory live endpoints.
- Infrastructure as code (CloudFormation, CDK, Terraform, docker-compose) as a declarative inventory of what exists and what is wired to what.
- Schema inference from real payloads ([valibot](https://valibot.dev/), [zod](https://zod.dev/), [TypeBox](https://github.com/sinclairzx81/typebox), [ajv](https://ajv.js.org/)).

---

## About

I'm Matteo Valerio, a developer at **Air srl** (connected mobility), working mostly on Node.js/TypeScript backends, React frontends and AWS.

- LinkedIn: [matteo-valerio-dev](https://www.linkedin.com/in/matteo-valerio-dev)
- GitHub: [@MatteoValerio](https://github.com/MatteoValerio)

The case study in Layer 6 is deliberately described without product, domain or service names. The method is the point; the specifics aren't mine to publish.

---

## Credits & licence

Strangler fig photograph by **Vinayaraj**, [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0), via Wikimedia Commons. The photo keeps its own licence.

Everything else in this repository — slides and text — is released under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0): use it, adapt it, give credit. If you give a version of this talk, I'd love to hear how it went.