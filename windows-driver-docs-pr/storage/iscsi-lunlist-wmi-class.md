---
title: ISCSI\_LUNList WMI クラス
description: ISCSI\_LUNList WMI クラス
ms.assetid: 2ad0dabe-54b3-4075-966b-491e078f2c8b
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: c7ffa1008fd58567021d28d48c28023456b3a5e5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842266"
---
# <a name="iscsi_lunlist-wmi-class"></a>ISCSI\_LUNList WMI クラス


## <span id="ddk_iscsi_lunlist_wmi_class_kr"></span><span id="DDK_ISCSI_LUNLIST_WMI_CLASS_KR"></span>


ISCSI\_LUNList WMI クラスは、論理ユニット番号 (LUN) からのマッピングを記述します。これは、オペレーティングシステムによってローカルで64ビット番号として定義され、論理ユニットが属するターゲットの名前と共に、論理ユニットを一意に識別します。とは、ネットワーク内の任意の場所でグローバルに有効です。 このクラスは、*一般的な .mof*で次のように定義されています。

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

WMI ツールスイートは、前のクラス定義をコンパイルするときに、 [**ISCSI\_LUNList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsidef/ns-iscsidef-_iscsi_lunlist)データ構造を生成します。

 

 





