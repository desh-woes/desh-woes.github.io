---
title: Blind Signing: The Digital Equivalent of Carbon Paper
published: true
---

I’ve recently gone down a rabbit hole with a concept called `Blind Signing`, and like every new thing I learn, it’s too elegant not to share.

At a technical level, it’s a tool for generating anonymous tokens for authentication. But the real magic is how it creates trust while keeping secrets (the `secret` here being your identity).

### The Layman's Explanation (Chaum’s analogy) 

Say you want to participate anonymously in an election and you have a trusted authority i.e an election officer that actually officiates and authorizes a vote. Here is the problem: You need the officer to validate your ballot so it counts, but if you show them who you voted for, it’s no longer anonymous. If you don't show them, how do they know you are authorized to vote?

You are determined to vote as a good citizen, so you go ahead and write your vote on a slip of paper. This paper needs to be officially signed by a trusted election official so before handing your paper slip to the officer, you put that slip inside an envelope lined with carbon paper inside. 

> “Carbon paper is a thin, ink-coated sheet that uses the pressure of a pen to transfer writing onto the page beneath it.”

You seal this envelope and hand it to the officer. The officer checks your ID to ensure you are allowed to vote and then they sign the ***outside*** of the envelope. 
Because of the carbon paper, their signature is transferred through the envelope directly onto your voting slip inside. You can now take the slip out and cast your vote. The tally counters will know it’s legitimate because it has the officer’s signature, but the officer has no idea who you voted for.

### How it works digitally

In the digital world, we replace the envelope with a "blinding factor" (e.g a random number or nonce). Here is the flow:

```
YOU (The Voter)                        SERVER (The Official)
    ===============                        =====================

+----------------+
| Your Data (D)  |
+----------------+
       |
       | (1) BLIND:
       | Multiply by Random Number (R)
       v
+----------------+
|  Blinded Data  |
|    (D * R)     |
+----------------+
       |
       +------------ SEND ------------> +----------------+
                                        |  Blinded Data  |
                                        +----------------+
                                                |
                                                | (2) SIGN:
                                                | Apply Private Key
                                                v
                                        +----------------+
        <---------- RETURN ------------ | Signed Blinded |
        |                               |     Data       |
        |                               +----------------+
        v
+----------------+
| Signed Blinded |
|     Data       |
+----------------+
       |
       | (3) UNBLIND:
       | Divide by Random Number (R)
       v
+==================+
| SIGNED DATA (D)! |  <-- Final Result: Only you see this.
+==================+      The server never saw 'D'.
```

1. Blind: You take your data (the vote) and multiply it by this random number to "blind" it.

2. Sign: You send this jumbled mess to the server. The server signs it and sends it back.

3. Unblind: You use math to remove the random number.

The result? You are left with your original data signed by the server, but the server has no idea what it just signed. It’s the perfect way to prove you have permission to do something without revealing who you are.
