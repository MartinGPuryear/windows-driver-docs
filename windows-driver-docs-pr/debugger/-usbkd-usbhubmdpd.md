---
title: usbkd.usbhubmdpd
description: The usbkd.usbhubmdpd command displays a usbhub \_HUB\_PORT\_DATA structure if one is present in a crash dump that was generated as a result of Bug Check 0xFE.
ms.assetid: 128D45A2-A891-42BC-9E3E-FCDC5B4504A2
keywords: ["usbkd.usbhubmdpd Windows Debugging"]
ms.author: windowsdriverdev
ms.date: 05/23/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
topic_type:
- apiref
api_name:
- usbkd.usbhubmdpd
api_type:
- NA
---

# !usbkd.usbhubmdpd


The **!usbkd.usbhubmdpd** command displays a **usbhub!\_HUB\_PORT\_DATA** structure if one is present in a crash dump that was generated as a result of [**Bug Check 0xFE**](bug-check-0xfe--bugcode-usb-driver.md).

``` syntax
!usbkd.usbhubmdpd [PortNum]
```

## <span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>Parameters


<span id="_______PortNum______"></span><span id="_______portnum______"></span><span id="_______PORTNUM______"></span> *PortNum*   
A USB port number. If you specify a port number, this command displays the structure (if one is present) that represents the specified port. If you do not specify a port number, this command displays the structure (if one is present) on which [**Bug Check 0xFE**](bug-check-0xfe--bugcode-usb-driver.md) was initiated.

## <span id="DLL"></span><span id="dll"></span>DLL


Usbkd.dll

Remarks
-------

Use this command only when you are debugging a crash dump file that was generated as a result of [**Bug Check 0xFE: BUGCODE\_USB\_DRIVER**](bug-check-0xfe--bugcode-usb-driver.md).

## <span id="see_also"></span>See also


[USB 2.0 Debugger Extensions](usb-2-0-extensions.md)

[Universal Serial Bus (USB) Drivers](http://go.microsoft.com/fwlink/p?LinkID=227351)

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[debugger\debugger]:%20!usbkd.usbhubmdpd%20%20RELEASE:%20%285/15/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")





