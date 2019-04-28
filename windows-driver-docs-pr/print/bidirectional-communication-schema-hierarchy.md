---
title: 双方向通信のスキーマ履歴
description: 双方向通信のスキーマ履歴
ms.assetid: b3435c17-f72b-4925-8d13-bd3e71b4947e
keywords:
- 双方向通信スキーマ WDK の印刷
- 双方向通信スキーマ WDK の印刷
- WDK の双方向通信の階層
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 17a038643a66fabf8374255195d22fd1ffa909d3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379042"
---
# <a name="bidirectional-communication-schema-hierarchy"></a>双方向通信のスキーマ履歴

双方向通信のスキーマには、次の階層またはツリーのプロパティと値が含まれています。

-   プロパティは、プレーン テキスト (たとえば、DeviceInfo) に表示されます。

-   角かっこで双方向マッピング ファイルから生成されるプロパティが表示されます (たとえば、\[型\])。

-   斜体のテキスト (たとえば、FriendlyName) の値が表示されます。

```cpp
Printer
  DeviceInfo
 FriendlyName
 Manufacturer
 ModelName
 Location
    FirmwareVersion
    IEEE1284DeviceId
    NetworkingInfo
      HostName
      IPAddress
 Comment
  Configuration
    Memory
 Size
 PS
    HardDisk
 Installed
 Capacity
 FreeSpace
    DuplexUnit
 Installed
  Consumables
    [Name]
 Installed
      Type
      Color
      Level
      Model
  Layout
    NumberUp
      PagesPerSheet
 CurrentValue
 Supported
      Direction
 CurrentValue
 Supported
    Orientation
 CurrentValue
 Supported
    Resolution
 CurrentValue
 Supported
    InputBins
      [TrayName]
 Installed
 MediaSize
 MediaType
 MediaColor
 FeedDirection
 Capacity
 Level
  Finishing
 CollationSupported
 JogOffsetSupported
    Staple
 Installed
      Location
 CurrentValue
 Supported
      Angle
 CurrentValue
 Supported
    HolePunch
 Installed
      Pattern
 CurrentValue
 Supported
      Location
 CurrentValue
 Supported
    OutputBins
      [TrayName]
 Installed
 Capacity
 Level
Maintenance
    AlignHead
    CleanHead
Status
    Summary
 State
 StateReason
    Detailed
      Event###
 Name
        Component
 Group
 Name
 Severity
```

 

 




