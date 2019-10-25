---
title: PDO\_情報 WMI クラス
description: PDO\_情報 WMI クラス
ms.assetid: 1a972905-42ea-4cb2-b937-5ed0f287d80a
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 13c7b63e15eae973caa4d9424cf1957e6bba5172
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842732"
---
# <a name="pdo_information-wmi-class"></a>PDO\_情報 WMI クラス


MPIO ドライバーは、PDO\_INFORMATION WMI クラスを使用して、物理デバイスのデバイスからパスへのマッピングを識別します。

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

このクラス定義が WMI ツールスイートによってコンパイルされると、 [**PDO\_INFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mpiodisk/ns-mpiodisk-_pdo_information)データ構造が生成されます。 この WMI クラスに関連付けられているメソッドはありません。

 

 





