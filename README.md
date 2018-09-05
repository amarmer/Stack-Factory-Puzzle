### Stack Factory Puzzle

What code should be instead of function `main` comments, which doesn't call `new` and program output to console is:<br/><br/>
X0::X0 X0::Process<br/>
X1::X1 X1::Process<br/>
X2::X2 X2::Process<br/>

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
    std::cout << "X" << N << "::X" << N << " "; 
  }
    
  virtual void Process() 
  { 
    std::cout << "X" << N << "::Process\n"; 
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
