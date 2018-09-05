### Stack Factory Puzzle

What code should be instead of function `main` comments, which doesn't call `new` and program output to console is:<br/><br/>
X0::X0 X0::Process<br/>
X1::X1 X1::Process<br/>
X2::X2 X2::Process<br/>

```C++
#include <iostream>

struct X
{
  virtual ~X() {}
  virtual void Process() = 0;
};

struct X1: public X
{
  X1() { std::cout << "X1::X1 "; }
    
  void Process() override { std::cout << "X1::Process\n"; }
};

struct X2: public X
{
  X2() { std::cout << "X2::X2 "; }
    
  void Process() override { std::cout << "X2::Process\n"; }
};

struct X3: public X
{
  X3() { std::cout << "X3::X3 "; }
    
  void Process() override { std::cout << "X3::Process\n"; }
};

int main()
{
  for (auto i = 0; i < 3; i++)
  {
    X* pX = nullptr;

    // Code should be here.

    pX->Process();
  }

  return 0;
}
