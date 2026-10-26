# When the OTP SMS Does Not Arrive

*By Alex Carter, Editor at GetVerifyCode*

Most "code never came" tickets are not mysterious. The message was never accepted by the carrier, it was filtered, or the wrong number was submitted. Work the list below before blaming the SMS provider.

## Confirm the number first

1. Ask the user to read back the full number, including country code.
2. Check that the app stored E.164 (for example `+14155550100`), not a national format with a leading zero still attached.
3. Retry with a different device or SIM only after the stored number is proven correct.

A large share of failures stop here: wrong country picker, pasted spaces, or a landline that cannot receive SMS.

## Check timing and resend behavior

- Codes usually expire in a few minutes. Entering an old code after a resend often returns "invalid".
- Each resend should cancel the previous code. If the UI still accepts the first code, that is a product bug, not a carrier issue.
- Rapid resend clicks can trip provider or app rate limits. Wait for the cooldown.

## Carrier and device causes

| Symptom | Likely cause |
| --- | --- |
| No SMS at all | Wrong number, blocked sender ID, or region the provider cannot reach |
| Delayed by minutes | Congestion, roaming, or deferred short-code delivery |
| Message in spam / blocked | Carrier filtering or device SMS blocker |
| Arrives without a usable code | Truncated template, encoding issue, or wrong message thread |

Also check signal, airplane mode, dual-SIM routing, and a full SMS inbox on older devices.

## App-side causes worth logging

- The provider rejected the send (invalid destination, unsupported country, insufficient balance).
- The app never called the gateway because validation failed silently.
- The code was generated but the SMS template omitted it.
- Logs or analytics stored the OTP string (security issue) while the user still saw nothing.

Log provider response codes and message IDs. Do not log the OTP itself.

## Temporary numbers and "virtual" ranges

Some platforms refuse known virtual or VoIP ranges. If you are testing with a temporary inbound number, confirm that the destination app accepts that number type. Failure here is policy, not delivery.

With [GetVerifyCode](https://getverifycode.com/), you reserve a number for about 20 minutes and read inbound SMS in the browser. If no SMS arrives for that hold, the held amount returns to your wallet. Top up your wallet from $1; each number is priced live.

## Escalation order for support

1. Verify the exact number on file.
2. Check whether a code was generated and whether the provider accepted the send.
3. Ask for approximate wait time and whether any SMS from other senders arrived in that window.
4. Offer a resend after the cooldown, then a different number or channel (authenticator, email) if the product allows it.
5. File a ticket with provider message ID, country, and timestamp. Never paste live OTPs into tickets.

## Longer read

A fuller list of fixes lives on the product blog: [Didn't Get the Verification Code? 12 Fixes](https://getverifycode.com/blog/didnt-receive-verification-code-sms-fixes).

## FAQ

### Why does resend make the first code stop working?

Because a correct implementation issues a new secret and invalidates the previous one. That prevents two valid codes from living at once.

### Can airplane mode cause a missed OTP?

Yes. The SMS may arrive after the code has already expired, which looks like "invalid code" rather than "never delivered".

### Should support ask the user to forward the SMS?

Prefer not to. Forwarded messages can leak codes into email threads and chat logs. Ask for timing and sender name instead.
