---
title: vtop
description: The vtop extension converts a virtual address to the corresponding physical address, and displays other page table and page directory information.
ms.assetid: 41f4accc-3eb9-4406-a6cc-a05022166e14
keywords: ["vtop Windows Debugging"]
topic_type:
- apiref
api_name:
- vtop
api_type:
- NA
---

# !vtop


The **!vtop** extension converts a virtual address to the corresponding physical address, and displays other page table and page directory information.

Syntax

``` syntax
!vtop PFN VirtualAddress 
!vtop 0 VirtualAddress 
```

## <span id="ddk__vtop_dbg"></span><span id="DDK__VTOP_DBG"></span>Parameters


<span id="_______DirBase______"></span><span id="_______dirbase______"></span><span id="_______DIRBASE______"></span> *DirBase*   
Specifies the directory base for the process. Each process has its own virtual address space. Use the [**!process**](-process.md) extension to determine the directory base for a process.

<span id="_______PFN______"></span><span id="_______pfn______"></span> *PFN*   
Specifies the page frame number (PFN) of the directory base for the process.

<span id="_______0______"></span> **0**   
Causes **!vtop** to use the current [process context](changing-contexts.md#process-context) for address translation.

<span id="_______VirtualAddress______"></span><span id="_______virtualaddress______"></span><span id="_______VIRTUALADDRESS______"></span> *VirtualAddress*   
Specifies the virtual address whose page is desired.

### <span id="DLL"></span><span id="dll"></span>DLL

Kdexts.dll

### <span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>Additional Information

For other methods of achieving these results, see [Converting Virtual Addresses to Physical Addresses](converting-virtual-addresses-to-physical-addresses.md). Also see [**!ptov**](-ptov.md). For information about page tables and page directories, see *Microsoft Windows Internals*, by Mark Russinovich and David Solomon.

Remarks
-------

To use this command, first use the [**!process**](-process.md) extension to determine the directory base of the process. The page frame number (PFN) of this directory base can be found by removing the three trailing hexadecimal zeros (in other words, by right-shifting the number 12 bits).

Here is an example:

```
kd> !process 0 0
**** NT ACTIVE PROCESS DUMP ****
....
PROCESS ff779190  SessionId: 0  Cid: 04fc    Peb: 7ffdf000  ParentCid: 0394
 DirBase: 098fd000  ObjectTable: e1646b30  TableSize:   8.
    Image: MyApp.exe
```

Since the directory base is 0x098FD000, its PFN is 0x098FD.

```
kd> !vtop 98fd 12f980
Pdi 0 Pti 12f
0012f980 09de9000 pfn(09de9)
```

Notice how the trailing three zeros are optional. The **!vtop** extension displays the page directory index (PDI), the page table index (PTI), the virtual address that you had originally input, the physical address of the beginning of the physical page, and the page frame number (PFN) of the page table entry (PTE).

If you want to convert the virtual address 0x0012F980 to a physical address, you simply have to take the last three hexadecimal digits (0x980) and add them to the physical address of the beginning of the page (0x09DE9000). This gives the physical address 0x09DE9980.

If you forget to remove the three zeros, and pass the full directory base to **!vtop** instead of the PFN, the results will usually be correct. This is because when **!vtop** receives a number too large to be a PFN, it right-shifts it twelve bits and uses that number instead:

```
kd> !vtop 98fd 12f980
Pdi 0 Pti 12f
0012f980 09de9000 pfn(09de9)

kd> !vtop 98fd000 12f980
Pdi 0 Pti 12f
0012f980 09de9000 pfn(09de9)
```

However, it is better to always use the PFN, because some directory base values will not be converted in this manner.

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[debugger\debugger]:%20!vtop%20%20RELEASE:%20%285/15/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")



