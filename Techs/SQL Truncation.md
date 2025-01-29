# Description

SQL truncation is a flaw in the database configuration in which an input is truncated (deleted) when added to the database due to surpassing the maximum defined length. The database management system truncates any newly inserted values to fit the width of the designated column size.

If the database considers spaces as valid characters between inputs and doesn’t do any trimming before storing the values, an attacker can create a duplicate accounts of an existing user like ‘’admin’’ with many additional spaces and characters — ‘’admin++++++random’’ that are too long to be stored in the specified column and gets deleted after passing the max length.

# Example of Usage

<h3>1st Step</h3> 

send POST request with login/register page and catch it with burp

![image](https://github.com/user-attachments/assets/8d7ac287-81a3-4f80-ae5a-28c7e2c1da97)

<h3>2nd Step</h3>

In burp add "+" and random value in the end with new password

![image](https://github.com/user-attachments/assets/53b30ce3-0a72-4a21-a09f-c1113ed500b7)

<h3>3rd Step</h3>

Output should be like this

![image](https://github.com/user-attachments/assets/23725d8f-6d7a-485e-ad26-0372c51b489f)


<h3>4th Step</h3>

Now login with rewritten password

![image](https://github.com/user-attachments/assets/158bf488-d419-4346-b1cd-d17e7195c6e0)
