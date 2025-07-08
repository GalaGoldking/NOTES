# Getting args

Just include inside int main following: int main(int argc, char* argv[])

```
#include <iostream>

int main(int argc, char* argv[]){
        std::cout << "Number of arguments: " << argc;
        std::cout << "Arguments: " << std::endl;

        for (int i = 0; i < argc; i++){
                std::cout << "Argument" << i << ": " << argv[i] << std::endl;
        }

        return 0;
}
```
