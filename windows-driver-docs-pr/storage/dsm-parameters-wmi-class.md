---
title: DSM\_パラメーター WMI クラス
description: DSM\_パラメーター WMI クラス
ms.assetid: c946f8cb-327c-4d5a-a133-0051a405fcad
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 418fd4df986cbde09e9f20b85434c1d09553911b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368244"
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

このクラスの定義が WMI ツール スイートによってコンパイルされると、生成、 [ **DSM\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mpiowmi/ns-mpiowmi-_dsm_parameters)データ構造体。 この WMI クラスに関連付けられているメソッドはありません。

 

 





