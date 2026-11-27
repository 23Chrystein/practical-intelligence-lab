[README.md](https://github.com/user-attachments/files/35500130/README.md)
# Synthetic Customer-Support Dataset

## Purpose

This fictional dataset supports Project 001: Small Business Intelligence Toolkit. It is intended for developing and testing customer-support analytics, data validation, data cleaning and reporting features.

**All records are synthetic.** They do not represent real customers, businesses, orders or support interactions.

## File

- `support_tickets_synthetic.csv` — 200 rows and 9 columns.

## Column dictionary

| Column | Description | Expected values / rules |
|---|---|---|
| `ticket_id` | Reference assigned to a support ticket | Text identifier; expected to be unique |
| `date_received` | Date the support request was received | Date in `YYYY-MM-DD` format |
| `channel` | Channel through which the request arrived | `email`, `live_chat`, `social_media`, `phone` |
| `enquiry_type` | Main reason for the contact | `delivery`, `refund`, `product_defect`, `cancellation`, `product_information`, `payment`, `other` |
| `product_name` | Product associated with the request, when applicable | Text; may be blank when no specific product applies or is known |
| `priority` | Support team's assigned urgency | `low`, `medium`, `high` |
| `resolution_status` | Current state of the ticket | `resolved`, `open`, `pending` |
| `first_response_hours` | Elapsed hours from receipt to first support response | Numeric and non-negative; may be blank if not recorded |
| `resolution_hours` | Elapsed hours from receipt to resolution | Numeric and non-negative for resolved tickets; blank for open or pending tickets |

## Important interpretation rules

1. `first_response_hours` measures time to the first response, not time to resolution.
2. `resolution_hours` measures total time from receipt to resolution.
3. A blank `resolution_hours` is expected for tickets whose status is `open` or `pending`. Do not automatically treat those blanks as data errors.
4. A blank `product_name` is allowed because some enquiries may not relate to a specific product.
5. `ticket_id` should be unique. Repeated IDs should be flagged for investigation.
6. Categories should be normalised carefully. Unknown category values should be flagged for review rather than silently assigned to a known category.
7. The dataset does not contain customer names, contact details, addresses, order numbers or other personal identifiers.

## Deliberately included data-quality issues

The raw CSV includes examples for testing validation and cleaning:

- Blank `first_response_hours` values.
- Blank `product_name` values.
- Inconsistent capitalisation and surrounding spaces in some category values.
- An unknown `enquiry_type` value (`technical_issue`).
- A malformed date (`2026-15-40`).
- A negative `first_response_hours` value.
- A duplicated `ticket_id`.

These issues are intentional. The application should detect and report them. It should not silently discard records or make irreversible corrections without a documented rule.

## Suggested first checks

- Confirm the file has 200 rows and 9 columns.
- Check whether `ticket_id` values are unique.
- Parse `date_received` and identify invalid dates.
- Inspect missing values by column.
- Compare category values with the allowed lists above.
- Check numeric durations for negative or non-numeric values.
- Confirm that unresolved tickets can legitimately have blank `resolution_hours`.

## Reproducibility

The dataset was generated synthetically with a fixed random seed (`20261127`) so the same underlying example data can be reproduced. The deliberate quality issues are documented above.

## Licence and use

This dataset is provided for learning, development and testing within the Practical Intelligence Lab initiative. It is fictional and should not be interpreted as evidence about actual customer behaviour or business performance.
