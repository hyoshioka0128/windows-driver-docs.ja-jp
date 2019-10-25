---
title: MPIO\_コントローラー\_情報 WMI クラス
description: MPIO\_コントローラー\_情報 WMI クラス
ms.assetid: 0448e056-2bbe-4e4f-a729-a872393222e5
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f272fccb05fb5599b4e24c82f295d55f1adfbddd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844545"
---
# <a name="mpio_controller_info-wmi-class"></a>MPIO\_コントローラー\_情報 WMI クラス


Mpio ドライバーは、MPIO\_CONTROLLER\_INFO WMI クラスを使用して、記憶域コントローラーとそれに関連付けられている DSM を識別します。

```cpp
class MPIO_CONTROLLER_INFO
{

    //
    // Devices behind this controller will have a matching
    // ControllerId in the PDO_INFORMATION class.
    //
    [WmiDataId(1)] uint32 IdentifierType;
    [WmiDataId(2)] uint32 IdentifierLength;
    [WmiDataId(3)] uint8 Identifier[32];
    [WmiDataId(4)] uint32 ControllerState;
    [WmiDataId(5)] uint32 Pad;
    [WmiDataId(6), MaxLen(63)] string AssociatedDsm;
};
```

このクラス定義が WMI ツールスイートによってコンパイルされると、 [**MPIO\_CONTROLLER\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mpiowmi/ns-mpiowmi-_mpio_controller_info)データ構造が生成されます。 この WMI クラスに関連付けられているメソッドはありません。

 

 





