---
title: u, ub, uu (Unassemble)
description: The u\ commands display an assembly translation of the specified program code in memory.Do not confuse this command with the ~u (Unfreeze Thread) command.
ms.assetid: 933a308c-61d1-4ca4-89c1-5749ba1b41c1
keywords: ["u, ub, uu (Unassemble) Windows Debugging"]
ms.author: windowsdriverdev
ms.date: 05/23/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
topic_type:
- apiref
api_name:
- u, ub, uu (Unassemble)
api_type:
- NA
---

# u, ub, uu (Unassemble)


The **u\*** commands display an assembly translation of the specified program code in memory.

Do not confuse this command with the [**~u (Unfreeze Thread)**](-u--unfreeze-thread-.md) command.

``` syntax
u[u|b] Range 
u[u|b] Address
u[u|b] 
```

## <span id="ddk_cmd_unassemble_dbg"></span><span id="DDK_CMD_UNASSEMBLE_DBG"></span>Parameters


<span id="_______Range______"></span><span id="_______range______"></span><span id="_______RANGE______"></span> *Range*   
Specifies the memory range that contains the instructions to disassemble. For more information about the syntax, see [Address and Address Range Syntax](address-and-address-range-syntax.md). If you use the **b** flag, you must specify *Range* by using the "*Address* **L***Length*" syntax, not the "*Address1 Address2*" syntax.

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
Specifies the beginning of the memory range to disassemble. Eight instructions (on an x86-based processor) or nine instructions (on an Itanium-based processor) are unassembled. For more information about the syntax, see [Address and Address Range Syntax](address-and-address-range-syntax.md).

<span id="_______b______"></span><span id="_______B______"></span> **b**   
Determines the memory range to disassemble by counting backward. If **ub** *Address* is used, the disassembled range will be the eight or nine byte range ending with *Address*. If a range is specified using the syntax **ub** *Address* **L***Length*, the disassembled range will be the range of the specified length ending at *Address*.

<span id="_______u______"></span><span id="_______U______"></span> **u**   
Specifies that the disassembly will continue even if there is a memory read error.

### <span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>Environment

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Modes</strong></p></td>
<td align="left"><p>User mode, kernel mode</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Targets</strong></p></td>
<td align="left"><p>Live, crash dump</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>Platforms</strong></p></td>
<td align="left"><p>All</p></td>
</tr>
</tbody>
</table>

 

### <span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>Additional Information

For more information about assembly debugging and related commands, see [Debugging in Assembly Mode](debugging-in-assembly-mode.md).

Remarks
-------

If you do not specify a parameter for the **u** command, the disassembly begins at the current address and extends eight instructions (on an x86-based or x64-based processor) or nine instructions (on an Itanium-based processor). When you use **ub** without a parameter, the disassembly includes the eight or nine instructions before the current address.

Do not confuse this command with the [**up (Unassemble from Physical Memory)**](up--unassemble-from-physical-memory-.md). The **u** command disassembles only virtual memory, while the **up** command disassembles only physical memory.

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[debugger\debugger]:%20u,%20ub,%20uu%20%28Unassemble%29%20%20RELEASE:%20%285/15/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")




