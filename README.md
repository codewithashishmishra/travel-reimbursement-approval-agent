# Travel Reimbursement Approval Agent

Ashish Mishra

This is a small notebook that checks the five sample travel claims from the assignment against the mock policy and returns one decision per claim.

## Setup

Use Python 3.11 or newer.

In this folder, create a file named `.env`:

```
GEMINI_API_KEY=your_key_here
```

`GOOGLE_API_KEY` works too if that is what you already have. To try another model, set `GEMINI_MODEL`. If you leave it blank, the notebook uses `gemini-3.5-flash-lite`.

Open `ashishmishra.ipynb` and run the cells from top to bottom. The first cell installs `google-genai`, `matplotlib`, and `python-dotenv`.

Keep the key in `.env`. That file is ignored by git, so it will not be uploaded.

## How to run the demo

The five claims are the Appendix B JSON inside the notebook.

Gemini has to call the tools before it decides. The notebook prints each call: policy lookup, receipt check, category and limit check, approval tier, timeliness, and duplicate check.

The last code cell prints a JSON array with one result per claim.

The chart is under the Dashboard heading and is also saved next to the notebook as `UI SS_1.png`.

## Design choices

The model chooses which tools to call and writes the explanation. The dollar caps, receipt rules, and approval tiers come back from the tools.

Temperature is set to 0. If a draft does not match those tool results, the notebook asks the model to revise it. The notebook does not paste in its own decision.

`tools_used` is the list of tools that actually ran for that claim.

If a receipt is missing, the airfare is business or first class, or the reimbursable total is over 2000 USD, the claim goes to Manual Review. Nothing is auto paid or auto deducted in that case.
