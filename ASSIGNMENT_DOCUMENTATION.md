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

**Your Answer**:

[Your answer here - 4-6 sentences with code examples]

---

### Question 2: Locks vs Semaphores
**Q**: Explain the difference between ReentrantLock and Semaphore. Where did you use each in your code and why?

**Your Answer**:

[Your answer here - explain your implementation choices]

---

### Question 3: Deadlock Prevention
**Q**: What is deadlock? Explain TWO prevention techniques and what you did to prevent deadlocks in your code.

**Your Answer**:

[Your answer here - reference try-finally blocks, lock ordering, etc.]

---

### Question 4: Lock Granularity Design Decision 
**Q**: For Task 1 (protecting the three counters), explain your lock design choice:
- Did you use ONE lock for all three counters (coarse-grained) OR separate locks for each counter (fine-grained)?
- Explain WHY you made this choice
- What are the trade-offs between the two approaches?
- Given that the three counters are independent, which approach provides better concurrency and why?

**Your Answer**:

[Your answer here - explain coarse-grained vs fine-grained locking, independence of counters, concurrency implications. Show understanding of when to use each approach. 5-8 sentences expected.]

---

## Part 3: Synchronization Analysis (1 mark)

### Critical Section #1: Counter Variables

**Which variables**: 

**Why they need protection**: 

**Synchronization mechanism used**: 

**Code snippet**:
```java
// Paste your implementation here
```

**Justification**: 

---

### Critical Section #2: Execution Log

**What resource**: 

**Why it needs protection**: 

**Synchronization mechanism used**: 

**Code snippet**:
```java
// Paste your implementation here
```

**Justification**: 

---

### Critical Section #3: CPU Semaphore

**Purpose of semaphore**: 

**Number of permits and why**: 

**Where implemented**: 

**Code snippet**:
```java
// Paste your implementation here
```

**Effect on program behavior**: 

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
