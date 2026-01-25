---
source_url: https://docs.aws.amazon.com/bedrock/latest/userguide/claude-messages-thinking-differences.html
fetched_at: 2026-01-25T03:13:30.502224
---

# Differences in thinking
            across model versions

# Differences in thinking across model versions

The Messages API handles thinking differently across Claude 3.7 Sonnet and Claude 4 models, primarily in redaction and summarization behavior. The following table summarizes those differences.

Feature |
Claude 3.7 Sonnet |
Claude 4 Models |
|---|---|---|
Thinking output |
Returns the full thinking output |
Returns summarized thinking |
Redaction handling |
Uses |
Redacts and encrypts full thinking, returned in a
|
Interleaved thinking |
Not supported |
Supported with a beta header |