---
title: PDO\_情報 WMI クラス
description: PDO\_情報 WMI クラス
ms.assetid: 1a972905-42ea-4cb2-b937-5ed0f287d80a
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 30d92578d1ae17a72b5735647537ea50005f95d3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580804"
---
# <a name="pdoinformation-wmi-class"></a>PDO\_情報 WMI クラス


MPIO ドライバーの PDO を使用して\_物理デバイスのデバイスのパスにマッピングを識別する情報の WMI クラスです。

```cpp
class PDO_INFORMATION
{

    [WmiDataId(1)] PDOSCSI_ADDR ScsiAddress;

    //
    // Indicates whether this device-path is usable,
    // i.e. whether DsmIsPathActive returned TRUE for this device-path.
    //
    [WmiDataId(2)] uint32 DeviceState;

    //
    // The PathId matches the identifier returned by DsmSetDeviceInfo.
    //
    [WmiDataId(3)] uint64 PathIdentifier;

    //
    // Matches the MPIO_CONTROLLER_INFO ControllerId of the controller
    // fronting this device.
    //
    [WmiDataId(4)] uint32 IdentifierType;
    [WmiDataId(5)] uint32 IdentifierLength;
    [WmiDataId(6)] uint8 Identifier[32];
    [WmiDataId(7)] uint8 Pad[4];
};
```

このクラスの定義が WMI ツール スイートによってコンパイルされると、生成、 [ **PDO\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff563828)データ構造体。 この WMI クラスに関連付けられているメソッドはありません。

 

 





