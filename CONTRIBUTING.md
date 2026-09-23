# Contributing to Donna

Donna is a proprietary product by Semicolon One Technologies.
All rights reserved. Copyrights enforced.

## Contribution Policy

External code contributions are accepted only with prior written approval from Semicolon One Technologies.
If you want to propose an improvement, contact Semicolon One Technologies through official company channels.

## Development Setup

For local development instructions in this repository, refer to the setup guides under `docs/contribution/`.

## Legal

By submitting any contribution, you acknowledge that:

- Donna and related code are proprietary to Semicolon One Technologies.
- Submission does not grant any license to Donna IP except as explicitly agreed in writing.
- Semicolon One Technologies may accept, modify, or reject submissions at its sole discretion.

## Pull Request Requirements

### Telephony Provider Integration Pull Requests

Telephony changes require thorough review and testing. Every telephony pull request must follow the requirements in this section and include clear documentation and a video demonstrating the complete integration and end-to-end local testing. Maintainers will use these requirements when evaluating whether a pull request is ready for review.

#### Required Evidence

The video must demonstrate all of the following:

- All provider-side setup required before configuring the integration in Donna, including where to find the account credentials and any other required values
- Configuring the provider integration in Donna
- Outbound calls
- Inbound calls
- Number provisioning and any required KYC flow
- Error handling, including an attempt to add a number that the provider account does not own

The pull request must also document the provider setup, configuration, API behavior, number-provisioning flow, and KYC requirements. Where the implementation relies on a specific provider API, add a link to the relevant provider API documentation in a code comment near the applicable logic.

#### Scope of Telephony Integrations

A telephony provider integration pull request must focus on complete, working core calling functionality. Ideally, the integration should support both inbound and outbound calls. If the provider does not support one direction, or it cannot reasonably be included, explain the limitation and its effect on the integration in the pull request.

Additional capabilities, such as call transfer or other provider-specific add-ons, must be submitted in separate pull requests. Keeping these features separate allows maintainers to validate the core integration independently.

Pull requests that omit required documentation, have API mismatches, leave number provisioning or KYC unclear, or do not adequately demonstrate the core calling functionality may be blocked or rejected, depending on the size of the gaps and the pull request's overall compliance with this guide.

### AI Provider Integration Pull Requests

This section applies to new or changed TTS, STT, LLM, realtime, embeddings, and other third-party AI providers.

#### Provider Eligibility

Before maintainers perform detailed code review, the pull request must explain why Donna should support the provider: the user need or maintainer sponsorship, the clear benefit over providers already supported, and links to the provider's public API documentation and pricing. The provider must have a usable public API, self-service account or credential setup, and a credible support or maintenance path.

Providers must be generally available for production use, with a publicly documented and stable API, for at least six months. Alpha, beta, private-preview, or newly launched providers are not accepted by default. A maintainer may approve a documented exception before implementation when there is a compelling user or product need.

#### Required Evidence

Contributors must create or use a real provider account and test the complete integration manually in Donna. Unit, mock, and provider-SDK tests are required where appropriate, but they are not evidence that the Donna integration works.

The pull request must include redacted evidence of all of the following:

- Provider-side account and credential setup (never commit or share secrets)
- Configuring and saving the provider in the Donna UI or API
- Running a real Donna workflow through the same adapter, endpoint, protocol, and authentication scheme that the PR adds
- The resulting provider output and the selected settings
- Redacted provider API request/response logs showing the endpoint, protocol, status, and request fields (never include credentials or user data)
- Invalid-credential and network/error behaviour

For TTS, show real audio produced by Donna and its voice, language, speed, format, sample rate, and duration as applicable. For STT, show a known audio input and transcript. For LLM and realtime providers, show a real Donna turn and any claimed tool or structured-output behaviour.

Include the test date, Donna commit SHA, provider endpoint/API version, and the command, workflow, or recording used to produce the evidence. A direct API request, provider sample SDK, or smoke test using a different protocol does not satisfy this requirement.

Pull requests without a convincing provider-value case or complete live Donna evidence will be rejected without detailed implementation review.
