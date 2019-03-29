---
title: ACPI 記述子のサンプル
description: このトピックでには、ACPI 記述子のサンプルが含まれています。
ms.assetid: E091DF59-2E9F-4652-801C-3F55CBB910FE
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 9d1badd6c1aee7326d4584df13203f6bd0eb9d58
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573578"
---
# <a name="acpi-descriptor-samples"></a>ACPI 記述子のサンプル


このトピックでには、ACPI 記述子のサンプルが含まれています。

**注**  (CONV) などのデバイス定義の ACPI 記述子の 4 つの文字の長さを使用します。

 

## <a name="span-idacpidescriptionforbuttonarrayspanspan-idacpidescriptionforbuttonarrayspanspan-idacpidescriptionforbuttonarrayspanacpi-description-for-button-array"></a><span id="ACPI_description_for_button_array"></span><span id="acpi_description_for_button_array"></span><span id="ACPI_DESCRIPTION_FOR_BUTTON_ARRAY"></span>ボタン配列の ACPI 記述


``` syntax
Device(BTT00N)
{
    Method(_HID, 0x0, NotSerialized)
    {
        Return("ID9000")
    }
        Name(_CID, "PNP0C40")
        Name(_CRS, ResourceTemplate()
                {
                GpioInt(Edge, 
                        ActiveLow, 
                        SharedAndWake, 
                        PullDefault, 
                        0, "\\_SB.GPIO", 
                        0, ResourceConsumer, , 
                        RawDataBuffer() {}) 
                 {0xE1}
                GpioInt(Edge, 
                        ActiveBoth, 
                        SharedAndWake, 
                        PullDefault, 
                        0, "\\_SB.GPIO", 
                        0, ResourceConsumer, , 
                        RawDataBuffer() {}) 
                {0xE2}
                GpioInt(Edge, 
                        ActiveBoth, 
                        Exclusive, 
                        PullDefault, 
                        0, "\\_SB.GPIO", 
                        0, ResourceConsumer, , 
                        RawDataBuffer() {}) 
                {0xE3}
                GpioInt(Edge, 
                        ActiveBoth, 
                        Exclusive, 
                        PullDefault, 
                        0, "\\_SB.GPIO", 
                        0, ResourceConsumer, , 
                        RawDataBuffer() {}) 
                {0xE4}
                GpioInt(Edge, 
                        ActiveBoth, 
                        Exclusive, 
                        PullDefault, 
                        0, "\\_SB.GPIO", 
                        0, ResourceConsumer, , 
                        RawDataBuffer() {}) 
                {0xE5}
                })
}
```

## <a name="span-idacpidescriptionforlaptopslatemodeindicatorspanspan-idacpidescriptionforlaptopslatemodeindicatorspanspan-idacpidescriptionforlaptopslatemodeindicatorspanacpi-description-for-laptopslate-mode-indicator"></a><span id="ACPI_description_for_laptop_slate_mode_indicator"></span><span id="acpi_description_for_laptop_slate_mode_indicator"></span><span id="ACPI_DESCRIPTION_FOR_LAPTOP_SLATE_MODE_INDICATOR"></span>ラップトップ/スレート モードのインジケーターの ACPI 記述


``` syntax
Device(CONV)
{
    Method(_HID, 0x0, NotSerialized)
        {
            Return("ID9001")
        }
     Name(_CID, "PNP0C60")
}
```

## <a name="span-idacpidescriptionfordockingmodeindicatorspanspan-idacpidescriptionfordockingmodeindicatorspanspan-idacpidescriptionfordockingmodeindicatorspanacpi-description-for-docking-mode-indicator"></a><span id="ACPI_description_for_docking_mode_indicator"></span><span id="acpi_description_for_docking_mode_indicator"></span><span id="ACPI_DESCRIPTION_FOR_DOCKING_MODE_INDICATOR"></span>ドッキングのモードのインジケーターの ACPI 記述


``` syntax
Device(DOCK)
{
    Method(_HID, 0x0, NotSerialized)
    {
        Return("ID9002")
     }
     Name(_CID, "PNP0C70")
}
```

 

 




