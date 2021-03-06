---
title: Claiming Legacy Resources
description: Claiming Legacy Resources
ms.assetid: f3e573a1-0e7a-422b-8bed-db3ba7712a2f
keywords:
- video miniport drivers WDK Windows 2000 , legacy resources
- legacy resources WDK video miniport
- video miniport drivers WDK Windows 2000 , initializing
- initializing video miniport drivers
- VIDEO_HW_INITIALIZATION_DATA
ms.author: windowsdriverdev
ms.date: 04/20/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
---

# Claiming Legacy Resources


## <span id="ddk_claiming_legacy_resources_gg"></span><span id="DDK_CLAIMING_LEGACY_RESOURCES_GG"></span>


A video miniport driver must claim and report all legacy resources in its [**VIDEO\_HW\_INITIALIZATION\_DATA**](https://msdn.microsoft.com/library/windows/hardware/ff570505) structure during driver initialization. Legacy resources are those resources not listed in the device's PCI configuration space but that are decoded by the device. NT-based operating systems will disable power management and docking when they encounter legacy resources that are not reported in the manner outlined in this section.

Miniport drivers must do the following to report such legacy resources:

-   If the legacy resource list for the device is known at compile time, fill in the following two fields of the [**VIDEO\_HW\_INITIALIZATION\_DATA**](https://msdn.microsoft.com/library/windows/hardware/ff570505) structure that is created and initialized in the [**DriverEntry**](https://msdn.microsoft.com/library/windows/hardware/ff556159) routine:

    <table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th align="left">Structure Member</th>
    <th align="left">Definition</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td align="left"><p><strong>HwLegacyResourceList</strong></p></td>
    <td align="left"><p>Points to an array of [<strong>VIDEO_ACCESS_RANGE</strong>](https://msdn.microsoft.com/library/windows/hardware/ff570498) structures. Each structure describes a device I/O port or memory range for the video adapter that is not listed in PCI configuration space.</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p><strong>HwLegacyResourceCount</strong></p></td>
    <td align="left"><p>Is the number of elements in the array to which <strong>HwLegacyResourceList</strong> points.</p></td>
    </tr>
    </tbody>
    </table>

     

<!-- -->

-   If the legacy resource list for the device is not known at compile time, implement a [*HwVidLegacyResources*](https://msdn.microsoft.com/library/windows/hardware/ff567352) function and initialize the **HwGetLegacyResources** member of VIDEO\_HW\_INITIALIZATION\_DATA to point to this function. For example, a miniport driver that supports two devices with different sets of legacy resources would implement *HwVidLegacyResources* to report the legacy resources at run time. The video port driver will ignore the **HwLegacyResourceList** and **HwLegacyResourceCount** members of VIDEO\_HW\_INITIALIZATION\_DATA when a miniport driver implements *HwVidLegacyResources*.

-   Fill in the **RangePassive** field for each VIDEO\_ACCESS\_RANGE structure defined in the miniport driver accordingly. Setting **RangePassive** to VIDEO\_RANGE\_PASSIVE\_DECODE indicates that the region is decoded by the hardware but that the display and video miniport drivers will never touch it. Setting **RangePassive** to VIDEO\_RANGE\_10\_BIT\_DECODE indicates that the device decodes ten bits of the port address for the region.

Again, a driver should only include resources that the hardware decodes but that are not claimed by PCI. Code in a driver that needs to claim minimal legacy resources might look something like the following:

```
//              RangeStart        RangeLength
//              |                 |      RangeInIoSpace
//              |                 |      |  RangeVisible
//        +-----+-----+           |      |  |  RangeShareable
//       low         high         |      |  |  |  RangePassive
//        v           v           v      v  v  v  v
VIDEO_ACCESS_RANGE AccessRanges[] = {
    // [0] (0x3b0-0x3bb)
    {0x000003b0, 0x00000000, 0x0000000c, 1, 1, 1, 0},
    // [1] (0x3c0-0x3df)
    {0x000003C0, 0x00000000, 0x00000010, 1, 1, 1, 0},
    // [2] (0xa0000-0xaffff)
    {0x000A0000, 0x00000000, 0x00010000, 1, 0, 0, 0},
};
 
// Within the DriverEntry routine:
VIDEO_HW_INITIALIZATION_DATA hwInitData;
hwInitData.HwLegacyResourceList = AccessRanges;
hwInitData.HwLegacyResourceCount = 3;
```

The miniport driver can "reclaim" legacy resources again in subsequent call(s) to [**VideoPortVerifyAccessRanges**](https://msdn.microsoft.com/library/windows/hardware/ff570377); however, the video port driver will just ignore requests for any such previously claimed resources. Power management and docking will be disabled in the system if the miniport driver attempts to claim a legacy access range in **VideoPortVerifyAccessRanges** that was not previously claimed in the **HwLegacyResourceList** during [**DriverEntry**](https://msdn.microsoft.com/library/windows/hardware/ff556159) or returned in the *LegacyResourceList* parameter of [*HwVidLegacyResources*](https://msdn.microsoft.com/library/windows/hardware/ff567352).

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[display\display]:%20Claiming%20Legacy%20Resources%20%20RELEASE:%20%282/10/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")




