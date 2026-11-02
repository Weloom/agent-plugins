## Map contexts and preserve model integrity across boundaries

Use when a change crosses models, integration contracts, or team ownership. Establish the actual model relationships before proposing shared code or translation; keep local cleanup local and map only the affected scope.

### Map the current reality before proposing a new design

- Identify each **bounded context**: the scope within which a model and its language have consistent meanings. A context is not automatically a class, module, aggregate, deployment, or microservice.
- Trace representative domain scenarios through the existing code and integrations. Look for changes in terminology, identity, rules, ownership, and assumptions that reveal where one model stops and another begins.
- Distinguish legitimate differences between contexts from accidental inconsistency within one context. The same word can represent different concepts in different contexts; different names can also conceal a genuinely shared concept.
- Create or update a **context map** of the existing system before drawing a desired future map. Include legacy and external systems even when their models are implicit, awkward, or outside the team's control.
- For each context, record its name, responsibility, model ownership, and relevant team. For each relationship, record:
  - The points of contact and what information or functionality crosses them.
  - The direction of dependency: who supplies a model or contract, and who must adapt when it changes.
  - Where translation occurs and which team maintains it.
  - Whether changes are negotiated, jointly owned, or imposed by one side.
  - The integration pattern actually used, including accidental sharing or undefined arrangements.
- Use a small diagram, a textual map, or both. Its purpose is shared understanding of boundaries and relationships, not documentation volume. A list of services and network calls alone is not a context map.

### Analyze the relationship before choosing a pattern

1. **Is integration necessary and valuable?**
   - If the features can meet their requirements independently, consider **Separate Ways**. Related screens or use cases do not by themselves require shared domain models or integrated implementations.
   - If integration is indispensable, identify the minimum required exchange and continue the analysis.
2. **Can the teams make and sustain mutual commitments?**
   - For distinct upstream and downstream models, consider **Customer/Supplier** when downstream needs can influence upstream priorities and both teams can honor the agreement.
   - Consider a **Shared Kernel** only when a small, genuinely common model is worth joint ownership and coordinated changes. Do not choose it merely because code looks similar.
   - If the upstream team cannot or will not accommodate downstream needs, do not plan around promises of cooperation; assess the downstream options explicitly.
3. **Can the downstream context safely adopt the upstream model?**
   - If its concepts and rules fit the downstream purpose and the loss of model autonomy is acceptable, **Conformist** can remove unnecessary semantic translation.
   - If adopting that model would distort important downstream concepts or rules, use an **Anticorruption Layer** to preserve the downstream model while retaining the necessary integration.
   - Complexity alone does not determine the choice. An anticorruption layer adds translation and maintenance cost; use it to protect meaningful model differences, not simply because an API is complicated.
4. **How should a provider support its consumers?**
   - Consider an **Open Host Service** when multiple consumers need a coherent, reusable integration protocol rather than individual integrations.
   - Consider a **Published Language** to define a documented interchange model. It can complement an Open Host Service and coexist with translation into each consumer's own model.

These are decision aids, not a mandatory sequence or a worst-to-best ranking. They apply between distinct contexts; they do not require splitting one coherent context. Separate Ways can be the best result when integration has no value. A Shared Kernel requires more coordination, not inherently better design. Several patterns can describe different aspects or sides of the same relationship.

### Choose and make the relationship explicit

| Pattern | Appropriate result of the analysis | Coding and maintenance guidelines |
|---|---|---|
| **Separate Ways** | Integration provides insufficient value or the capabilities can remain independent. | Keep domain logic and models independent. Do not reintroduce coupling through shared domain libraries, database structures, or hidden synchronization. Keep any necessary coordination or exchange minimal and explicit. |
| **Anticorruption Layer** | Integration is required, but the foreign model would undermine the local model. | Expose operations in local domain terms and translate concepts, behavior, identities, and rules at the boundary. Keep foreign types and assumptions from leaking into the local domain. Transport wrappers and field renaming alone are not semantic protection. |
| **Conformist** | The downstream team has little influence and can accept the upstream model for the integrated area. | Adopt its semantics deliberately; technical format conversion may still be necessary. Make upstream ownership, constraints, and change exposure explicit. Do not pretend that conformity provides joint control. |
| **Open Host Service** | A provider needs to support multiple integrations through a stable, coherent protocol. | Define a service protocol consumers can use without access to internal implementations. Keep it coherent as it evolves; handle unusual consumer-specific needs with dedicated translation rather than distorting the common protocol. |
| **Customer/Supplier** | There is a directional dependency and the supplier can commit to the customer's integration needs. | Negotiate requirements, priorities, and change expectations. Jointly define automated acceptance tests for the expected interface and run them in the supplier's integration process. Keep the models distinct where their purposes differ. |
| **Published Language** | Systems need a documented common vocabulary and interchange model. | Specify the meaning and structure of exchanged information; use an established language when it fits. Translate between that language and local models as needed. A schema or serialization format without agreed semantics is insufficient. |
| **Shared Kernel** | Teams benefit from sharing a small, carefully selected part of the domain model and can maintain it together. | Define the exact shared model and associated code or database design. Consult affected teams before changes, integrate frequently, and test the combined behavior. Keep the kernel small; a shared utility library is not automatically a Shared Kernel. |

- Published Language means a shared language for integration, not necessarily a declarative programming style. Declarative domain design is a separate concern.
- Open Host Service and Published Language address an integration contract; they do not by themselves establish equal influence, joint ownership, or a customer/supplier agreement.
- Treat shared domain models as explicit collaboration commitments, not convenient reuse. Avoid deduplicating concepts across contexts solely because they currently have similar fields or implementations.

### Refactor the boundary and verify the outcome

- State the observed problem, current relationship, proposed relationship, and reason for the change. Separate code evidence from assumptions about team authority or domain meaning; confirm those assumptions with the responsible people.
- Record the selected relationship and its ownership; do not infer a model-sharing decision from technical dependency alone.
- For a transition, specify which responsibilities move, where translation will live, who owns the resulting contracts, and how existing callers will continue to work. A target context map does not replace the current map until the implementation and working arrangements actually match it.
- Test boundary semantics, not just successful serialization or connectivity: verify identifiers, meanings, valid state changes, and important rules on both sides. Test that foreign assumptions do not leak through a protective boundary.
- Within a bounded context, integrate frequently and run automated tests to keep the shared model coherent. Across contexts, verify the agreed contracts without forcing all participants into one internal model.
- Update the context map and affected contracts when the transition is complete. A local cleanup must not silently change a context boundary, shared-kernel ownership, or a cross-team agreement.
