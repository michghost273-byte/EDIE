# Improvement status — EDIE 31.47.0

This tracker maps the previous 100 suggestions to the delivered package.
The full roadmap is not complete: **23 complete, 36 partial,
41 planned**. Complete refers to the code change and available automated
checks; live Windows audio and target-device behaviour remain unverified.
Partial rows describe the precise included work and the outstanding part.
Planned rows may retain existing support from the uploaded application but do
not claim a new implementation in this release.

| # | Improvement | Status | Delivered work and remaining scope |
|---|---|---|---|
| 1 | Recover from malformed performance settings | Complete | EDIE46Performance validates nested modes; malformed JSON shapes recover to defaults. |
| 2 | Prevent concurrent settings-save collisions | Complete | Unique temporary files, per-path thread/process locks, atomic replacement and locked updates; thread/process regression tests. |
| 3 | Report failed health checks accurately | Complete | Shared outcome classification handles unhealthy nested checks and unknown non-success health states. |
| 4 | Cancel automation under its original profile | Complete | Owner-scoped state updates and a profile-operation lease; cancellation after profile changes is tested. |
| 5 | Speak only the current request's answer | Complete | Voice reply polling uses a new-message boundary, profile and turn identity. |
| 6 | Split the application into cohesive modules | Partial | New persistence, audio, speech, configuration, UI dispatch, backup, retrieval and launch modules; the historical UI remains a compatibility source. |
| 7 | Replace accumulated startup/shutdown overrides | Partial | New services have one lifecycle owner; historical init layers remain for compatibility. |
| 8 | Move embedded artwork into packaged resources | Complete | Brain PNG moved out of the source and packaged as a resource. |
| 9 | Unify release identity and packaged filenames | Partial | Stable launcher, current desktop title, About and version output are consistent. Historical subsystem titles still exist. |
| 10 | Validate settings schemas and migrations | Partial | Voice settings have typed ranges; JSON container/performance recovery is implemented. Older settings need further schema work. |
| 11 | Recover from broken optional configuration | Partial | Preflight and capture-safe recovery strengthened. A comprehensive broken-integration recovery UI remains future work. |
| 12 | Route worker UI callbacks through one queue | Partial | Worker root.after scheduling is queued to the owning Tk thread. Direct legacy widget access still needs a wider audit. |
| 13 | Move lengthy operations off the UI thread | Partial | New model preparation, backup and health actions run off-thread; legacy operations remain to be profiled. |
| 14 | Batch streamed rendering and bound event draining | Complete | Chat draining has a time/count budget and coalesces tokens into fewer widget updates. |
| 15 | Surface actionable exceptions | Partial | New private rotating UI error logs; the inherited broad exception handlers still need review. |
| 16 | Continue audio capture during transcription | Complete | Recorder thread continues producing while the inference consumer transcribes. |
| 17 | Bound audio buffering and report dropped frames | Complete | Queue size is bounded, old frames are dropped with a visible status and counters. |
| 18 | Preserve speech pre-roll | Complete | Configurable pre-roll with deterministic segmentation tests. |
| 19 | Strengthen noisy-environment speech detection | Partial | Adaptive energy gate improved; neural VAD and real-room evaluation remain future work. |
| 20 | Configure pauses and maximum utterance length | Complete | Per-profile silence, pre-roll and utterance duration preferences. |
| 21 | Expose transcription language selection | Complete | Explicit Whisper language with multilingual models exposed in the session picker. |
| 22 | Improve microphone/playback device selection | Partial | Per-profile device name/ID selection is implemented. Automatic enumeration/reconnection needs further work. |
| 23 | Reconnect devices after hotplug | Planned | Existing support is retained; the additional improvement is not implemented in this release. |
| 24 | Negotiate sample rates and resampling | Planned | Existing support is retained; the additional improvement is not implemented in this release. |
| 25 | Select speech processing for available hardware | Partial | Explicit CPU/CUDA preference with a CPU fallback; automatic hardware benchmarking remains future work. |
| 26 | Stop workers after parent exit or pipe closure | Complete | Parent watcher plus EOF shutdown for all three new worker entry points. |
| 27 | Version and validate worker messages | Partial | Version, timestamps, message bounds, readiness and capture heartbeat added. A unified utterance-ID protocol remains future work. |
| 28 | Interrupt speech without blocking the UI | Complete | SAPI cancel control stays responsive while speech runs; microphone process cleanup is asynchronous. |
| 29 | Bound speech queues and discard stale generations | Partial | SAPI queue bounds and generation checks prevent stale completion events. Piper retains its inherited separate queue. |
| 30 | Preserve long answers through sentence chunks | Complete | Sentence/word-aware bounded chunks replace long-request truncation. Queue saturation is reported. |
| 31 | Coordinate wake, conversation and speech services | Partial | Wake listening pauses for a Whisper microphone owner; historical alternate capture interfaces remain. |
| 32 | Apply provider voice/rate/volume preferences consistently | Partial | SAPI rate/volume/voice preferences are implemented. Piper provider controls remain separate. |
| 33 | Provide a consistent push-to-talk shortcut | Planned | Existing support is retained; the additional improvement is not implemented in this release. |
| 34 | Prepare models before offline listening | Complete | Whisper is cache-only during capture; explicit preparation controls download models. |
| 35 | Preserve typed drafts during voice requests | Complete | Wake requests use the normal transcript dispatcher and preserve the typed composer. |
| 36 | Verify model capabilities through the API | Planned | Existing support is retained; the additional improvement is not implemented in this release. |
| 37 | Budget prompt context in tokens | Planned | Existing support is retained; the additional improvement is not implemented in this release. |
| 38 | Improve editable long-conversation summaries | Planned | Existing support is retained; the additional improvement is not implemented in this release. |
| 39 | Measure response timing and generation performance | Partial | Bounded samples of first-displayed-chunk and total response timings; token throughput and percentiles remain future work. |
| 40 | Propagate cancellation through active processing | Planned | Existing support is retained; the additional improvement is not implemented in this release. |
| 41 | Distinguish tool success from factual verification | Partial | Unhealthy jobs report partial; receipts no longer claim that every conclusion is factually verified. |
| 42 | Reference exact retrieved source passages | Planned | Existing support is retained; the additional improvement is not implemented in this release. |
| 43 | Keep retrieved instructions untrusted | Planned | Existing support is retained; the additional improvement is not implemented in this release. |
| 44 | Validate plans and tool arguments with schemas | Planned | Existing support is retained; the additional improvement is not implemented in this release. |
| 45 | Provide actionable model/setup failure messages | Partial | Missing cached speech models, offline Ollama and launcher failures have clearer next actions. |
| 46 | Cache model inventory and recover after restart | Planned | Existing support is retained; the additional improvement is not implemented in this release. |
| 47 | Benchmark models on repeatable user tasks | Planned | Existing support is retained; the additional improvement is not implemented in this release. |
| 48 | Index large archives with full-text search | Complete | FTS5 with update/delete triggers and a bounded fallback; profile-scoped tests. |
| 49 | Unify the memory interfaces | Planned | Existing support is retained; the additional improvement is not implemented in this release. |
| 50 | Track embedding identity and version | Partial | Model name and vector dimensions are recorded; unknown/incompatible vectors are excluded. Model digest/revision tracking remains future work. |
| 51 | Chunk along meaningful boundaries with references | Partial | Overlapping paragraph/word-boundary character chunks include offsets. Token-aware/page-aware chunking remains future work. |
| 52 | Read indexing preferences once per operation | Complete | Preferences are loaded once in the document indexing operation. |
| 53 | Re-index changed content incrementally | Partial | Unchanged source content preserves chunks/embeddings. Cross-file stale-source reconciliation remains future work. |
| 54 | Review duplicate and conflicting memories | Planned | Existing support is retained; the additional improvement is not implemented in this release. |
| 55 | Separate relevance, importance and confidence | Planned | Existing support is retained; the additional improvement is not implemented in this release. |
| 56 | Expose memories used by an answer | Planned | Existing support is retained; the additional improvement is not implemented in this release. |
| 57 | Correct/delete data across memory stores | Planned | Existing support is retained; the additional improvement is not implemented in this release. |
| 58 | Include new settings and report backup omissions | Partial | New full backups include declarative data/current settings and report omissions. Older inherited backup formats remain separate. |
| 59 | Rehearse restoration before recovery claims | Partial | Checksums, SQLite integrity and staged recovery are tested. Restore certification against real Windows user data remains pending. |
| 60 | Unify task and mission states | Planned | Existing support is retained; the additional improvement is not implemented in this release. |
| 61 | Bind background operations to a fixed profile | Partial | New automation freezes the owner and blocks UI profile changes while active. Broader legacy worker ownership remains to be audited. |
| 62 | Bind approvals to exact action content | Planned | Existing support is retained; the additional improvement is not implemented in this release. |
| 63 | Extend replay protection and durable receipts | Planned | Existing support is retained; the additional improvement is not implemented in this release. |
| 64 | Cancel active mission model/I/O calls | Planned | Existing support is retained; the additional improvement is not implemented in this release. |
| 65 | Handle reminder time zones and daylight-saving changes | Planned | Existing support is retained; the additional improvement is not implemented in this release. |
| 66 | Extract structured task dates and priorities | Planned | Existing support is retained; the additional improvement is not implemented in this release. |
| 67 | Distinguish prepared/approved/executed/verified states | Planned | Existing support is retained; the additional improvement is not implemented in this release. |
| 68 | Limit retries and resume failed work correctly | Planned | Existing support is retained; the additional improvement is not implemented in this release. |
| 69 | Explain dependencies and blocked steps | Planned | Existing support is retained; the additional improvement is not implemented in this release. |
| 70 | Simplify primary navigation | Partial | Compact native menu provides primary routes. The older dashboard/navigation layout is retained. |
| 71 | Improve command search and everyday terminology | Planned | Existing support is retained; the additional improvement is not implemented in this release. |
| 72 | Unify favourite/recent actions | Planned | Existing support is retained; the additional improvement is not implemented in this release. |
| 73 | Standardise typography, spacing and labels | Planned | Existing support is retained; the additional improvement is not implemented in this release. |
| 74 | Distinguish available/configured/running/setup states | Partial | New Health output distinguishes local reachability and installed optional packages. Older capability catalogue labels remain. |
| 75 | Coordinate status messages | Planned | Existing support is retained; the additional improvement is not implemented in this release. |
| 76 | Restore geometry and adapt to smaller displays | Partial | New controls include scrolling and a smaller minimum size. Global multi-monitor restoration remains future work. |
| 77 | Improve keyboard and screen-reader access | Planned | Existing support is retained; the additional improvement is not implemented in this release. |
| 78 | Apply reduced motion throughout | Planned | Existing support is retained; the additional improvement is not implemented in this release. |
| 79 | Recover unsent drafts and attachment selections | Partial | Unsent text is saved/recovered without automatic sending. Attachment restoration remains future work. |
| 80 | Group routine notifications | Planned | Existing support is retained; the additional improvement is not implemented in this release. |
| 81 | Standardise previews, diffs and recovery | Planned | Existing support is retained; the additional improvement is not implemented in this release. |
| 82 | Make capture pause govern the capture pipelines | Partial | Capture pause and safe-mode guards cover modern microphone, loopback and observation routes; older capture adapters need wider verification. |
| 83 | Offer selected-window capture and exclusions | Planned | Existing support is retained; the additional improvement is not implemented in this release. |
| 84 | Avoid analysing unchanged screenshots | Planned | Existing support is retained; the additional improvement is not implemented in this release. |
| 85 | Keep credentials in secure storage and redact logs | Planned | Existing support is retained; the additional improvement is not implemented in this release. |
| 86 | Recheck voice permissions during a conversation | Partial | Wake listening checks permission inside capture and before dispatch; active Whisper polling stops when capture permission is revoked. |
| 87 | Consolidate URL/redirect/address validation | Planned | Existing support is retained; the additional improvement is not implemented in this release. |
| 88 | Unify archive extraction limits and checksums | Partial | New full backups and the model installer reject unsafe paths, links and excessive expansion. Older archive handlers remain. |
| 89 | Separate generated proposals from installed trusted code | Planned | Existing support is retained; the additional improvement is not implemented in this release. |
| 90 | Share the configured Python across launcher and installer | Complete | All three Windows scripts delegate to the same stable launcher and interpreter selection. |
| 91 | Preflight supported Python and components | Planned | Existing support is retained; the additional improvement is not implemented in this release. |
| 92 | Make optional dependencies reproducible | Partial | Optional wake dependency versions are pinned. Complete platform-specific transitive hash locks remain future work. |
| 93 | Verify downloaded speech models before installation | Complete | Official Vosk archive SHA-256 pinned and verified; extraction quotas and rollback preserve existing models. |
| 94 | Resolve the data directory consistently | Complete | One resolver for stable launch/install/open-data, nested override directories supported, worker environment includes the selected data path. |
| 95 | Provide tested signed/portable Windows distributions | Partial | Portable source ZIP produced. A signed installer requires a Windows build and signing credentials and is not supplied. |
| 96 | Add Windows launch and CI checks | Partial | Windows/Linux, Python 3.11/3.13 workflow supplied; no remote GitHub CI run or Windows launch was performed here. |
| 97 | Replace brittle source-position/version tests | Partial | Startup graph validation replaces physical line ordering and metadata rewriting; most historical release-version wrappers remain. |
| 98 | Cover the five reproduced bugs with regressions | Complete | All five reproduced defects have regression coverage. |
| 99 | Test failures, long operation and sleep/resume | Partial | Corrupt settings, concurrent writers, bounded buffering, cancellation, unsafe archives and staged recovery covered; real sleep/hotplug/soak/disk-full testing remains. |
| 100 | Label capabilities by actual verification scope | Planned | New health/validation documentation states verification scope. The inherited full capability catalogue still needs relabelling. |
