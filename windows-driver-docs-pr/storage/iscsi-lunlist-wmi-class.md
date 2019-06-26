---
title: ISCSI\_LUNList WMI クラス
description: ISCSI\_LUNList WMI クラス
ms.assetid: 2ad0dabe-54b3-4075-966b-491e078f2c8b
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 86e03ce1c8d728c97856355f8fbac608010e2022
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378425"
---
# <a name="iscsilunlist-wmi-class"></a>ISCSI\_LUNList WMI クラス


## <span id="ddk_iscsi_lunlist_wmi_class_kr"></span><span id="DDK_ISCSI_LUNLIST_WMI_CLASS_KR"></span>


ISCSI\_LUNList WMI クラスが、論理ユニットが所属するターゲットの名前と一意に識別する論理 64 ビットの数値にするには、ローカル オペレーティング システムを定義する論理ユニット番号 (LUN) からのマッピングについて説明します単位は、ネットワークのどこかでグローバルに無効です。 このクラスが次のように定義されている*Common.mof*します。

```cpp
class ISCSI_LUNList {
  [WmiDataId(1), description("Target LUN") : amended]
    uint64  TargetLUN;
  [WmiDataId(2), description("OS Scsi bus number target
  is mapped to") : amended]
    uint32  OSLUN;
  [WmiDataId(3), description("Reserved") : amended]
    uint32  Reserved;
};
```

WMI ツールのスイートでは、上記のクラス定義をコンパイルするときに生成、 [ **ISCSI\_LUNList** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/iscsidef/ns-iscsidef-_iscsi_lunlist)データ構造体。

 

 





