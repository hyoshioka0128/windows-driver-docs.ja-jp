---
title: DSM\_パラメーター WMI クラス
description: DSM\_パラメーター WMI クラス
ms.assetid: c946f8cb-327c-4d5a-a133-0051a405fcad
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f3fc0f478f369302520f5b861b3ad19d24d12ea7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380669"
---
# <a name="dsmparameters-wmi-class"></a>DSM\_パラメーター WMI クラス


MPIO ドライバー ユーザー DSM\_DSM とそのすべての関連付けられているタイマー値を識別するパラメーターの WMI クラスです。

```cpp
class DSM_PARAMETERS
{
    //
    // Friendly name of the registered DSM.
    //
    [WmiDataId(1), MaxLen(63)] string DsmName;

    //
    // DSM-unique handle.
    //
    [WmiDataId(2)] uint64 DsmContext;

    //
    // Version Info
    //
    [WmiDataId(3)] DSM_VERSION DsmVersion;

    //
    // Counters Info
    //
    [WmiDataId(4)] DSM_COUNTERS DsmCounters;
};
```

このクラスの定義が WMI ツール スイートによってコンパイルされると、生成、 [ **DSM\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff552713)データ構造体。 この WMI クラスに関連付けられているメソッドはありません。

 

 





