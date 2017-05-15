---
title: object
description: The object extension displays information about a system object.
ms.assetid: dc6d862b-3246-4d5b-992c-8723a0347f1d
keywords: ["object Windows Debugging"]
topic_type:
- apiref
api_name:
- object
api_type:
- NA
---

# !object


The **!object** extension displays information about a system object.

``` syntax
!object Address [Flags] 
!object Path
!object 0 Name 
!object -p
!object {-h|-?}
```

## <span id="ddk__object_dbg"></span><span id="DDK__OBJECT_DBG"></span>Parameters


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
If the first argument is a nonzero hexadecimal number, it specifies the hexadecimal address of the system object to be displayed.

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *Flags*   
Specifies the level of detail in the command output.

Set *Flags* to a bitwise OR of these values:

<span id="0x0"></span><span id="0X0"></span>**0x0**  
Display object type.

<span id="0x1"></span><span id="0X1"></span>**0x1**  
Display object type, object name, and reference counts.

<span id="0x8"></span><span id="0X8"></span>**0x8**  
Display the contents of an object directory or the target of a symbolic link. This flag has an effect only if **0x1** is also set.

<span id="0x10"></span><span id="0X10"></span>**0x10**  
Display optional object headers.

<span id="0x20"></span><span id="0X20"></span>**0x20**  
Display the full path to a named object. This flag has an effect only if **0x1** is also set.

The *Flags* parameter is optional. The default value is 0x9.

<span id="_______Path______"></span><span id="_______path______"></span><span id="_______PATH______"></span> *Path*   
If the first argument begins with a backslash (\), **!object** interprets it as an object path name. When this option is used, the display will be arranged according to the directory structure used by the Object Manager.

<span id="_______Name______"></span><span id="_______name______"></span><span id="_______NAME______"></span> *Name*   
If the first argument is zero, the second argument is interpreted as the name of a class of system objects for which to display all instances.

<span id="_______-p"></span><span id="_______-P"></span> **-p**  
Display private object name spaces.

<span id="-h-_"></span><span id="-H-_"></span>{**-h**|**-?**}  
Display help for this command.

### <span id="DLL"></span><span id="dll"></span>DLL

Kdexts.dll

### <span id="Examples"></span><span id="examples"></span><span id="EXAMPLES"></span>Examples

This example passes the path of the \\Device directory to **!object**. The output lists all objects in the \\Device directory.

``` syntax
0: kd> !object \Device
Object: ffffc00b074166a0  Type: (ffffe0083b768690) Directory
    ObjectHeader: ffffc00b07416670 (new version)
    HandleCount: 0  PointerCount: 224
    Directory Object: ffffc00b074092e0  Name: Device

    Hash Address          Type          Name
    ---- -------          ----          ----
     00  ffffe0083e6a61f0 Device        00000044
         ffffe0083dcc4050 Device        00000030
         ffffe0083d34f050 Device        NDMP2
         ffffe0083bdf7060 Device        NTPNP_PCI0002
         ...
         ffffe0083b85d060 Device        USBPDO-8
         ffffe0083d33d050 Device        USBFDO-6
         ...
         ffffe0083bdf0060 Device        NTPNP_PCI0001
```

Choose one of listed objects, say USBPDO-8. Pass the address of USBPDO-8 (ffffe0083b85d060) to **!objec**t. Set *Flags* to 0x0 to get minimal information.

``` syntax
0: kd> !object ffffe0083b85d060 0x0
Object: ffffe0083b85d060  Type: (ffffe0083b87df20) Device
    ObjectHeader: ffffe0083b85d030 (new version)
```

Include name and reference count information for the same object by setting *Flags* to 0x1.

``` syntax
0: kd> !object ffffe0083b85d060 0x1
Object: ffffe0083b85d060  Type: (ffffe0083b87df20) Device
    ObjectHeader: ffffe0083b85d030 (new version)
    HandleCount: 0  PointerCount: 6
    Directory Object: ffffc00b074166a0  Name: USBPDO-8
```

Get optional header information for the same object by setting *Flags* to 0x10.

``` syntax
0: kd> !object ffffe0083b85d060 0x10
Object: ffffe0083b85d060  Type: (ffffe0083b87df20) Device
    ObjectHeader: ffffe0083b85d030 (new version)
Optional Headers: 
    NameInfo(ffffe0083b85d010)
```

The following example calls **!object** twice for a Directory object. The first time, the contents of the directory are not displayed because the 0x8 flag is not set. The second time, the contents of the directory are displayed because both the 0x8 and 0x1 flags are set (Flags = 0x9).

``` syntax
0: kd> !object ffffc00b07481d00 0x1
Object: ffffc00b07481d00  Type: (ffffe0083b768690) Directory
    ObjectHeader: ffffc00b07481cd0 (new version)
    HandleCount: 0  PointerCount: 3
    Directory Object: ffffc00b07481eb0  Name: Filters

0: kd> !object ffffc00b07481d00 0x9
Object: ffffc00b07481d00  Type: (ffffe0083b768690) Directory
    ObjectHeader: ffffc00b07481cd0 (new version)
    HandleCount: 0  PointerCount: 3
    Directory Object: ffffc00b07481eb0  Name: Filters

    Hash Address          Type          Name
    ---- -------          ----          ----
     19  ffffe0083c5f56e0 Device        FltMgrMsg
     21  ffffe0083c5f5060 Device        FltMgr
```

The following example calls **!object** twice for a SymbolicLink object. The first time, the target of the symbolic link is not displayed because the 0x8 flag is not set. The second time, the target of the symbolic link is splayed because both the 0x8 and 0x1 flags are set (Flags = 0x9).

``` syntax
0: kd> !object ffffc00b07628fb0 0x1
Object: ffffc00b07628fb0  Type: (ffffe0083b769450) SymbolicLink
    ObjectHeader: ffffc00b07628f80 (new version)
    HandleCount: 0  PointerCount: 1
    Directory Object: ffffc00b074166a0  Name: Ip6

0: kd> !object ffffc00b07628fb0 0x9
Object: ffffc00b07628fb0  Type: (ffffe0083b769450) SymbolicLink
    ObjectHeader: ffffc00b07628f80 (new version)
    HandleCount: 0  PointerCount: 1
    Directory Object: ffffc00b074166a0  Name: Ip6
    Target String is '\Device\Tdx'
```

### <span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>Additional Information

For information about objects and the object manager, see the Microsoft Windows SDK documentation, the Windows Driver Kit (WDK) documentation, and *Microsoft Windows Internals*, by Mark Russinovich and David Solomon.

## <span id="see_also"></span>See also


[Object Reference Tracing](object-reference-tracing.md)

[**!obtrace**](-obtrace.md)

[**!handle**](-handle.md)

[Determining the ACL of an Object](determining-the-acl-of-an-object.md)

[Kernel-Mode Extension Commands](kernel-mode-extensions.md)

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[debugger\debugger]:%20!object%20%20RELEASE:%20%285/15/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")




