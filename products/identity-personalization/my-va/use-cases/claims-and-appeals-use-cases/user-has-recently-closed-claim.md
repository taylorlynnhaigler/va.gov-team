# My VA Claims and Appeals Use Case: User has a claim or appeal that has been closed in the last 60 days

**Last updated:** April 13, 2023

For LOA3 users who sign in and have a claim or appeal that has been closed within the last 60 days, we will show a card for that claim or appeal with the current status of “Complete” in the Claims and Appeals section on My VA.

## UX
- Any logged in LOA3 user can see the Claims and Appeals section on My VA.
- If a logged in LOA3 user has a claim or appeal that has been closed in the last 60 days, they will see a card in this section that tells them the type of claim or appeal, the date the application was received, a current status update of “Complete”, and a link to "Review details" which links to the details page for that specific claim in the claims tool. The claim details link is specific to the claim card. It is in the following format and the ###### is the claim number: https://va.gov/track-claims/your-claims/########/status.
- When a user has a claims or appeals card to show, they will also see a link to "Manage all claims and appeals" which links to the [claims tool](https://www.va.gov/claim-or-appeal-status/) where they can view a list of all current and past claims.
- This card is always displayed on the lefthand side of the page on desktop and at the top of the list directly under the Claims and appeals header on mobile.
- Once a claim or appeal has been closed for longer than 60 days, the status card will no longer show on My VA.
- Uses the [card component](https://design.va.gov/components/card) from the VA design system.
- [Desktop mockup](https://www.sketch.com/s/9b0e6efc-423a-4354-9db3-ab2083d566c9/a/uuid/47848588-D962-4ED8-8936-3B496E7F7C54)
- [Mobile mockup](https://www.sketch.com/s/9b0e6efc-423a-4354-9db3-ab2083d566c9/a/uuid/54A44752-3361-4BE7-891D-0116F56C690B)

## How to reproduce

- Find a staging user who has a claim or appeal closed in the last 60 days in the [claims and appeals staging user test cases](https://github.com/department-of-veterans-affairs/va.gov-team-sensitive/blob/master/Administrative/vagov-users/staging-test-accounts-myvaaudit.md#claims-and-appeals-section).
- Log into staging.va.gov with a test user who has a recently closed claim to show.
- Once logged in, you will be redirected to My VA.
- Verify that you see a card for the recently closed claim or appeals under the "Claims and appeals" header and that the status says “Complete”.
- Verify that the link in the card to “Review details” links to the details page about that particular claim and the status in the claims tool matches what is displaying on My VA.
- Verify that you see a secondary link to “Manage all claims and appeals” that links to the claims tool and that it appears on the righthand side on desktop.
