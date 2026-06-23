# QScriptMangager
A script manager inside a QWidget-based Terminal window


**RPRMScripting** version 0.0.1a

**What Can A Script Do**
- normal standard lib python, possible with some restriction on disk access
- a script can request additional data from the host:
 - Packed Files: GetPackedFile("roman_ass.rigid_model_v2")
 - Request Data Processing: Conver the RMV2 Binaryt into a common mesh format (which is also done by a script)
 - Manipulate the loaded data
 - Send Back the loaded data

**Ideas for different type of calling convention**
```c++
void Raw_Basic(int Handle, Uint64 param1, Uint64 param2, Uint64 param3 ,Uint64 param4)   // Data is sendt trough these 64 bit value, could be ptrs, could be....
- Raw_Query(Handle, Uint64 param1, Uint64 param2, Uint64 param3 ,Uint64 param4)  // Same, but the script can send message back to host

- Formatted_Basic(Handle, JSON data) // uses JSON to neat format data
- Formatted_Quere(Handle, JSON data) // same with data query

- Formatted_Raw(Handle, JSON metaData, List<Uint64> data) // possible a fastere way of transfering big data
- Formatted_Quere(Handle, , JSON metaData, List<Uint64> data))
```
