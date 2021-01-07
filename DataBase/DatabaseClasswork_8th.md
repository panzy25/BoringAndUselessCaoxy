# 数据库第8次随堂作业

<center>最小覆盖</center>



> written by panzy25, 18372046
>
> Typora used
>
> Based on Markdown

## 1. 问题

**Assume that we wish to construct a database from a set of data items {A, B, C, D, E, F, G} (which will become attributes in tables) and a set F of FDs given by F=(1)BCD** **→** **A, (2) BC** **→** **E, (3) A** **→** **F, (4) F** **→** **G, (5) C** **→** **D, (6) A** **→** **G. **

**Find the minimal cover for this set of FDs and name this set G.**

1. 将函数依赖的右边分解为第一属性。

2. 去除多余的闭包。

   |    依赖    | 依赖左边的原始闭包 | 去除依赖后的闭包 |
   | :--------: | :----------------: | :--------------: |
   | (1)BCD → A |     {ABCDEFG}      |      {BCDE}      |
   | (2)BC → E  |     {ABCDEFG}      |     {ABCDFG}     |
   |  (3)A → F  |       {AFG}        |       {AG}       |
   |  (4)F → G  |        {FG}        |       {F}        |
   |  (5)C → D  |        {CD}        |       {C}        |
   |  (6)A → G  |       {AFG}        |      {AFG}       |

   在去除依赖后，(1)~(5)的对应闭包都减少了，因此只需要去除(6)。

3. 去除依赖中左边的多余部分

   $\because$ C → D

   $\therefore$  BCD → A  可以去除D

   即BC → A

4. 综上所述，答案为

   **G = {BC** **→** **A, BC** **→** **E, A** **→** **F, F** **→** **G, C** **→** **D}** 













