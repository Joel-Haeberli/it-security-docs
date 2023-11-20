tags: #distributedsystems
# Two Generals Problem

links: [[002 Terms|Terms]] - [[themes/000 Index|Index]]

---

> Two Generals’ Problem is a classic computer science problem that remains unsolvable.
> It comes up whenever we talk about communication over an unreliable channel.
> The main problem is an inconsistent state caused by lack of common knowledge

In computing, the Two Generals' Problem ("Two Generals' Paradox" or the "Byzantine Generals Problem") is a thought experiment meant to illustrate the pitfalls and design challenges of attempting to coordinate an action by communicating over an unreliable link.
In the experiment, two generals are only able to communicate with one another by sending a messenger through enemy territory. The experiment asks how they might reach an agreement on the time to launch an attack, while knowing that any messenger they send could be captured.

The key issue in the Two Generals Problem is how the generals can reach a consensus despite the uncertainty and potential for communication failures. No matter how many times the generals exchange messages, there is always a risk that a message may be lost, delayed, or compromised, leading to a lack of agreement on the attack plan.

This problem is important in the field of distributed computing because it highlights the fundamental challenges of achieving consensus in a network where communication is not entirely reliable.

## TCP

As we probably know, TCP uses a mechanism called 4-way handshake to terminate the connection. In this mechanism, a system that wants to terminate a connection sends a FIN message. The system on the other side of the communication channel replies with an ACK and sends its own FIN message which is followed by another ACK from the system which initialised termination. When all of those messages are received correctly, both sides know that the connection is terminated. So far it looks ok, but the problem here is again the shared knowledge between the two systems. When, for example, the second FIN is lost we end up with a half-open connection where one side is not aware that the connection has been closed. That’s why even though TCP is very reliable protocol it doesn’t solve the Two Generals’ Problem. [^1]

[^1]: https://finematics.com/two-generals-problem/

---
links: [[002 Terms|Terms]] - [[themes/000 Index|Index]]