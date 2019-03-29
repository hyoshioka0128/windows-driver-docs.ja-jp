---
title: MS\_SMHBA\_PORTLUN WMI クラス
description: MS\_SMHBA\_PORTLUN WMI クラス
ms.assetid: 28473b3b-2b88-4abc-81b5-9a6a7f8166e3
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 70a07917f4065bad385ff2966d676ddf6a111c7a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574650"
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

[**MS\_SMHBA\_PORTLUN**](https://msdn.microsoft.com/library/windows/hardware/ff563169)

この WMI クラスに関連付けられているメソッドはありません。

 

 





