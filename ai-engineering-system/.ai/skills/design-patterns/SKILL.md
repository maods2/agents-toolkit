---
name: design-patterns
description: Select and apply design patterns pragmatically. Use when recurring design forces appear, such as object creation, behavior variation, orchestration, adaptation, or decoupling.
---

# Design Patterns

## Purpose

Use known patterns as vocabulary for recurring design problems, not as mandatory structure.

## Source framing

This skill follows the Refactoring.Guru framing of design patterns as reusable blueprints for common software design problems. It uses the classic catalog categories as a navigation aid:

- **Creational**: object creation and construction.
- **Structural**: object composition, adaptation, and interface shaping.
- **Behavioral**: responsibility flow, algorithms, state transitions, and communication.

## When to use

Use this skill when the same design force appears repeatedly or a pattern can simplify communication and implementation.

## How to apply a pattern

1. **Name the design force**: what varies, what is hard to test, what is coupled, or what is repeated?
2. **Try the direct solution first**: inline logic, a helper function, or a small class may be enough.
3. **Select the smallest pattern** that removes the force without adding unused extension points.
4. **Name the participants** in domain language, then optionally note the pattern role.
5. **Add one concrete example** in the code or documentation so future maintainers know how to extend it.
6. **Verify the payoff**: easier testing, lower coupling, simpler extension, or clearer orchestration.

## Decision rules

- Start from the problem, not the pattern name.
- Prefer the simplest pattern that resolves the force.
- Keep pattern participants visible and named.
- Document why the pattern is useful in this context.
- Favor composition over inheritance when both are viable.
- Avoid adding a pattern when the only benefit is future-proofing.

## Pattern example catalog

Use these examples to choose a pattern by problem shape. The examples are intentionally implementation-neutral so they can be adapted to any language.

### Creational patterns

#### Factory Method

- **Use when** one workflow needs to create different product variants but should not know their concrete classes.
- **Example**: a notification service calls `create_sender(channel)` and receives an email, SMS, or push sender depending on the channel.
- **Participants**: creator, concrete creator or factory function, product interface, concrete products.
- **Avoid when** a simple constructor call or small conditional appears in only one place and is unlikely to vary.

#### Abstract Factory

- **Use when** a system must create related families of objects that must be compatible.
- **Example**: a UI renderer receives a `ThemeFactory` that creates matching buttons, dialogs, and form controls for light, dark, or high-contrast themes.
- **Participants**: abstract factory, concrete factories, abstract products, concrete products.
- **Avoid when** only one product type varies; Factory Method is usually smaller.

#### Builder

- **Use when** constructing an object requires many optional parts, ordered steps, validation, or readable setup.
- **Example**: a report builder assembles filters, columns, grouping, sorting, and export options before producing an immutable report request.
- **Participants**: builder, concrete builder, product, optional director.
- **Avoid when** the object has only a few required fields; use a constructor or named parameters instead.

#### Prototype

- **Use when** cloning a configured object is cheaper or clearer than rebuilding it from scratch.
- **Example**: a workflow engine clones a preconfigured approval workflow template, then changes only the requester and approver groups.
- **Participants**: prototype interface, concrete prototype, clone operation, client.
- **Avoid when** object identity, resource ownership, or deep-copy semantics are unclear.

#### Singleton

- **Use when** exactly one instance must coordinate shared state or access to a resource.
- **Example**: a process-wide clock, metrics registry, or configuration provider is initialized once and reused.
- **Participants**: singleton class or module, controlled access point.
- **Avoid when** it hides dependencies, makes tests order-dependent, or acts as global mutable state.

### Structural patterns

#### Adapter

- **Use when** existing code exposes the wrong interface for the client that needs it.
- **Example**: a payment adapter translates a third-party gateway response into the application's `PaymentResult` interface.
- **Participants**: target interface, adapter, adaptee, client.
- **Avoid when** changing the original interface is safe and simpler.

#### Bridge

- **Use when** an abstraction and its implementation need to vary independently.
- **Example**: a `Report` abstraction supports summary and detailed reports while output implementations support PDF, CSV, and HTML.
- **Participants**: abstraction, refined abstractions, implementation interface, concrete implementations.
- **Avoid when** only one side varies; Strategy or simple composition may be enough.

#### Composite

- **Use when** clients should treat individual objects and object groups uniformly.
- **Example**: a permissions model evaluates both single permissions and nested permission groups through the same `is_allowed` operation.
- **Participants**: component interface, leaf, composite, client.
- **Avoid when** group behavior differs so much that a shared interface becomes misleading.

#### Decorator

- **Use when** behavior should be added around an object without changing the object or subclassing it.
- **Example**: an HTTP client is wrapped with retry, logging, tracing, and caching decorators.
- **Participants**: component interface, concrete component, base decorator, concrete decorators.
- **Avoid when** the wrapper stack becomes hard to understand or ordering is fragile.

#### Facade

- **Use when** a subsystem has many steps or dependencies and callers need a simpler entry point.
- **Example**: a checkout facade coordinates cart validation, tax calculation, payment authorization, inventory reservation, and receipt creation.
- **Participants**: facade, subsystem services, client.
- **Avoid when** it becomes a god object that owns business rules better placed in subsystem services.

#### Flyweight

- **Use when** many similar objects duplicate immutable data and memory pressure matters.
- **Example**: a map renderer shares immutable marker style objects across thousands of map pins.
- **Participants**: flyweight, shared intrinsic state, external extrinsic state, factory or cache, client.
- **Avoid when** memory pressure is not proven or separating shared and external state makes the code confusing.

#### Proxy

