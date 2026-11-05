# Reconciliation playbooks

These are original decision guides. They do not call services or prove a service's current API behavior. Read only the section needed for the task.

## Gmail send

Prefer a returned message ID. Otherwise inspect Sent mail with the intended account and a narrow time/recipient scope. Check the actual candidate before concluding that it is the same send. A delayed index or inaccessible thread leaves the outcome unknown. Do not search the entire mailbox or resend to see what happens. The SQLite helper records a short non-secret reference such as `message-42`; it does not read Gmail.

## GitHub file update

After a lost update response, fetch the current file and inspect the relevant commit/content identity. If the intended content is already present, avoid a duplicate commit. If a newer update is present, do not overwrite it to restore a guessed state. Check the API's concurrency rules before retrying with a SHA. The helper does not call GitHub or resolve merge conflicts.

## File upload

Use the receipt or upload ID when available. Compare the actual destination and package identity; filename equality alone is weak evidence. A visible file with a different digest is not the completed intended upload. Do not upload another copy because the first upload is still processing.

## Browser submission

Look for a confirmation, stable submission ID, or destination record. A closed spinner or disabled button is not a receipt. Re-observe after navigation or interruption before deciding. Do not refresh a POST confirmation page or press Submit again until the outcome is reconciled.
