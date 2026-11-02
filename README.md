Self-Healing Financial Ledger

An Excel workbook that takes a raw list of transactions, finds the bad ones, sets them aside for review, and keeps a clean ledger of everything that passed. A dashboard at the end shows whether the numbers add up.

I built this to deal with a common problem: transaction exports with text in the amount column, negative values where there shouldn't be any, and no easy way to see what was dropped. Instead of deleting or hand-fixing rows, this keeps every record accounted for.

File: Self_Healing_Financial_Ledger.xlsx

Sheets
01_Raw_Transaction_Stream - the original data as it arrives. Some rows are intentionally broken (for example INVALID_AMT or a negative amount).
02_Error_Trap_Engine - checks each amount, labels the problem if there is one, and gives it an error code. It also numbers the bad rows and the good rows separately so the next sheets can pick them up in order.
03_Quarantine_Recovery_Log - every failed transaction with the reason it failed. These need a manual fix.
04_Healed_General_Ledger - every transaction that passed, ready to post.
05_Control_Center_Dashboard - total records, quarantined records, health score and a status line.
Error codes
Code	Meaning
ERR-FIN-01	Amount is not a valid number
ERR-FIN-02	Amount is negative
NONE	No problem found
How the numbers stay consistent

Sheet 02 decides once whether a row is an error. Sheets 03, 04 and 05 all read that same decision, so they can't disagree with each other. The dashboard checks that total records equals clean records plus quarantined records. If it doesn't, the status changes to RECONCILIATION BREAK.

Adding new data
Add new rows at the bottom of sheet 01.
Fill the formulas in sheets 02, 03 and 04 down to the same row.
Check the dashboard.

The formulas are set up to read down to row 1000.
