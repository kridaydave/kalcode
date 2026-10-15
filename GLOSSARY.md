# Glossary

Vocabulary for kalcode. Implementation details live in the spec, not here.

## Backends

**Backend**: an agent process kalcode can spawn and talk to over ACP. A backend is the whole
process (its CLI, its session state, its login), not a model. One backend can serve many threads.

**Backend family**: two backends built on the same upstream agent, for example two CLIs from the
same project. They share quotas, so they are one budget wearing two names.

**Headroom**: how much a backend can still do before its free limit bites.

**Drained**: a backend with no headroom left. Drained is not the same as broken: a drained backend
works fine, it just says no.

## Work

**Thread**: the durable record of one piece of work. A thread outlives any single backend session
and is owned by kalcode, not by a backend.

**Orchestrator**: the one backend that owns a thread and decides what work leaves the thread.

**Subagent**: a backend session spawned to do delegated work inside a thread.

**Delegation**: sending work from a thread's orchestrator out to a subagent and taking the result
back. One delegation is one subagent session and one unit of that backend's headroom.

## Still unsettled

Thread, session, turn and run still overlap, and the boundaries between them are being decided in
"Thread and session model across agents that resume differently". Do not define them here before
that ticket closes.

## Wayfinding

**Map**: the single issue holding this effort's destination, the decisions made, and the fog ahead.

**Ticket**: a child issue of the map holding one decision. Sizing: one agent session.

**Frontier**: the open, unblocked, unclaimed tickets. The edge of what is known.