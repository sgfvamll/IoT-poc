# D-Link DIR809 Vulnerability

The Vulnerability is in page `/formWlanSetup` which influences the latest version of this router OS. 

The firmware version is [DIR-809Ax_FW1.12WWB03_20190410](http://www.dlinktw.com.tw/techsupport/ProductInfo.aspx?m=DIR-809) 

 ## Vulnerability description

In the function `FUN_80040af8`, which is called by `FUN_80041fc4`( page `/formWlanSetup` ), we find two stack overflow vulnerabilities. Each of them allows attackers to execute arbitrary code on system via a crafted post request. 

Here is the description of the first vulnerability,  

1. The `get_var` function extracts user input from the a http request. For example, the code below will extract the value of a key of format `"ssid_%d"` in the http post request which is completely under the attacker's control. 
2. The string `pcVar1` obtained from user is copied onto the stack using `strcpy` without checking its length. So we can make the stack buffer overflow in `local_18`. 

![2021-05-10_11h44_26](README/2021-05-10_11h44_26.png)

The second vulnerability follows the same paradigm as the first. First get the user input in `pcVar1` and then copy to `local_18` without checking its length. 

![2021-05-10_11h52_46](README/2021-05-10_11h52_46.png)



## PoC

``` 

```





## Acknowledgment

Credit to  [@Ainevsia](https://github.com/Ainevsia), [@peanuts62](https://github.com/peanuts62), [@Lnkvct](https://github.com/Lnkvct/IoT-poc) from Shanghai Jiao Tong University and TIANGONG Team of Legendsec at Qi'anxin Group.

