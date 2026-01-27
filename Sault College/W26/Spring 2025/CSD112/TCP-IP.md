{MISSING EXPLANATION ABOUT TCP IP}

---

The [[OSI Model]] has **seven layers**. But real networks use TCP/IP with fewer layers:
- **Application** (combines OSI layers 5, 6, 7)
- **Transport** (Layer 4)
- **Internet**(Layer 3)
- Network Access (Layer 1)

## TCP vs UDP - Two Ways to Send Data

### **TCP** is like a careful librarian:
- Checks if you received everything
- Resends missing pieces
- Makes sure everything arrives in order
- Slow but reliable

### **UDP** is like shouting across a crowded room:
- Just throws data and hopes it arrives
- No checking, no resending
- Fast but unreliable
- Good for video games and live streams