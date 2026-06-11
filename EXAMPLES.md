# Karpathy Guidelines — Examples

Reference patterns for the four principles. Adapted from [andrej-karpathy-skills](https://github.com/forrestchang/andrej-karpathy-skills).

---

## 1. Think Before Coding

### Hidden Assumptions

**User Request:** "Add a feature to export user data"

**Bad Response (Makes Assumptions Silent)**

```python
def export_users(format='json'):
    """Export all users to a file."""
    users = User.query.all()
    
    if format == 'json':
        with open('users.json', 'w') as f:
            json.dump([u.to_dict() for u in users], f)
    elif format == 'csv':
        # ... assumes all fields, file paths, etc.
```

**Problems:**
- Assumes exporting ALL users (privacy implications?)
- Assumes file location without asking
- Assumes which fields to include
- Assumes CSV structure

**Good Response (Surfaces Assumptions Explicitly)**

```
Before implementing, I need to clarify:

1. **Scope**: Export all users or filtered subset? (privacy implications)
2. **Format**: API endpoint, download file, or background job?
3. **Fields**: Which user fields? (some might be sensitive)
4. **Volume**: How many users? (affects approach)

Simplest approach: Add an API endpoint that returns paginated JSON.
Would need more info for file-based exports.

What's your preference?
```

### Multiple Interpretations

**User Request:** "Make the search faster"

**Bad:** Jumps to caching, indexes, and async without clarifying what "faster" means.

**Good:**

```
"Make the search faster" could mean:

1. **Faster response time** (< 100ms instead of 500ms)
   - Add database indexes, cache frequent queries
   - Estimated effort: 2 hours

2. **Handle more concurrent searches** (throughput)
   - Add async/await, connection pooling
   - Estimated effort: 4 hours

3. **Faster perceived speed** (UX)
   - Show partial results immediately, progressive loading
   - Estimated effort: 3 hours

Current search takes ~500ms for typical queries. Which matters most?
```

---

## 2. Simplicity First

### Over-abstraction

**User Request:** "Add a function to calculate discount"

**Bad (Overengineered):**
- Strategy pattern, abstract classes, dataclasses, config objects
- 40+ lines for a simple calculation

**Good:**

```python
def calculate_discount(amount: float, percent: float) -> float:
    """Calculate discount amount. percent should be 0-100."""
    return amount * (percent / 100)
```

**Add complexity only when needed:** Only when multiple discount types actually exist should you refactor.

### Speculative Features

**User Request:** "Save user preferences to database"

**Bad:** Adds caching layer, validation, merging, notifications, configurable paths.

**Good:**

```python
def save_preferences(db, user_id: int, preferences: dict):
    """Save user preferences to database."""
    db.execute(
        "UPDATE users SET preferences = ? WHERE id = ?",
        (json.dumps(preferences), user_id)
    )
```

---

## 3. Surgical Changes

### Drive-by Refactoring

**User Request:** "Fix the bug where empty emails crash the validator"

**Bad (Changes Everything):**
- Reformats all comments
- Adds type hints
- Changes validation logic beyond the reported bug
- Adds username validation nobody asked for

**Good (Only Changes What's Needed):**

```diff
-     if not user_data.get('email'):
+     email = user_data.get('email', '')
+     if not email or not email.strip():
          raise ValueError("Email required")
```

Only the two lines that fix empty email handling. Nothing more.

### Style Drift

**User Request:** "Add logging to the upload function"

**Bad:** Changes quote style, adds type hints, adds docstrings, reformats whitespace.

**Good (Match Existing Style):**
- Use same quote style as the file
- Skip type hints if the file doesn't have them
- Skip docstrings if the file doesn't have them
- Add logging in the exact style the existing code uses

---

## 4. Goal-Driven Execution

### Vague vs. Verifiable

**User Request:** "Fix the authentication system"

**Bad:** "I'll review the code, identify issues, and make improvements."

**Good:**

```
To "fix authentication," I need to define success criteria.
What specific issue are we solving?

If the issue is "users stay logged in after password change":

Plan:
1. Write test: Change password → verify old session invalidated
   Verify: Test fails (reproduces bug)

2. Implement: Invalidate sessions on password change
   Verify: Test passes

3. Check edge cases: Multiple active sessions, concurrent changes
   Verify: Additional tests pass

4. Verify no regression: Existing auth tests still pass
   Verify: Full test suite green

Current test coverage for auth: [shows coverage]
What's the specific auth issue you're seeing?
```

### Multi-Step with Verification

**User Request:** "Add rate limiting to the API"

**Good:**

```
Plan for rate limiting:

1. Add basic in-memory rate limiting (single endpoint)
   Verify: 100 requests → first 10 succeed, rest get 429

2. Extract to middleware (apply to all endpoints)
   Verify: Rate limits apply to /users and /posts; existing tests still pass

3. Add Redis backend (for multi-server)
   Verify: Rate limit persists across app restarts

4. Add configuration (rates per endpoint)
   Verify: /search allows 10/min, /users allows 100/min

Each step is independently verifiable and deployable.
Start with step 1?
```

### Test-First Verification

**User Request:** "The sorting breaks when there are duplicate scores"

**Bad:** Changes sort logic without confirming the bug.

**Good:**

```
1. First, write a test that reproduces the issue
   scores = [{'name': 'Alice', 'score': 100}, {'name': 'Bob', 'score': 100}]
   result = sort_scores(scores)
   Test this 10 times — if order is non-deterministic, the bug reproduces

2. Fix with stable sort
   return sorted(scores, key=lambda x: (-x['score'], x['name']))

3. Verify: Test passes consistently every time
```

---

## Anti-Patterns Summary

| Principle | Anti-Pattern | Fix |
|---|---|---|
| Think Before Coding | Silently assumes file format, fields, scope | List assumptions explicitly, ask for clarification |
| Simplicity First | Strategy pattern for single discount calculation | One function until complexity is actually needed |
| Surgical Changes | Reformats quotes, adds type hints while fixing bug | Only change lines that fix the reported issue |
| Goal-Driven | "I'll review and improve the code" | "Write test for bug X → make it pass → verify no regressions" |
| Local-First | Assumes remote/cloud when user says "local" | Verify endpoint URL and port before suggesting alternatives |
| Root Cause | Explains fallback without checking primary service | Trace full chain: browser → API → downstream → DB |
| Clarify | Makes 3 changes instead of asking "which part?" | Ask one clarifying question before acting |

## Anti-Patterns: Local-First

**User Request:** "Set up the local TTS server"

**Bad (Assumes Remote):**
```
You can use the cloud TTS API: https://api.cloud-tts.com/v1/synthesize
```

**Good (Local-First):**
```
The local TTS endpoint is http://127.0.0.1:10101/tts.
Is the Piper server running? Let me check:
curl -s http://127.0.0.1:10101/health

If it's not running, start it with:
python src/lib/piper-server.py --port 10101
```

## Anti-Patterns: Root Cause

**User Request:** "The TTS isn't working"

**Bad (Explains Symptom):**
```
The TTS fell back to Web Speech API because the Piper server isn't available.
```

**Good (Traces Chain):**
```
Let me trace the chain:

1. Browser → `/api/tts` → Next.js proxy
2. Next.js → `http://127.0.0.1:10101/tts` → Piper server

The Piper server isn't running on port 10101, so the fallback kicked in.
The real problem is Piper isn't started, not that "TTS failed."
```

## Anti-Patterns: Clarify

**User Request:** "the piper tts endpoint"

**Bad (Guesses):**
```
I'll update the endpoint URL and voice config.
```

**Good (Clarifies):**
```
You mentioned "the piper tts endpoint" — which part do you want to change?

1. The Next.js proxy URL (`/api/tts` → Piper server)
2. The Piper server config (port, voice, host)
3. The Web Speech API fallback

Which one?
```

## Key Insight

The "overcomplicated" examples aren't obviously wrong — they follow design patterns and best practices. The problem is **timing**: they add complexity before it's needed, which makes code harder to understand, introduces more bugs, takes longer to implement, and is harder to test.

The "simple" versions are easier to understand, faster to implement, easier to test, and can be refactored later when complexity is actually needed.

**Good code is code that solves today's problem simply, not tomorrow's problem prematurely.**

## Key Insight

The "overcomplicated" examples aren't obviously wrong — they follow design patterns and best practices. The problem is **timing**: they add complexity before it's needed, which makes code harder to understand, introduces more bugs, takes longer to implement, and is harder to test.

The "simple" versions are easier to understand, faster to implement, easier to test, and can be refactored later when complexity is actually needed.

**Good code is code that solves today's problem simply, not tomorrow's problem prematurely.**
