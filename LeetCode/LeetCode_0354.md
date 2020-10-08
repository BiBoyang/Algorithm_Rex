# LeetCode_0354 俄罗斯套娃信封问题

```C++
sort(envelopes.begin(), envelopes.end(), [&](auto& a, auto& b) { 
    return a[0] < b[0] || (a[0] == b[0] && a[1] < b[1]); 
});



```

