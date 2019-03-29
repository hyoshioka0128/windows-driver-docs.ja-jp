---
title: MPIO\_コント ローラー\_構成 WMI クラス
description: MPIO\_コント ローラー\_構成 WMI クラス
ms.assetid: c11429d6-b016-464e-a7b4-03b6cdc8ddb7
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 7bdec1e2404d168c8bce660c4808e271ed744d19
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57350291"
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

このクラスの定義が WMI ツール スイートによってコンパイルされると、生成、 [ **MPIO\_コント ローラー\_構成**](https://msdn.microsoft.com/library/windows/hardware/ff562321)データ構造体。 この WMI クラスに関連付けられているメソッドはありません。

 

 





