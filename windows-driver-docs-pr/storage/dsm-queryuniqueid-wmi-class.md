---
title: DSM\_QueryUniqueId WMI クラス
description: DSM\_QueryUniqueId WMI クラス
ms.assetid: 576e208d-972c-47ba-ab30-a05bf3d0943d
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a747abe604f7c7030e82e5ff1ecd9a2a3fd2bff9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380662"
---
# <a name="dsmqueryuniqueid-wmi-class"></a>DSM\_QueryUniqueId WMI クラス


MPIO DSM の発行\_QueryUniqueId WMI クラスには、GUID を登録して、その実装を処理する DSM が必要です。 DSM を使用する WMI クライアント\_QueryUniqueId WMI クラス パスの一意の識別子を照会します。

```cpp
class DSM_QueryUniqueId
{

    [key, read]
    string InstanceName;

    [read]
    boolean Active;

    //
    // This Identifier needs to be set by DSMs that want management applications
    // like VDS to be able to manage the devices controlled by the particular DSM.
    // This DsmUniqueId will be used in conjuction with the DsmPathId to construct
    // a path identitifer that is unique not just among all paths known to this DSM,
    // but also among all the DSMs present on the system.
    //
    [WmiDataId(1),
     DisplayName("DSM Unique Identifier") : amended,
     Description("DSM Unique Identifier to be used by a management application") : amended
    ]
    uint64 DsmUniqueId;
};
```

このクラスの定義が WMI ツール スイートによってコンパイルされると、生成、 [ **DSM\_QueryUniqueId** ](https://msdn.microsoft.com/library/windows/hardware/ff552742)データ構造体。 この WMI クラスに関連付けられているメソッドはありません。

 

 





