### Stack Factory Puzzle

What code should be instead of function `main` comments, which doesn't call `new` and program output to console is:<br/>
```C++
X0::X0 X0::Process: A   X0::~X0
X1::X1 X1::Process: ABC	X1::~X1
X2::X2 X2::Process: 123	X2::~X2
```
<br/>

```C++
#include <iostream>
#include <string>

struct X
{
  virtual ~X() {}
  virtual void Process() = 0;
};

struct X0: public X
{
  X0() { std::cout << "X0::X0 "; }
  ~X0() { std::cout << "\tX0::~X0\n"; }
    
  void Process() override { std::cout << "X0::Process: " << c_; }
  
  char c_ = 'A';
};

struct X1: public X
{
  X1() { std::cout << "X1::X1 "; }
  ~X1() { std::cout << "\tX1::~X1\n"; }
    
  void Process() override { std::cout << "X1::Process: " << s_; }
  
  std::string s_ = "ABC";
};

struct X2: public X
{
  X2() { std::cout << "X2::X2 "; }
  ~X2() { std::cout << "\tX2::~X2\n"; }
    
  void Process() override { std::cout << "X2::Process: " << i_; }
  
  int i_ = 123;
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
