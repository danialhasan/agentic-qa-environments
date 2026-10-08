# Evidence and measurement

Read this when auditing a run, delivering a recording, or comparing runtimes. Set acceptance thresholds before the measured run when a threshold is part of the request.

## Acceptance across boundaries

Connect each assertion to the same run, fixture, revision, and runtime. For a save-and-reopen journey, retain the visible saved value, a fresh API read after navigation, and an independent database observation of the exact value. Check the baseline as well as the transition so old records cannot satisfy the test. A database observer must not repair or synthesize the write it verifies.

Fault injection tests the verifier as well as the application. For example, an isolated adapter can acknowledge a write without persisting it. The database check should detect the missing transition even if the UI displays success. Restore the normal path, retry the same fixture, and preserve both outcomes. Never label the injected fault as an observed production defect.

For concurrency, record overlapping intervals and fixture isolation. Test shared-row conflicts separately from independent users saving different records. For recovery, correlate the interrupted runtime, replacement runtime, data continuity, and any healthy peer observations. Overlapping agent activity is not evidence of continuous simultaneous model computation.

## Recording and cadence

Keep the source capture and an annotated export separate. Preserve original timestamps, capture settings, resolution, viewport, codec, clock basis, and any inserted hold frames. Inspect the requested states in chronological order, including transitions that are blank or loading. Do not replace those frames without disclosing the edit.

Separate these quantities:

| Quantity | Evidence it requires |
| --- | --- |
| Encoded frame rate | Stream metadata and time base; this describes the file |
| Capture delivery cadence | Received frame timestamps, frame count, elapsed interval and gaps |
| Renderer callback cadence | Instrumented callback timestamps during the same interval |
| Capture coverage | Known emitted identifiers matched to decoded captured frames |
| Application visual changes | Changes within the application region, excluding instrumentation |

Use `(frame_count - 1) / (last_timestamp - first_timestamp)` for a simple mean arrival cadence when at least two distinct timestamps exist. Report units, interval, median/p95 inter-frame gaps and the largest gap as well as the mean. Timing clocks may have different origins; correlate them with measured brackets and state uncertainty rather than subtracting unrelated timestamps.

A callback counter is a disclosed probe, not the application. A captured counter cannot prove the app repainted, and an unchanged app region is not necessarily a dropped frame. Decode all frames needed for a coverage claim, match probe IDs, and separately inspect or hash application pixels. Keep any missing IDs and trace buffer loss visible. Bound recording duration and output size, reserve disk, and sample recorder overhead when assessing performance.

[FFprobe](https://ffmpeg.org/ffprobe.html) can inspect stream and per-frame fields. An encoded file reporting 60 fps may contain duplicates or resampled timestamps. It cannot by itself establish 60 unique captures per second, renderer cadence, or smooth application behavior. A short readable demo can pass its visual objective while a separate cadence requirement fails.

## Local and cloud comparisons

Match the application revision, scenario data, assertion protocol, dependency versions, viewport, browser, warmups and measured iterations where feasible. Report unavoidable differences in architecture, service topology, emulation, background load and hardware limits. Keep setup, login, warmups, measurement and cleanup timings separate.

Retain raw timing samples and state the percentile method. Do not generalize from one workload or compare cold installation with warm startup. A cloud label alone does not identify where the browser, database, application, controller, and recorder ran.

For resource measurements, identify sampled process trees and containers, sampling intervals, CPU units, memory measure, lifecycle boundaries and missing samples. Attach observation before launching or releasing replacement processes if restart coverage is required. Sampled maxima are not true peaks; summed RSS can double-count shared pages and short-lived children can escape sampling. Do not add totals from overlapping scopes. Missing cost or scheduler telemetry remains unknown.

## Artifact handling

Use a manifest with relative paths, byte counts, cryptographic hashes, source identity, and the assertion each artifact supports. Verify hashes after transfer, then decode or open the delivered artifact. A link or upload response alone does not prove that the recipient can read a useful result.

Keep secrets out of evidence at collection time when possible. Before sharing, inspect archives recursively and review authentication responses, network bodies and headers, URLs, console logs, browser storage, traces, screenshots and filenames. Password-only filtering misses tokens and cookies. Use an allowlisted sanitized representation where practical and hash it separately from restricted originals.

If redaction removes a necessary payload or trace event, mark the affected claim limited or unverified. A scan with no matches is bounded evidence, not a guarantee of privacy. Re-audit changed files and any reachable commit history before publishing a reusable package.

The final receipt should distinguish functional outcome, negative controls, recovery, capture, resources, provider execution, cleanup and human review. An incomplete layer does not erase a valid narrower result, but it prevents claiming the broader acceptance target.
