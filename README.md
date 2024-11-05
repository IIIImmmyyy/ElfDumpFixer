

# [Android U3D手游安全中级篇]
# [https://github.com/IIIImmmyyy/u3dCourse](https://github.com/IIIImmmyyy/U3DGameCourse)

- [README 中文](./README.md)
- [README English](./README-en.md)
# ElfDumpFixer
## 介绍
### 基于Android12 linker的脱壳机。 用于一键Dump需要的So。可用于被 libtprt加固后的so脱壳。只有部分SectionTable未修复。关键信息全部修复
## 使用
### 注意：请保证在需要DumpSo的加载之前就已经完成注入调用，否则信息将有错误;
### 以frida为例子自行注入所在进程
```javascript
let module = Module.load("/data/data/com.bilibili.warmsnow/ElfDumpAndFix.so");
let nativePointer = module.findExportByName("_Z6DumpSoPKcS0_");//获取导出函数地址 (soname, dumpPath)  参数为需要Dump的so名字和dump路径
let dumpFun = new NativeFunction(nativePointer,"void",['pointer','pointer']);
dumpFun(Memory.allocUtf8String("libil2cpp.so"),Memory.allocUtf8String("/data/data/com.bilibili.warmsnow/dump_libil2cpp.so"));
```
#### 观察 logcat 输出Dump so /data/data/com.bilibili.warmsnow/dump_libil2cpp.so Done! 即为结束； 
#### global-metadata.dat文件 自行提取后 可结合脱壳下来的So 直接在 Il2CppDumper 中使用。
#### 如果你想要知道如何提取global-metadata.dat文件或者更多的游戏安全知识 可报名我的课程：https://github.com/IIIImmmyyy/U3DGameCourse

### 测试环境
- 系统：Android 12
- 机型：Pixel 6a
- 游戏：暖雪
- 加固厂商：libtprt

### 注意！！！ 非Android12系统 linker结构体变化有可能无法正常工作，该项并未测试！
