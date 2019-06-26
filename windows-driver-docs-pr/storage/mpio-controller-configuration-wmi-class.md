---
title: MPIO\_コント ローラー\_構成 WMI クラス
description: MPIO\_コント ローラー\_構成 WMI クラス
ms.assetid: c11429d6-b016-464e-a7b4-03b6cdc8ddb7
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: c985641613154c1d837bed6600b9d159492330af
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386177"
---
# <a name="mpiocontrollerconfiguration-wmi-class"></a>MPIO\_コント ローラー\_構成 WMI クラス


WMI クライアントが、MPIO を使用して\_コント ローラー\_システムに関連付けられている記憶域コント ローラーに関する情報を照会 MPIO の構成の WMI クラスです。

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

このクラスの定義が WMI ツール スイートによってコンパイルされると、生成、 [ **MPIO\_コント ローラー\_構成**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mpiowmi/ns-mpiowmi-_mpio_controller_configuration)データ構造体。 この WMI クラスに関連付けられているメソッドはありません。

 

 





