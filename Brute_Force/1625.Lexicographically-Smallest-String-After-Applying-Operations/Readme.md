### 1625.Lexicographically-Smallest-String-After-Applying-Operations

此题号称“LC史上最难周赛第二题”。从数据规模和历史经验来看，应该可以暴力解决问题，但是该怎么暴力才对呢？

#### 解法1：

题目告知字符串的长度是偶数。我们的第一个发现是，如果b是偶数的话，无论怎么rotate，每次add操作总是作用在所有的奇数位上。rotate只影响数字的排列，而不影响数值的大小。数值的大小只取决于你做了几次add。这就提示我们，可以先尽情地add，然后再尽情地rotate，两者可以互不影响。我们可以穷尽所有add的结果，再穷尽所有rotate的结果，再找其中的最小值即可。

再拓展一下，如果b是奇数的话，我们发现rotate一次之后，add操作其实作用在原本的偶数位上；再rotate一次之后，add操作又作用在原本的奇数位上。也就是说，我们可以通过rotate操作，来给所有的奇数位或者所有的偶数位加上任意的数值。奇数位上能加的数值，和偶数位上能加的数值，两者并不影响。同样，我们可以（分别在奇数位和偶数位上）穷尽所有add的结果，再穷尽所有rotate的结果，再找其中的最小值即可。

关于“穷尽所有add的结果”，我们只需要尝试最多add十次。因为```add a*10```和```add a```这两个操作本质上是一样。关于“穷尽所有rotate的结果”，我们也只需要最多rotate n次，因为```rotate by b```和```rotate by n*b```的效果也是一样的。但更高效的方法是，我们需要rotate的次数是```n/gcd(n,b)```.

#### 解法2：
既然add和rotate可以解耦合，那么另一种思路就是先枚举rotate，再确定最优的add。

在外层循环，我们枚举rotate的决策。然后我们查看如果b%2==1，说明我们允许对奇数位进行add操作，自然我们会选择最优的操作数使得str[0]最小。此外，无论b的奇偶性，我们都能对偶数位进行add操作，自然我们会选择最优的操作数使得str[1]最小。至此，奇数位和偶数位的操作次数都已经确定下来了，那么整个数也就确定下来了。
