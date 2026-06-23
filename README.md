# QScriptMangager
A script manager inside a QWidget-based Terminal window


**RPRMScripting** version 0.0.1a

**What Can A Script Do**
- normal standard lib python, possibly with some restriction on disk access
- a script can request additional data from the host:
 - Packed Files: GetPackedFile("roman_ass.rigid_model_v2")
 - Request Data Processing: Convert the RMV2 Binaryt into a common mesh format (which is also done by a script)
 - Manipulate the loaded data
 - Send Back the loaded data
- many different scripts can you simultanously, including many instances of the same script
 - Each "Script Instance" has a unique handle
 - ScriptInstance are handle using a "Message Bus" (Win32API, anyone?)


**Ideas for different type of calling convention**
```c++
void Raw_Basic(ScriptHandle Handle, uint64_t param1, uint64_t param2, uint64_t param3 ,uint64_t param4)   // Data is sendt trough these 64 bit value, could be ptrs, could be....
void Raw_Query(ScriptHandle Handle, int64_t param1, uint64_t param2, uint64_t param3 ,uint64_t param4) // Same, but the script can send message back to host

void Formatted_Basic(ScriptHandle handle, JSON data) // uses JSON to neat format data
void Formatted_Quere(ScriptHandle handle, JSON data) // same with data query

void Formatted_Raw((ScriptHandle handle, JSON metaData, std::map<Tag, void*> data) // faster way, for big data chunks, MetaData describes the pointers, IDed by Tag
void Formatted_Query((ScriptHandle handle, JSON metaData, std::map<Tag, void*> data) // Same, but with callback
```

**Imnplmenation sounds like a nightmare**
To make adoption easier, we pledge to cut corners, and use dumb code
for example, at the outset, the scriptmanger does not need a message system, CPython can just inject the functions scripts are allowed to call
dirty, worky.

**How do scripts send data back to caller**
 - Through a callback

**How do script raise an evente like "GetPackfedFile" over CLI **
  - The Caller listens for a file `request.JSON`
  - Script writes `request.JSON`
  - SCriptNanager listens for `answer.jon`
  - The Call processer the JSON request and writes the result in `answer.Json`

Very clumsy maybe, but it is a startpoint

