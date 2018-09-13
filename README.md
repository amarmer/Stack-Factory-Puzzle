### Stack Factory Puzzle

#### When instances of classes derived from the same class need to be created based on certain conditions,<br/>they are created on the heap. The puzzle is about how to create them on the stack.


In `main`, code between comments `Begin` `End` creates instances of classes `X0` or `X1` or `X2` (depends on `i`) on the heap<br/>
(similar to a factory function which creates instances of classes on the heap and returns pointer to their base class).<br/>
Console output of the program is:
```C++
X0::X0 X0::Process: A   X0::~X0
X1::X1 X1::Process: ABC	X1::~X1
X2::X2 X2::Process: 123	X2::~X2
```
How to modify code between the comments `Begin` `End`, that it doesn't call `new` nor `placement new` and output is the same.<br/>

```C++
#include <iostream>
#include <string>
#include <memory>

struct X
{
  friend struct X0;
  friend struct X1;
  friend struct X2;
  
  virtual ~X() {}
  virtual void Process() = 0;
  
private:
  X() {}
};

struct X0 final: public X
{
  X0() { std::cout << "X0::X0 "; }
  ~X0() { std::cout << "\tX0::~X0\n"; }
    
  void Process() override { std::cout << "X0::Process: " << c_; }
  
  char c_ = 'A';
};

struct X1 final: public X
{
  X1() { std::cout << "X1::X1 "; }
  ~X1() { std::cout << "\tX1::~X1\n"; }
    
  void Process() override { std::cout << "X1::Process: " << s_; }
  
  std::string s_ = "ABC";
};

struct X2 final: public X
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
```

#### The sames solutions ([solution](https://twitter.com/isocpp/status/1039615649759211520) and [solution](https://github.com/amarmer/Stack-Factory-Puzzle/pull/2)) and [solution](https://github.com/amarmer/Stack-Factory-Puzzle/issues/4) are already published. 
