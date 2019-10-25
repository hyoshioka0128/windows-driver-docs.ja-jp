---
title: DSM\_QueryUniqueId WMI クラス
description: DSM\_QueryUniqueId WMI クラス
ms.assetid: 576e208d-972c-47ba-ab30-a05bf3d0943d
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 21adc61357acf597e1b98677063e6f82856b76ba
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844563"
---
# <a name="dsm_queryuniqueid-wmi-class"></a>DSM\_QueryUniqueId WMI クラス


MPIO は、DSM\_QueryUniqueId WMI クラスを発行しますが、DSM が GUID を登録し、その実装を処理することを想定しています。 WMI クライアントは、DSM\_QueryUniqueId WMI クラスを使用して、パスの一意の識別子を照会します。

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

このクラス定義が WMI ツールスイートによってコンパイルされると、 [**DSM\_QueryUniqueId**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mpiodisk/ns-mpiodisk-_dsm_queryuniqueid)データ構造が生成されます。 この WMI クラスに関連付けられているメソッドはありません。

 

 





