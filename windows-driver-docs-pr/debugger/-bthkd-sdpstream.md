---
title: bthkd.sdpstream
description: The bthkd.sdpstream command displays the contents of a SDP stream.
ms.assetid: 238A10D2-1DAB-4826-AE60-1FD69B0ABABC
keywords: ["bthkd.sdpstream Windows Debugging"]
ms.author: windowsdriverdev
ms.date: 05/23/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
topic_type:
- apiref
api_name:
- bthkd.sdpstream
api_type:
- NA
---

# !bthkd.sdpstream


The **!bthkd.sdpstream** command displays the contents of a SDP stream.

``` syntax
!bthkd.sdpstream streamaddr streamlength
```

## <span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>Parameters


<span id="_______streamaddr______"></span><span id="_______STREAMADDR______"></span> *streamaddr*   
A pointer to beginning of stream.

<span id="_______streamlength______"></span><span id="_______STREAMLENGTH______"></span> *streamlength*   
The length of SDP stream in bytes to display.

## <span id="DLL"></span><span id="dll"></span>DLL


Bthkd.dll

## <span id="see_also"></span>See also


[Bluetooth Extensions (Bthkd.dll)](bluetooh-extensions--bthkd-dll-.md)

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[debugger\debugger]:%20!bthkd.sdpstream%20%20RELEASE:%20%285/15/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")





