# Reading a Verification Code from the API

*By Alex Carter, Editor at GetVerifyCode*

Some QA runs should not watch a handset. The inbox can be polled over HTTP, then the code can be entered by the test. This page is the sequence. Request and response shapes live in the API docs, not here.

Only do this for an app you own or are authorized to test.

## Sequence

1. Call `GET /api/v1/catalog/meta`. Continue only when the public API is available.
2. Create an API key on a confirmed account and top up the wallet. Top up your wallet from $1. Each number is priced live.
3. Load destinations and routes for the service and country you intend to test. Quote with the operator from that route list.
4. Buy with a new idempotency key. Use the same key only when you are retrying that same purchase.
5. Poll the activation while it is pending. The window is about 20 minutes. When the status is received, read the code from the SMS payload (`sms[].otp_code`).
6. If no SMS arrives in the window, the held amount returns to the wallet. You can cancel an activation you still own.

Do not log the code. Log the activation id, the service, the country, and the timestamps.

The contract, including quote, buy, poll, and cancel, is documented at [GetVerifyCode for developers](https://getverifycode.com/developers).

## What the test should assert

| Step | Assert |
| --- | --- |
| Meta | Public API is available before the suite spends money |
| Quote | Service, country, and operator match the case you meant to run |
| Buy | Response includes an activation id and a phone number |
| Poll | Status moves to received, or the hold ends with no SMS |
| Secrets | OTP appears in the test assertion only, never in shared logs |

Prices come back as integer cents in USD. Do not hard-code a retail amount in the test. Quote again when the run starts.

## Failures that are not carrier bugs

- The idempotency key was reused for a different purchase, so you observed the first order again.
- The operator on buy did not match the operator you quoted.
- The suite logged the OTP into CI output.
- The destination app rejected the number type. Record that as policy.

## Related

- [Testing SMS OTP Before Launch](./testing-sms-otp-before-launch.md)
- [Checking a WhatsApp Code in QA](./checking-whatsapp-codes-in-qa.md)
- [Testing a Google Verification SMS](./testing-google-verification-sms.md)
- Checklist: [getverifycode.github.io](https://getverifycode.github.io/)
