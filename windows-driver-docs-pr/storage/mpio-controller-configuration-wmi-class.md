---
title: MPIO\_コントローラー\_構成 WMI クラス
description: MPIO\_コントローラー\_構成 WMI クラス
ms.assetid: c11429d6-b016-464e-a7b4-03b6cdc8ddb7
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 97129fd9a93995ae47fb9355479b9457e23c8afc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844547"
---
# <a name="mpio_controller_configuration-wmi-class"></a>MPIO\_コントローラー\_構成 WMI クラス


WMI クライアントは、MPIO\_CONTROLLER\_CONFIGURATION WMI クラスを使用して、システムに接続されているストレージコントローラーに関する情報を MPIO に照会します。

```cpp
class MPIO_CONTROLLER_CONFIGURATION
{

    [key, read]
     string InstanceName;
    [read] boolean Active;

    //
    // Number of controllers in the array.
    //
    [WmiDataId(1),
     read,
     Description("Number of Controllers.") : amended
    ] uint32 NumberControllers;

    //
    // Array of each controller's information.
    // Note that these are ULONGLONG aligned.
    //
    [WmiDataId(2),
     read,
     Description("Array of Controller Information Structures.") : amended,
     WmiSizeIs("NumberControllers")
    ] MPIO_CONTROLLER_INFO ControllerInfo[];

};
```

このクラス定義が WMI ツールスイートによってコンパイルされると、 [**MPIO\_CONTROLLER\_構成**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mpiowmi/ns-mpiowmi-_mpio_controller_configuration)データ構造が生成されます。 この WMI クラスに関連付けられているメソッドはありません。

 

 





