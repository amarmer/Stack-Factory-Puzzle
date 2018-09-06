### Stack Factory Puzzle

#### Solution of the puzzle shows that in some cases objects derived from the same class can be created on the stack.

In `main`, code between comments `Begin` `End` creates objects `X0` or `X1` or `X2` (based on `i`) on the heap,<br/>
similar to a factory function which creates objects on the heap and returns pointer to their base class.<br/>
Console output of the program is:
```C++
X0::X0 X0::Process: A   X0::~X0
X1::X1 X1::Process: ABC	X1::~X1
X2::X2 X2::Process: 123	X2::~X2
```
How to modify code between the comments `Begin` `End`, that it doesn't call `new` and console output is the same.
<br/>

```C++
#include <iostream>
#include <string>
#include <memory>

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

    // Begin 
    if (i == 0)
      pX = new X0;
    else if (i == 1)
      pX = new X1;
    else 
      pX = new X2;
      
    std::unique_ptr<X> x{pX};    
    // End

    pX->Process();
  }

  return 0;
}