- **Use when** access to an object needs control, lazy loading, security checks, caching, or remote communication.
- **Example**: a document proxy loads a large document from storage only when the content is first requested.
- **Participants**: subject interface, real subject, proxy, client.
- **Avoid when** a direct dependency plus explicit service call communicates the behavior more clearly.

### Behavioral patterns

#### Chain of Responsibility

- **Use when** a request should pass through a sequence of handlers until one handles it or all contribute.
- **Example**: an authorization pipeline checks API key, user session, role policy, and account status as separate handlers.
- **Participants**: handler interface, concrete handlers, request, client or pipeline builder.
- **Avoid when** handler order is implicit, hard to test, or critical to correctness but undocumented.

#### Command

- **Use when** an action should be represented as an object for queuing, logging, retries, undo, or authorization.
- **Example**: an admin action queue stores `SuspendUser`, `RestoreUser`, and `ResetPassword` commands with audit metadata.
- **Participants**: command interface, concrete commands, invoker, receiver, optional command bus.
- **Avoid when** a direct function call is enough and no action metadata or lifecycle is needed.

#### Iterator

- **Use when** clients need to traverse a collection without knowing its storage details.
- **Example**: a paginated API iterator yields customer records while hiding page tokens and network calls.
- **Participants**: iterator, aggregate or collection, concrete iterator, client.
- **Avoid when** the native collection traversal is already clear and stable.

#### Mediator

- **Use when** many objects coordinate through complex direct references and need a central interaction policy.
- **Example**: a form mediator updates validation, submit availability, and dependent fields when any field changes.
- **Participants**: mediator, concrete mediator, colleagues, client.
- **Avoid when** the mediator accumulates unrelated business logic or hides simple one-to-one collaboration.

#### Memento

- **Use when** an object's state must be captured and restored without exposing its internals.
- **Example**: an editor stores document snapshots for undo while keeping document internals encapsulated.
- **Participants**: originator, memento, caretaker.
- **Avoid when** snapshots are large, frequent, or better represented as explicit domain events.

#### Observer

- **Use when** one change should notify multiple independent subscribers without coupling the publisher to them.
- **Example**: an order service publishes `OrderPlaced`; email, analytics, and fulfillment subscribers react independently.
- **Participants**: subject or publisher, observers or subscribers, event payload, subscription mechanism.
- **Avoid when** notification ordering, retries, or transactions are critical but not explicitly managed.

#### State

- **Use when** an object changes behavior based on its current state and state-specific rules are growing.
- **Example**: an invoice behaves differently in draft, issued, paid, overdue, and void states.
- **Participants**: context, state interface, concrete states, transitions.
- **Avoid when** there are only two simple states and a conditional is more readable.

#### Strategy

- **Use when** interchangeable algorithms or policies should be selected at runtime or injected for tests.
- **Example**: a shipping calculator chooses ground, express, pickup, or international pricing strategies.
- **Participants**: strategy interface, concrete strategies, context, selection policy.
- **Avoid when** the behavior is unlikely to vary or only differs by a constant value.

#### Template Method

- **Use when** an algorithm has stable steps but subclasses customize specific steps.
- **Example**: an import job defines parse, validate, transform, and persist steps while CSV and JSON imports customize parsing.
- **Participants**: abstract base workflow, template method, primitive or hook methods, concrete subclasses.
- **Avoid when** composition would make variation clearer or inheritance would couple unrelated workflows.

#### Visitor

- **Use when** many operations must be performed across a stable object structure without changing those object classes.
- **Example**: an expression tree supports evaluation, pretty-printing, and validation visitors.
- **Participants**: visitor interface, concrete visitors, element interface, concrete elements, accept operation.
- **Avoid when** new element types are added frequently; updating every visitor becomes costly.

## Quick selection guide

- Need to vary **which object is created**? Start with Factory Method.
- Need compatible **families of objects**? Consider Abstract Factory.
- Need readable or staged **object construction**? Consider Builder.
- Need to reuse configured **templates**? Consider Prototype.
- Need one shared instance and controlled access? Consider Singleton cautiously.
- Need to make one interface look like another? Use Adapter.
- Need abstraction and implementation to vary separately? Use Bridge.
- Need tree-like part-whole behavior? Use Composite.
- Need additive wrapper behavior? Use Decorator.
- Need a simple entry point to a complex subsystem? Use Facade.
- Need to share immutable object data at scale? Use Flyweight.
- Need controlled or lazy access? Use Proxy.
- Need request processing through handlers? Use Chain of Responsibility.
- Need actions as first-class objects? Use Command.
- Need controlled traversal? Use Iterator.
- Need centralized coordination among peers? Use Mediator.
- Need restoreable snapshots? Use Memento.
- Need publish/subscribe notifications? Use Observer.
- Need state-specific behavior? Use State.
- Need interchangeable algorithms? Use Strategy.
- Need fixed algorithm skeleton with variable steps? Use Template Method.
- Need new operations over a stable structure? Use Visitor.

## Pattern application template

When recommending or implementing a pattern, include:

```text
Design force:
Simpler alternatives considered:
Selected pattern:
Participants:
Example extension:
Why this is easier to change or test:
Risks / when to remove:
```

## Anti-patterns

- Applying patterns to look sophisticated.
- Introducing factories, strategies, or observers before variation exists.
- Hiding straightforward logic behind excessive indirection.
- Mixing multiple patterns without clear ownership.
- Turning every pattern participant into a separate file before the codebase needs that structure.
- Preserving a pattern after the variation it supported has disappeared.

## Checklist

- Describe the design force.
- List simpler alternatives.
- Choose the minimal pattern.
- Name participants.
- Add or document one concrete extension example.
- Verify the result is easier to change or test.
- Note when the pattern should be simplified or removed.
