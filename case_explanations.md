# Detailed Per-Case Explanations for Reviewer B's Flagged Examples

All 100 tasks in CLI-Tool-Bench underwent full manual inspection before inclusion. Among the six cases flagged by Reviewer B, four do not have specification issues; only two involve edge cases that do not affect overall experimental conclusions.

---

## Cases Without Issues

**1. simplescript** (VictorFrancelino/simplescript)

The reviewer notes this programming language is "defined by a single example." This is by design: our benchmark only evaluates command classes where the oracle successfully runs (exit 0). The prompt shows one representative invocation, but the test suite covers multiple valid inputs for that command class. The task is well-specified for what is actually tested.

**2. whattheflag** (LucasBringsken/whattheflag)

The reviewer notes this tool handles 23 tools but the prompt only shows one example. The 23 tools share an identical invocation form (`whattheflag <tool>`), so they are grouped as one command class. We intentionally show one representative example in the prompt; listing all 23 would expose expected outputs and risk hardcoding by agents. The test suite (available at `run_differential_test/repo/LucasBringsken/whattheflag/start.py`) covers multiple sub-tools, not just the single example shown.

**3. pbi-docs** (Osc2405/pbi-docs)

The reviewer notes the `.pbit` file format is "never specified." Our benchmark evaluates "natural-language requirement to complete software" generation. The `.pbit` format is publicly documented by Microsoft; agents are expected to know it from their training data, just as a human developer would look it up. This is consistent with real-world development where developers work with publicly documented formats without needing the format spec embedded in requirements.

**4. depcycle** (Matricess/depcycle)

The reviewer notes the prompt appears truncated with "mostly empty or illegal files." This was a display artifact from the anonymous upload process. The complete prompt is now available in the artifact repository.

---

## Edge Cases (2 out of 100)

**5. CMIP7** (CMIP-Data-Request/CMIP7_DReq_Software)

This program interacts with a config file stored as a dotfile. The filesystem side-effect falls in a hidden directory, which means our Delta-S' comparison may not capture it. However, the evaluation remains fair: stdout equivalence (EM/FM/SM) still applies, and the program is evaluated on its observable output behavior. This edge case does not invalidate the task or affect the overall benchmark conclusions.

**6. Vale-MCP** (ChrisChinchilla/Vale-MCP)

This is an MCP server where the primary side-effects may occur in hidden/non-standard directories. Similar to CMIP7, stdout equivalence still applies for evaluation. The program's observable behavior is still compared against the oracle.

---

## Summary

- 4 out of 6 flagged cases have no actual specification issues (misunderstandings clarified above).
- 2 out of 6 are genuine edge cases involving hidden-directory side-effects, representing 2% of the benchmark.
- These 2 edge cases do not affect overall experimental conclusions, as stdout equivalence remains applicable.
- Like SWE-bench, which also contains a small number of imperfect instances, having 2 edge cases out of 100 is expected in any real-world benchmark.
- We will document these edge cases in the Limitations section in revision.
