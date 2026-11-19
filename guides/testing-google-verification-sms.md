# Testing a Google Verification SMS

*By Alex Carter, Editor at GetVerifyCode*

Google uses a text code for sign-in, recovery, and some 2-step checks. This note is for a QA pass on a flow your team owns or is allowed to test. Record one request carefully. Do not treat a refused number as a flaky carrier.

## What you are proving

A useful run answers four questions:

- Did the stored number match the number Google was asked to text?
- Did a code arrive before the expiry window closed?
- Did a resend invalidate the previous code?
- Did your logs stay free of the OTP string?

Google may refuse some number types. Save the exact message and the number type. That refusal belongs in the test report as a constraint.

## Run the check once

1. Enter the number in E.164 and read it back before you submit.
2. Request a single code. Note the clock time.
3. Record the sender, the arrival time, and the code length. Do not copy the code into Slack, email, or analytics.
4. Enter the code in the product under test.
5. After the cooldown, request one resend. Confirm the first code now fails and the new code works.
6. Scan logs for the OTP. Fail the run if the raw code is there.

If nothing arrives, check the stored number before you blame the route. A wrong country code, a leading zero left on a national number, or a landline will look like a missed SMS.

## Fields worth keeping

| Field | Pass signal |
| --- | --- |
| E.164 number | Same value in the app and in the inbox |
| Request and arrival timestamps | Arrival is inside the expiry window |
| Sender | Matches the sender you expect for this Google flow |
| Resend | First code rejected, second code accepted |
| Logs | No OTP string in events or traces |

Clock skew and a late SMS often show up as "invalid code" after the window has closed. Write the times down so that case is obvious.

## Temporary numbers

When the test needs a number you do not want tied to a personal SIM, reserve one for the Google check on [GetVerifyCode](https://getverifycode.com/sms-verification/google). The hold is about 20 minutes. If no SMS arrives, the held amount returns to your wallet. Top up your wallet from $1; each number is priced live.

If Google rejects that range, stop and record it. Switching countries belongs in the test plan, not in a loop of retries.

## Related

- [When the OTP SMS Does Not Arrive](./when-otp-sms-does-not-arrive.md)
- [Checking a WhatsApp Code in QA](./checking-whatsapp-codes-in-qa.md)
- Checklist: [getverifycode.github.io](https://getverifycode.github.io/)
