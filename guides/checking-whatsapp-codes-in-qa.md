# Checking a WhatsApp Code in QA

*By Alex Carter, Editor at GetVerifyCode*

Use this note when you are testing a WhatsApp verification flow you own, or one you are allowed to test. The goal is a written pass or fail for one code request. It is a QA record, not a way to open accounts for other people.

## What a pass looks like

Treat the run as a pass only when all of these are true:

- The number you submitted is the number that received the message.
- You stored that number in E.164 before the request.
- The code arrived before it expired, and you recorded the sender and the arrival time.
- After one resend, the first code is rejected and the new code works.
- The OTP string is not in your logs, analytics, or the ticket.

If WhatsApp refuses the number, record the refusal and stop. That is a platform rule for that number type. Retrying the same range does not turn it into a delivery bug.

## Before you request a code

1. Pick a number your team controls for this test.
2. Write it in E.164, for example `+14155550100`.
3. Confirm the country picker and the dialing code describe that same number.
4. Plan one request, then at most one resend after the cooldown.

Rapid resend clicks hit WhatsApp limits and your own rate limits. Wait for the cooldown before you call the run invalid.

## What to write down

| Field | Why it matters |
| --- | --- |
| Number in E.164 | Proves the app and the inbox refer to the same destination |
| Request time and arrival time | Separates a slow route from a code that expired |
| Sender | Shows whether the SMS came from the expected WhatsApp sender |
| Code length | Lets the next run compare like with like |
| Result after resend | Confirms the first code died when a new one was issued |
| Refusal text, if any | Distinguishes policy from a carrier miss |

Do not paste the live code into the ticket, chat, or an analytics event. A hash or a simple "received" flag is enough.

## Temporary numbers

A personal SIM does not scale when you need another country. A temporary inbound number lets the test read the SMS in a browser.

For a WhatsApp check, reserve the number on [GetVerifyCode](https://getverifycode.com/sms-verification/whatsapp). The hold is about 20 minutes. If no SMS arrives, the held amount returns to your wallet. Top up your wallet from $1; each number is priced live.

Some apps reject virtual ranges. If this run is refused, write down the number type and move to a type your test plan allows.

## Related

- [Testing SMS OTP Before Launch](./testing-sms-otp-before-launch.md)
- [Reading a Verification Code from the API](./reading-a-verification-code-from-the-api.md)
- Checklist: [getverifycode.github.io](https://getverifycode.github.io/)
