## 2. Solution and Project Structure

Use this baseline for a business-focused solution; omit projects without a real responsibility.

```text
Acme.Commerce.sln
src\
  Acme.Commerce.Domain\
  Acme.Commerce.Application\
  Acme.Commerce.Infrastructure\
  Acme.Commerce.Api\
  Acme.Commerce.Worker\                 (when needed)
tests\
  Acme.Commerce.Domain.UnitTests\
  Acme.Commerce.Application.UnitTests\
  Acme.Commerce.Infrastructure.IntegrationTests\
  Acme.Commerce.Api.IntegrationTests\
  Acme.Commerce.ExternalIntegrationTests\
```

| Project | Owns | References |
|---|---|---|
| Domain | Business concepts, invariants, domain policies and events | No other solution layer |
| Application | Use cases, application policies, ports and results | Domain |
| Infrastructure | Persistence, messaging and external adapters | Application, Domain |
| Api / Worker | Transport adapters, host configuration and composition root | Application; Infrastructure for registration |

- **MUST** confine host access to infrastructure implementations to composition and registration; endpoints and consumers invoke application contracts.
- **SHOULD** use fewer projects for small applications when responsibilities remain clear. Project count is not a quality measure.
- **SHOULD** align project directory, project filename, assembly name, and root namespace. Use the repository's supported solution format (`.sln` or `.slnx`).
- For larger systems, **MAY** partition projects by business module before layer, such as `Commerce.Ordering.Domain`. Do not create every module/layer combination preemptively.
- **MUST NOT** create a catch-all shared project or shared domain model to bypass module ownership. Extract genuinely shared concepts only with explicit ownership and compatible semantics.
