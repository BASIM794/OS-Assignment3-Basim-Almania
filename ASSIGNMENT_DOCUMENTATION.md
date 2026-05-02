# Assignment 3 - Complete Documentation

**Student Name**: [Basim Saleh Almania]  
**Student ID**: [445050295]  
**Date Submitted**: [2026 May 2]

---

## 🎥 VIDEO DEMONSTRATION LINK (REQUIRED)

> **⚠️ IMPORTANT: This section is REQUIRED for grading!**
> 
> Upload your 3-5 minute video to your **PERSONAL Gmail Google Drive** (NOT university email).
> Set sharing to "Anyone with the link can view".
> Test the link in incognito/private mode before submitting.

**Video Link**: [Paste your personal Gmail Google Drive link here]

**Video filename**: `[YourStudentID]_Assignment3_Synchronization.mp4`

**Verification**:
- [ ] Link is accessible (tested in incognito mode)
- [ ] Video is 3-5 minutes long
- [ ] Video shows code walkthrough and commits
- [ ] Video has clear audio
- [ ] Uploaded to PERSONAL Gmail (not @std.psau.edu.sa)

---

## Part 1: Development Log (1 mark)

Document your development process with **minimum 3 entries** showing progression:

### Entry 1 - [MAY 2, 2026 (6:00 PM)]
**What I implemented**: After examining the original code, I discovered shared resources that are accessible by several threads, like counters and execution logs.

**Challenges encountered**: It was difficult to understand where racial circumstances exist in the software.
**How I solved it**: I looked over every common variable and examined how it is used by several threads.

**Testing approach**: I saw inconsistent results when I ran the application several times.
**Time spent**: 45 min

---

### Entry 2 - [MAY 2, 2026 (6:45 PM)]
**What I implemented**: To safeguard shared counters (contextSwitchCount, completedProcessCount, totalWaitingTime), I introduced ReentrantLock.

**Challenges encountered**: ensuring that locks are released correctly.

**How I solved it**: To ensure unlocking, I employed try-finally blocks.

**Testing approach**: To guarantee consistency, the software was tested using many threads.

**Time spent**: 30 min

---

### Entry 3 - [MAY 2, 2026 (7:15 PM)]
**What I implemented**: To avoid concurrent modification problems, I implemented a separate lock for the execution log.

**Challenges encountered**: comprehending ArrayList's thread safety.

**How I solved it**: For logging operations, a special lock called logLock was used.
**Testing approach**: looked for exceptions such as ConcurrentModificationException.

**Time spent**: 45 min

---

### Entry 4 -[MAY 2, 2026 (8:00 PM)]
**What I implemented**: To manage CPU access, I put in place a semaphore (1 permit).
**Challenges encountered**: accurately positioning acquire and release.

**How I solved it**: used acquire prior to execution and release in the final block.

**Testing approach**: noted that only one process is active at a time.

**Time spent**: 1 hour

---

### Entry 5 - [MAY 2, 2026 (9:00 PM)]
**What I implemented**: Debugging and final testing.

**Challenges encountered**: ensuring that there are no longer any race situations or deadlocks.

**How I solved it**: confirmed that every important area is secure.

**Testing approach**: ran the program several times and verified the consistency of the results.

**Time spent**: 1 hour

---

## Part 2: Technical Questions (1 mark)

### Question 1: Race Conditions
**Q**: Identify and explain TWO race conditions in the original code. For each:
- What shared resource is affected?
- Why is concurrent access a problem?
- What incorrect behavior could occur?

**Your Answer**:When many threads simultaneously increase the value of shared counters like contextSwitchCount, the first race situation takes place. Because the increment procedure is not atomic, this results in inaccurate counts.
When several threads try to add items simultaneously in the executionLog, the second race condition takes place. This may result in incorrect data or runtime problems because ArrayList is not thread-safe.
Because threads may overwrite each other's updates, concurrent access is challenging. Inaccurate statistics, such as an incorrect total waiting time or missing log entries, may result from this.

[Your answer here - 4-6 sentences with code examples]

---

### Question 2: Locks vs Semaphores
**Q**: Explain the difference between ReentrantLock and Semaphore. Where did you use each in your code and why?

**Your Answer**:Only one thread can access a crucial portion at a time thanks to reentrant lock, which ensures mutual exclusion. Conversely, a semaphore restricts access by permitting a certain number of threads.
ReentrantLock was utilized in my implementation to safeguard the execution log and shared counters. I simulated a single CPU by controlling CPU access with a semaphore, which only permits one task to run at a time.

