![image](https://github.com/mytechnotalent/0x06_arm_32_hacking_char_pointer/blob/main/RPI32AAHCP.png)

# 0x06_arm_32_hacking_char_pointer
ARM 32-bit Raspberry Pi Char Pointer example in Kali Linux.

<br>

## Join DC540 Discord [HERE](https://discord.gg/TC9V9RCr5U)

<br>

## FREE Reverse Engineering Self-Study Course [HERE](https://github.com/mytechnotalent/Reverse-Engineering-Tutorial)

<br>

## Schematic
![image](https://github.com/mytechnotalent/0x06_arm_32_hacking_char_pointer/blob/main/schematic.png?raw=true)

## Parts
[Raspberry Pi 4](https://www.adafruit.com/product/4292)<br>
[64GB Micro SD Card](https://www.amazon.com/SDSDQUA-064G-A11-Professional-MicroSDXC-formatted-recording/dp/106171327X)<br>
[Micro SD Card Reader/Writer](https://www.amazon.com/uni-Adapter-Supports-Compatible-MacBook/dp/B081VHSB2V)

## STEP 1: Download Kali Linux ARM Image - Raspberry Pi 32-bit
[Download](https://images.kali.org/arm-images/kali-linux-2020.4-rpi4-nexmon.img.xz) [https://www.offensive-security.com/kali-linux-arm-images/]

## STEP 2: Download balenaEtcher
[Download](https://www.balena.io/etcher)

## STEP 3: Flash Kali Linux ARM Image
[Watch YT Null Byte Video](https://www.youtube.com/watch?v=Jquf9BDm4iU&t=493s)

## STEP 4: Power Up RPI & Login
***POWER UP DEVICE AND LOGIN AS KALI AND SET UP SSH***

## STEP 5: Create File In VIM
```c
#include <stdio.h>

int main()
{
    char *x;

    x = "hello world!";

    printf("%s\n", x);

    return 0;
}
```

## STEP 6: Save File As - 0x06_arm_32_hacking_char_pointer.c [:wq]

## STEP 7: Build & Link
```
gcc -o 0x06_arm_32_hacking_char_pointer 0x06_arm_32_hacking_char_pointer.c
```

## STEP 8: Run Binary
```
./0x06_arm_32_hacking_char_pointer
hello world!
```

## STEP 9: Run Radare2 - Debug Mode
```
r2 -d ./0x06_arm_32_hacking_char_pointer
```

## STEP 10: Run Radare2 - Debug Step 1 [Examine Binary @ Entry Point]
```
aaa
s main
vv
```
![image](https://github.com/mytechnotalent/0x06_arm_32_hacking_char_pointer/blob/main/1.png?raw=true)

## STEP 11: Run Radare2 - Debug Step 2 [Examine char pointer]
```
q
[0x004e7500]> px @ 0x4e7528
- offset -   0 1  2 3  4 5  6 7  8 9  A B  C D  E F  0123456789ABCDEF
0x004e7528  6400 0000 2de9 f843 0746 0c4e 0c4d 8846  d...-..C.F.N.M.F
0x004e7538  7e44 9146 7d44 fff7 30ef 761b b610 0ad0  ~D.F}D..0.v.....
0x004e7548  043d 0024 55f8 043f 4a46 4146 3846 0134  .=.$U..?JFAF8F.4
0x004e7558  9847 a642 f6d1 bde8 f883 00bf d009 0100  .G.B............
0x004e7568  c809 0100 7047 00bf 0840 2de9 0880 bde8  ....pG...@-.....
0x004e7578  0100 0200 6865 6c6c 6f20 776f 726c 6421  ....hello world!
0x004e7588  0000 0000 70fe ff7f 0100 0000 0000 0000  ....p...........
0x004e7598  0000 0000 0000 0000 0000 0000 0000 0000  ................
0x004e75a8  0000 0000 0000 0000 0000 0000 0000 0000  ................
0x004e75b8  0000 0000 0000 0000 0000 0000 0000 0000  ................
0x004e75c8  0000 0000 0000 0000 0000 0000 0000 0000  ................
0x004e75d8  0000 0000 0000 0000 0000 0000 0000 0000  ................
0x004e75e8  0000 0000 0000 0000 0000 0000 0000 0000  ................
0x004e75f8  0000 0000 0000 0000 0000 0000 0000 0000  ................
0x004e7608  0000 0000 0000 0000 0000 0000 0000 0000  ................
0x004e7618  0000 0000 0000 0000 0000 0000 0000 0000  ................
[0x004e7500]>
```

## STEP 12: Run Radare2 - Debug Step 3 [Hack char pointer]
```
[0x004e7500]> w hacked world @0x004e757c
```

## STEP 13: Run Radare2 - Debug Step 4 [Review Hack]
```
[0xb6e43c66]> ps @0x004e757c
hacked world
```

## STEP 14: Run Radare2 - Debug Step 5 [Hack Binary Permanently]
```
q
r2 -w ./0x06_arm_32_hacking_char_pointer
[0x000003fc]> aaa
[0x000003fc]> s main
[0x000003fc]> vv
```
![image](https://github.com/mytechnotalent/0x06_arm_32_hacking_char_pointer/blob/main/2.png?raw=true)
```
q
[0x0000053c]> w hacked world @0x0000057c
```

## STEP 15: Prove Hack
```
./0x06_arm_32_hacking_char_pointer
hacked world
```

## Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

Please make sure to update tests as appropriate.

## License
[Apache License, Version 2.0](https://www.apache.org/licenses/LICENSE-2.0)
