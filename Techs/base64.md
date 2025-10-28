# Decode String

echo [base64 encoded string] | base64 -d

# Encode String

echo [string] | base64

# Encode String without wrapping lines 

echo [string] | base64 -w 0

-w 0 - means do not wrap output lines, meaning if the line is big it will considered as one whole

Double clicking on a line without -w 0

<img width="1864" height="296" alt="image" src="https://github.com/user-attachments/assets/5ff14e33-2abd-4afb-a8da-0dca0812ae7c" />

Double clicking on a line WITH -w 0

<img width="2842" height="345" alt="image" src="https://github.com/user-attachments/assets/ec3614c2-66b4-4c37-8aff-e357238f8591" />
