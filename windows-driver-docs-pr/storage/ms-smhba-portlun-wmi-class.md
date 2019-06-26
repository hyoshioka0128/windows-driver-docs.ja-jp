---
title: MS\_SMHBA\_PORTLUN WMI クラス
description: MS\_SMHBA\_PORTLUN WMI クラス
ms.assetid: 28473b3b-2b88-4abc-81b5-9a6a7f8166e3
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: d99a4f2e3ad2cd8e98a22610e09f597ef014ed97
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386129"
---
# <a name="mssmhbaportlun-wmi-class"></a>MS\_SMHBA\_PORTLUN WMI クラス


記憶域管理 API をサポートする HBA ミニポート ドライバーは、MS を使用して\_SMHBA\_PORTLUN クラスをターゲット LUN と SAS アダプター間のマッピングを公開します。

MS\_SMHBA\_PORTLUN クラスが次のように定義されている*Hbaapi.mof*:

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

このクラスの定義が WMI ツール スイートによってコンパイルされると、次のデータ構造が生成されます。

[**MS\_SMHBA\_PORTLUN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_ms_smhba_portlun)

この WMI クラスに関連付けられているメソッドはありません。

 

 





