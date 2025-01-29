# Description

SQL truncation is a flaw in the database configuration in which an input is truncated (deleted) when added to the database due to surpassing the maximum defined length. The database management system truncates any newly inserted values to fit the width of the designated column size.

If the database considers spaces as valid characters between inputs and doesn’t do any trimming before storing the values, an attacker can create a duplicate accounts of an existing user like ‘’admin’’ with many additional spaces and characters — ‘’admin++++++random’’ that are too long to be stored in the specified column and gets deleted after passing the max length.

# Example of Usage

<ol>
  <li>
    ![image](https://github.com/user-attachments/assets/a95d4c54-59ad-462e-8669-55eb2d58804a)

  </li>
</ol>
