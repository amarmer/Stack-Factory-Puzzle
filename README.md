### Stack Factory Puzzle

What code should be instead of function `main` comments, which doesn't call `new` and program output to console is:<br/><br/>
0::0 0::Process<br/>
1::1 1::Process<br/>
2::2 2::Process<br/>

```C++
#include <iostream>

struct IX
{
    virtual ~IX() {}
    virtual void Process() = 0;
};

template <int N>
struct X: public IX
{
    X() 
    { 
        std::cout << N << "::" << N << " "; 
    }
    
    virtual void Process() 
    { 
        std::cout << N << "::Process\n"; 
    }
};

int main()
{
  for (auto i = 0; i < 3; i++)
  {
    IX* pIX = nullptr;

    // Code should be here.

    pIX->Process();
  }

  return 0;
}
