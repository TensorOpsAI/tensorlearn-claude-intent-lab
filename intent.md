# Intent: results-ready notification

Sources: `inputs/01-approved-prd.md` (approved PRD N-17, 2026-09-18) and `inputs/02-current-meeting.md` (discovery notes, 2026-09-20). `inputs/03-superseded-request.md` is superseded history and approves nothing here.

## Problem

The fictional clinic receives avoidable calls from patients who only want to know whether their results are ready. Patients have no signal telling them when a result has been reviewed and released, so they phone to check (PRD N-17).

## Proposed outcome

- **I-1** A patient is notified when a result is ready for their review in the existing authenticated portal.
- **I-2** A notification is eligible only after a doctor has reviewed and released the result. "Ready" does not mean the laboratory upload finished.
- **I-3** The message says only that an update is available and directs the patient to the existing authenticated portal.

How success will be observed:

- **I-4** Fewer status-only calls, counted separately from clinical questions and compared against a measured baseline (support lead).
- **I-5** Delivery failures are tracked as a measure in their own right.
- **I-6** No numeric target is approved. The baseline and target are to be agreed during discovery; none is stated here.

## Affected users and systems

- The patient is the only recipient covered by this intent.
- The existing authenticated portal and its existing result route.
- The notification delivery path and its operational logs.
- The support team that takes the status calls, and the doctors who review and release results.

## Out of scope

- **X-1** Portal redesign, and a new patient dashboard (a separate project per the engineering lead).
- **X-2** Appointment scheduling.
- **X-3** Clinical interpretation.
- **X-4** Notifying third parties. This is excluded; the referring doctor is handled separately as OPEN-2 and is not approved.
- **X-5** Everything approved only by the superseded early request: sending on lab upload, putting result details in an SMS, copying the referring doctor, rebuilding the dashboard and the call-reduction target it set.

## Constraints

- **C-1** A doctor must review and release a result before any notification is eligible.
- **C-2** No diagnosis, test result, clinical measurement or treatment detail in the message, the notification or the operational logs.
- **C-3** Access is authenticated in the existing portal. No results attached to the message and no public result link.
- **C-4** No duplicate notification for the same released result version.
- **C-5** Delivery failures are handled without sending duplicate patient messages.
- **C-6** Use the existing portal result route.

## Open questions

- **OPEN-1** Channel (SMS, email or portal push). Owners: product and privacy, after the consent and delivery review. Consent and the actual channel are still under review.
- **OPEN-2** Notification to the referring doctor. Owners: clinical and privacy, who must decide recipient authorization. It is not approved by the PRD and must not be inferred from the old request.
- **OPEN-3** The baseline and numeric target for call reduction, to be agreed during discovery. Nothing is invented here.

```json
{
  "notifyWhen": ["doctor-reviewed", "released"],
  "messageMayInclude": ["update-available"],
  "inScope": ["existing-portal-route", "duplicate-prevention", "delivery-failure-handling"],
  "openDecisions": [
    {"topic": "channel", "owners": ["product", "privacy"]},
    {"topic": "referring-doctor-notification", "owners": ["clinical", "privacy"]}
  ],
  "successMeasures": ["status-only-calls", "delivery-failures"],
  "numericTarget": null
}
```
