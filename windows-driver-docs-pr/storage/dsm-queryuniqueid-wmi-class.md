---
title: DSM\_QueryUniqueId WMI クラス
description: DSM\_QueryUniqueId WMI クラス
ms.assetid: 576e208d-972c-47ba-ab30-a05bf3d0943d
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 3140d6937469eb4f68bd827a3d8f49ea5e7bdad5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373224"
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

このクラスの定義が WMI ツール スイートによってコンパイルされると、生成、 [ **DSM\_QueryUniqueId** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mpiodisk/ns-mpiodisk-_dsm_queryuniqueid)データ構造体。 この WMI クラスに関連付けられているメソッドはありません。

 

 





