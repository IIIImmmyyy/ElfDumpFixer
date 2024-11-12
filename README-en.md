# ElfDumpFixer
## Introduction
### ElfDumpFixer is a shell tool based on the Android 12 linker, designed for streamlined dumping of required .so files. It is particularly useful for unpacking .so files that have been protected by libtprt. While certain sections of the Section Table remain unmodified, all critical information is restored.
## support
### Android12-14
## Usage
### Example: Injecting with Frida
```javascript
let module = Module.load("/data/data/com.bilibili.warmsnow/ElfDumpAndFix.so");
let nativePointer = module.findExportByName("_Z6DumpSoPKcS0_"); // Locate exported function address
let dumpFun = new NativeFunction(nativePointer, "void", ['pointer', 'pointer']);
dumpFun(Memory.allocUtf8String("libil2cpp.so"), Memory.allocUtf8String("/data/data/com.bilibili.warmsnow/dump_libil2cpp.so"));

```
### Check the logcat output for "Dump so /data/data/com.bilibili.warmsnow/dump_libil2cpp.so Done!" to confirm completion.
### After extracting the global-metadata.dat file, it can be used along with the unpacked .so in Il2CppDumper.

### Test Environment
- System: Android 12
- Device：Pixel 6a
- Game: Warm Snow
- Protection：libtprt
