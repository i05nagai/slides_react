# slide 1 
- 1ページ目item1

--
count:false
- 1ページ目item2
.center[centered text]
.right[right text]
.left[left text]
.center[![:scale 70%](image/test.jpg)]

---

# slide 2
- 2ページ目

$$
x = a_{1} + b^{2}
$$
## フーリエ変換
$$
  F(u) = \int\_{-\infty}^{\infty} f(x)\mathrm{e}^{-j2\pi ux}dx
$$

## 2次元のフーリエ変換
$$
  F(u,v) = \int\_{-\infty}^{\infty} \int\_{-\infty}^{\infty} f(x,y)\mathrm{e}^{-j2\pi (ux + vy )}dxdy
$$

---
# slide3

```cpp
int main(int argc, char const* argv[])
{
    USDMarketFactory usdMarketFactory();
    IMarket usdMarket = usdMarketFactory();
    IFactory usdCurveFactory(usdMarket);
    CurveSet usdCurveSet = usdCurveFactory();
    return 0;
}

```

