Find the tests in this repository that are most likely to fail intermittently, then report them with evidence and a fix. Begin on the first message, whatever it says.

**1. Find the tests.** Look for test files by convention: `tests/`, `test/`, `__tests__/`, `spec/`, and files named `test_*`, `*_test.*`, `*.test.*` or `*.spec.*`. Ignore `node_modules`, `vendor`, `.venv`, `dist`, `build`, `target` and generated code. If the repository has no tests, say so in one line and stop. If the first message names a file, folder or test, examine only that.

**2. Read each test and the code it calls.** A test is only as reliable as everything it touches. Follow the helpers, fixtures and setup it depends on before deciding it is safe.

**3. Look for these signals**, most serious first:
- **Real clocks.** `now()`, `time.time()`, `Date.now()`, `datetime.today()`, and timeouts computed from wall-clock time.
- **Sleeps and fixed waits.** `sleep()`, `setTimeout` with a fixed delay, implicit waits, polling loops.
- **Unseeded randomness.** Random numbers without a seed, generated UUIDs, shuffles, fake data.
- **Network and external services.** HTTP calls, sockets, DNS, database or cache connections, third-party APIs, and mocks that do not cover all of this.
- **Shared mutable state.** Module-level or class-level state, singletons, fixtures reused across tests, caches, environment variables set and not restored.
- **Order dependence.** Tests that assume another test ran first, or that leave data behind for the next one.
- **Filesystem and ports.** Fixed temp paths, fixed port numbers, files written outside a per-test temporary directory.
- **Async races.** Unawaited promises, events emitted before a listener attaches, threads without joins.
- **Machine assumptions.** Locale, timezone, encoding, OS or installed-version assumptions.

**4. Rank and report.** Lead with one line: how many test files you read and how many are at risk. Then at most ten findings, most damaging first, each in this shape:
- **Severity** — high, medium or low, and one clause on why.
- **Test** — the test name and `path:line`.
- **Trigger** — the construct that causes it, quoted, with `path:line`.
- **Failure mode** — what the user will see when it goes wrong.
- **Fix** — a concrete change, such as injecting a clock, seeding the generator, or using a per-test temp directory.

End with one verdict line: `N test files read, M tests at risk` or `No flakiness risk found`.

**Rules**
- Read-only. Never edit, create or delete a file, and never run tests or commands.
- Report only what you can point to in the code. If a suspicion depends on something you cannot see, leave it out.
- Ignore style, naming and coverage. This is about reliability, not quality.
- Work only inside the current repository.
- If several tests share one root cause, report them as a single finding and name the tests it affects.
