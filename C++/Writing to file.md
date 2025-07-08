# Include necessary header fstream

```
#include <fstream>
```

# Choose appropriate file stream class

`ofstream`: stream class to write on file

`ifstream`: stream class to read from files

`fstream`: stream class to both read and write from/on files

# Open file

In order to open a file with a stream object we use its member function `open`:

`open (filename, mode)`

 - ## Modes

<table>
  <tr>
    <td>ios::in</td>
    <td>Open for input operations</td>
  </tr>
  <tr>
    <td>ios::out</td>
    <td>Open for output operations</td>
  </tr>
  <tr>
    <td>ios::binary</td>
    <td>Open in binary mode</td>
  </tr>
  <tr>
    <td>ios::ate</td>
    <td>Set the initial position at the end of the file. If this flag is not set, the initial position is the beginning of the file</td>
  </tr>
  <tr>
    <td>ios::app</td>
    <td>All output operations are performed at the end of the file, appending the content of the current content of the file</td>
  </tr>
  <tr>
    <td>ios::trunc</td>
    <td>If the file is opened for output operations and it already existed, its previous content is deleted and replaced by the new one</td>
  </tr>
</table>

All these flags can be combined using the bitwise operator OR (|).

```
ofstream myFile;
myFile.open ("test.txt", std::ios::out | std::ios::app | std::ios::binary);
```

| class | default mode parameter |
| ----- | ---------------------- |
| ofstream | std::out |
| ifstream | std::in |
| fstream  | std::in \| std::out |

 - ## Check if a file stream was successful opening a file
```
if (myFile.is_open()) {
  /* ok, proceed with output */
}
```

# Closing a file

When we are finished with out input and output operations on a file we shall close it so that the operating system is notified and its resources become available again. For that, we call the stream's member function called `close`. The member function takes flushes the associated buffers and closes the file.

`myFile.close()`

# Text files

- ## Writing to a file
  ```code
  #include <iostream>
  #include <fstream>

  int main(){
    std::ofstream myFile ("test.txt");
    if (myFile.is_open()){
      myFile << "This is a line \n";
      myFile << "This is another line \n";
      myFile.close();
    }
    else {
      std::cout << "Unable to open file";
    }
    return 0;
  }
  ```
- ## Reading a file
  ```
  #include <iostream>
  #include <fstream>

  int main(){
    std::string line;
    std::ifstream myFile ("test.txt");
    if (myFile.is_open()){
      while(getline (myFile, line)){
        std::cout << line << '\n';
      }
    myFile.close();
    }
    else {
      std::cout << "Unable to open a file";
    }
  return 0;
  ```

# Checking a state flags

 - ### `bad()`
   Returns true if a reading or writing operation fails. For example, in the case that we try to write to a file that is not open for writing or if the device where we try to write has no space left.
 - ### `fail()`
   Returns true in the same cases as bad(), but also in the case that a format error happens, like when an alphabetical character is extracted when we are trying to read an integer number.
 - ### `eof()`
   Returns true if a file open for reading has reached the end.
 - ### `good()`
   It is the most generic state flag: it returns false in the same cases in which calling any of the previous functions would return true. Note that good and bad are not exact opposites (good checks more state flags at once).
The member function `clear()` can be used to reset the state flags.

# get and put stream positioning 