[Your answer here - explain your implementation choices]

---

### Question 3: Deadlock Prevention
**Q**: What is deadlock? Explain TWO prevention techniques and what you did to prevent deadlocks in your code.

**Your Answer**:When threads wait endlessly for resources owned by one another, this is known as a deadlock.
Using try-finally blocks to guarantee that locks are always released is one preventative strategy. Keeping a constant locking sequence is another strategy.
To avoid deadlocks, I utilized try-finally blocks for all locks and semaphore actions in my code.

[Your answer here - reference try-finally blocks, lock ordering, etc.]

---

### Question 4: Lock Granularity Design Decision 
**Q**: For Task 1 (protecting the three counters), explain your lock design choice:
- Did you use ONE lock for all three counters (coarse-grained) OR separate locks for each counter (fine-grained)?
- Explain WHY you made this choice
- What are the trade-offs between the two approaches?
- Given that the three counters are independent, which approach provides better concurrency and why?

**Your Answer**:Because counters and logs are independent, fine-grained locking offers better concurrency and efficiency than coarse-grained locking, which would use a single lock for all resources. I used fine-grained locking by separating locks into counterLock and logLock, which improves performance because threads can update counters and logs independently.

[Your answer here - explain coarse-grained vs fine-grained locking, independence of counters, concurrency implications. Show understanding of when to use each approach. 5-8 sentences expected.]

---

## Part 3: Synchronization Analysis (1 mark)

### Critical Section #1: Counter Variables

**Which variables**: contextSwitchCount, completedProcessCount, totalWaitingTime

**Why they need protection**: They are updated simultaneously and shared by several threads.

**Synchronization mechanism used**: ReentrantLock (counterLock)

**Code snippet**:counterLock.lock();
try {
    contextSwitchCount++;
} finally {
    counterLock.unlock();
}
```java
// Paste your implementation here
```

**Justification**: avoids race situations and guarantees atomic updates.

---

### Critical Section #2: Execution Log

**What resource**: executionLog (ArrayList)

**Why it needs protection**: ArrayList is not thread-safe.

**Synchronization mechanism used**: ReentrantLock (logLock)

**Code snippet**:logLock.lock();
try {
    executionLog.add(message);
} finally {
    logLock.unlock();
}
```java
// Paste your implementation here
```

**Justification**: protects data integrity and stops concurrent alteration.

---

### Critical Section #3: CPU Semaphore

**Purpose of semaphore**: Limit CPU access

**Number of permits and why**: 1 permit to simulate a single CPU

**Where implemented**: In run() method before execution

**Code snippet**:cpuSemaphore.acquire();
try {
    // process execution
} finally {
    cpuSemaphore.release();
}
```java
// Paste your implementation here
```

**Effect on program behavior**: guarantees that a single process runs at a time.

---

## Part 4: Testing and Verification (2 marks)

### Test 1: Consistency Check
**What I tested**: Running program multiple times to verify consistent results

**Testing procedure**: 
```bash
# Commands used (run the program at least 5 times)
```

**Results**: 
(Show that running multiple times produces consistent, correct results)

**Why synchronization is necessary**: 
(Explain what race conditions COULD occur without synchronization, even if you didn't observe them. Explain which shared resources need protection and why.)

**Conclusion**: 

---

### Test 2: Exception Testing
**What I tested**: Checking for ConcurrentModificationException

**Testing procedure**: 

**Results**: 

**What this proves**: 

---

### Test 3: Correctness Verification
**What I tested**: Verifying correct final values (total burst time, context switches, etc.)

**Expected values**: 

**Actual values**: 

**Analysis**: 

---

### Test 4: Different Scenarios
**Scenario tested**: [e.g., different time quantum, more processes, etc.]

**Purpose**: 

**Results**: 

**What I learned**: 

---

## Part 5: Reflection and Learning

### What I learned about synchronization:

[6-8 sentences about key concepts, challenges, insights]

---

### Real-world applications:

Give TWO examples where synchronization is critical:

**Example 1**: 

**Example 2**: 

---

### How I would explain synchronization to others:

[Explain to someone who just finished Assignment 1 - use simple terms and analogies]

---

## Part 6: GitHub Repository Information

**Repository URL**: 

**Number of commits**: 

**Commit messages**: 
1. 
2. 
3. 
4. 

---

## Summary

**Total time spent on assignment**: 

**Key takeaways**: 
1. 
2. 
3. 

**Most challenging aspect**: 

**What I'm most proud of**: 

---

**End of Documentation**
