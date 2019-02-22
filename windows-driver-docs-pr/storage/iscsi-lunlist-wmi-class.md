---
title: ISCSI\_LUNList WMI クラス
description: ISCSI\_LUNList WMI クラス
ms.assetid: 2ad0dabe-54b3-4075-966b-491e078f2c8b
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 56318f4eea7591a5ae01d56369c470470dac6349
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552993"
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

WMI ツールのスイートでは、上記のクラス定義をコンパイルするときに生成、 [ **ISCSI\_LUNList** ](https://msdn.microsoft.com/library/windows/hardware/ff561544)データ構造体。

 

 





