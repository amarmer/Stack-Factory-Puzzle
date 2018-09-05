### Stack Factory Puzzle

What code should be instead of function `main` comments, which doesn't call `new` and program output to console is:<br/><br/>
X0::X0 X0::Process: A<br/>
X1::X1 X1::Process: ABC<br/>
X2::X2 X2::Process: 12345<br/>

```C++
#include <iostream>
#include <string>

struct X0: public X
{
  X0() { std::cout << "X0::X0 "; }
  ~X0() { c_ = ' '; }
    
  void Process() override { std::cout << "X0::Process: " << c_ << std::endl; }
  
  char c_ = 'A';
};

struct X1: public X
{
  X1() { std::cout << "X1::X1 "; }
  ~X1() { s_.clear(); }
    
  void Process() override { std::cout << "X1::Process: " << s_ << std::endl; }
  
  std::string s_ = "ABC";
};

struct X2: public X
{
  X2() { std::cout << "X2::X2 "; }
  ~X2() { i_ = 0; }
    
  void Process() override { std::cout << "X2::Process: " << i_ << std::endl; }
  
  int i_ = 12345;
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
