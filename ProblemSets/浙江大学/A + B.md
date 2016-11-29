# A + B

*时间限制：1000ms*  
*内存限制：32768K*


###题目描述：
　　读入两个小于100的正整数A和B,计算A+B. 需要注意的是:A和B的每一位数字由对应的英文单词给出


###输入：
测试输入包含若干测试用例,每个测试用例占一行,格式为"A + B =",相邻两字符串有一个空格间隔.当A和B同时为0时输入结束,相应的结果不要输出.

###输出：
对每个测试用例输出1行,即A+B的值.

###样例输入：
one + two =
three four + five six =
zero seven + eight nine =
zero + zero =


###样例输出：
3
90
96

###问题解析：
本题比较容易，只是需要注意细节处理。

看到题目一般思路都是读取字母再判断是否符合指定数字的英文拼写，读取一个单词（cin读取单词时恰好以空格为分界）后，使用循环逐个比较字母是否相同，完全匹配即可得出单词代表的数值。

但感觉上这种方法的处理更为麻烦，需要与十个英文单词逐个循环比较匹配（即使优化也需要循环一次，且优化的处理比较麻烦）。

因此，联想到本题可以使用英文单词的字母的ASCII码值的和作为分辨字母的依据，只要以空格或加减符号为分界，累加逐个字母的值即可。 实际使用中five与nine的字符值的和恰好相同，因此可在判断中添加单词的首字符，用以区分five和nine。

注意：cin>>char会跳过空白字符，请使用cin.get(char)读取单个字符。

###参考代码：

```
/*
author:pokemonWei
start_date:2016-11-9
version:1.0
*/
#include
#include
using namespace std;
int getFromEn(int n,char f);
int main(void){
    // std::cout << 'f'+'i'+'v'+'e' << std::endl;
    // std::cout << 'n'+'i'+'n'+'e' << std::endl;
  int a,b;
  a=b=0;
  int temp = 0;
  char ch = '\0';
  char f = '\0';
  do {
    a = b = 0;
    ch = f ='\0';
    cin.get(ch);
    while(ch != '+')
    {
      temp = 0;
      f = ch;
    //  std::cout << f << std::endl;
      while(ch != ' ' && ch != '+')
      {
        //std::cout << ch << std::endl;
        temp += ch;
        cin.get(ch);
      }
      cin.get(ch);
      a = a *10 + getFromEn(temp,f);
    }
    cin.get(ch);
    while(ch != '=')
    {
      temp = 0;
      //std::cin >> ch;
      f = ch;
      while(ch != ' ' && ch != '=')
      {
        temp += ch;
        cin.get(ch);
      }
        cin.get(ch);
      b = b*10 + getFromEn(temp,f);
    }
    if(a!=0 || b!=0)
      std::cout << a + b << std::endl;
    while (ch!='\n') {
      cin.get(ch);
    }
  } while(a != 0 || b !=0);
  return 0;
}
int getFromEn(int ascSum , char f)
{
  switch (ascSum) {
    case 'o'+'n'+'e':
      return 1;
    case 't'+'w'+'o':
      return 2;
    case 't'+'h'+'r'+'e'+'e':
      return 3;
    case 'f'+'o'+'u'+'r':
      return 4;
    // case 'f'+'i'+'v'+'e':
    //   return 5;
    case 's'+'i'+'x':
      return 6;
    case 's'+'e'+'v'+'e'+'n':
      return 7;
    case 'e'+'i'+'g'+'h'+'t':
      return 8;
    case 'n'+'i'+'n'+'e':
      if(f == 'n')
        return 9;
      else
        return 5;
    case 'z'+'e'+'r'+'o':
      return 0;
  }
  return 0;
}
```

###测试网站
www.nowcoder.com

###来源
浙大计算机研究生复试上机考试-2005年
