## Review checklist

Use this checklist to guide investigation, not as a requirement to change code for every item.

- Is the intent clear from names, structure, and call sites?
- Does each function, type, and module have a coherent responsibility?
- Are side effects, dependencies, and failure paths visible?
- Does each abstraction protect a meaningful boundary or clarify a real concept?
- Are the changed behavior and important edge cases covered by reliable tests?
- Does the change preserve behavior where required?
- Is there a relevant opportunity to remove duplication, dead code, hidden coupling, or an invalid state safely?
- Does the change follow repository conventions and stay within task scope?
