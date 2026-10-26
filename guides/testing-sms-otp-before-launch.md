# Testing SMS OTP Before Launch

*By Alex Carter, Editor at GetVerifyCode*

Mocks prove your UI wiring. They do not prove carriers will deliver a code in the countries you sell into. Run at least one real inbound SMS path in staging before you call the release done.

## What "ready" means

Treat the SMS path as ready only when all of the following hold:

- Happy-path delivery meets your p50 / p95 target for at least one production country.
- Resend shows a cooldown and rejects the previous code.
- Expired and rate-limited states show clear copy.
- OTP strings never appear in logs, analytics, or error trackers.
- Country picker and dialing code stay aligned for the numbers you accept.

## Minimum matrix

| Scenario | Assert |
| --- | --- |
| Domestic long number | Code arrives within SLO; E.164 paste works |
| International number | Country picker and dial code stay aligned |
| Immediate resend | Cooldown shows; previous code is rejected |
| Expired code | Clear expired or invalid message; new code works |
| Provider reject | Readable error; no silent hang |
| Log spot check | OTP string never appears in events or traces |

Printable sheet: [test matrix](https://github.com/GetVerifyCode/otp-sms-testing-checklist/blob/main/docs/test-matrix.md).

## Full checklist

The maintained checklist lives in two places:

- Interactive (local progress): [getverifycode.github.io](https://getverifycode.github.io/)
- Copy-paste for tickets: [CHECKLIST.md](https://github.com/GetVerifyCode/otp-sms-testing-checklist/blob/main/CHECKLIST.md)
- Repository: [GetVerifyCode/otp-sms-testing-checklist](https://github.com/GetVerifyCode/otp-sms-testing-checklist)

Cover input formatting, delivery, validation, and security. Fail the release if any security item is unchecked.

## Using temporary inbound numbers in QA

Personal SIMs do not scale across countries. A temporary inbound number lets QA exercise live routes without sharing private phones.

On [GetVerifyCode](https://getverifycode.com/), pick the service and country, reserve a number for about 20 minutes, and read the SMS in the inbox. If no SMS arrives, the held amount returns to your wallet. Top up your wallet from $1; each number is priced live.

Only test apps you own or are authorized to test. Follow each platform's terms and local law. Some platforms reject virtual ranges; document that as a known constraint, not a flaky test.

## After launch

Keep a thin smoke path in CI or a weekly manual run: one domestic send, one resend, one log scan. Carrier behavior changes. A checklist that only ran once will rot.

## Related

- [How SMS Verification Works](./how-sms-verification-works.md)
- [When the OTP SMS Does Not Arrive](./when-otp-sms-does-not-arrive.md)
- Product blog: [QA checklist for SMS OTP testing](https://getverifycode.com/blog/qa-checklist-sms-otp-testing)
