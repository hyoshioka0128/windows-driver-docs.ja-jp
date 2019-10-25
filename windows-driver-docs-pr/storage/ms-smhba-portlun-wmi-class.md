---
title: MS\_SMHBA\_PORTLUN WMI クラス
description: MS\_SMHBA\_PORTLUN WMI クラス
ms.assetid: 28473b3b-2b88-4abc-81b5-9a6a7f8166e3
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 8b5140605d22a058d1f29eb053dcf53ecdc0fcce
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844543"
---
# <a name="ms_smhba_portlun-wmi-class"></a>MS\_SMHBA\_PORTLUN WMI クラス


Storage Management API をサポートする HBA ミニポートドライバーは、MS\_SMHBA\_PORTLUN クラスを使用して、ターゲット LUN と SAS アダプター間のマッピングを公開します。

MS\_SMHBA\_PORTLUN クラスは、 *Hbaapi .mof*で次のように定義されています。

```cpp
class MS_SMHBA_PORTLUN 
{
    [HBAType("HBA_WWN"), WmiDataId(1)]
    uint8   PortWWN[8];

    [HBAType("HBA_WWN"), WmiDataId(2)]
    uint8   domainPortWWN[8];

    [HBAType("HBA_SCSILUN"), WmiDataId(3)]
    uint64  TargetLun;
};
```

このクラス定義が WMI ツールスイートによってコンパイルされると、次のデータ構造が生成されます。

[**MS\_SMHBA\_PORTLUN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_ms_smhba_portlun)

この WMI クラスに関連付けられているメソッドはありません。

 

 





