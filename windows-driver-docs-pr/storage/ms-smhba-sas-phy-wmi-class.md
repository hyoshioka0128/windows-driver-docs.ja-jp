---
title: MS\_SMHBA\_SAS\_PHY WMI クラス
description: MS\_SMHBA\_SAS\_PHY WMI クラス
ms.assetid: c4fcf9ae-d2ab-4791-bf1e-55087fe03185
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 8b14290d44da932bdbed6346367693fad23da550
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386128"
---
# <a name="mssmhbasasphy-wmi-class"></a>MS\_SMHBA\_SAS\_PHY WMI クラス


記憶域管理 API をサポートする HBA ミニポート ドライバーは、MS を使用して\_SMHBA\_SAS\_PHY クラスに関連付けられた SAS ポートの物理属性を公開します。 このクラスの各ポートの 1 つのインスタンスが必要です。

MS\_SMHBA\_SAS\_PHY クラスが次のように定義されている*Hbaapi.mof*:

```cpp
class MS_SMHBA_SAS_PHY
{
    [WmiDataId(1)]
    uint8   PhyIdentifier;

    [WmiDataId(2), HBAType("HBA_SASPHYSPEED")]
    uint32  NegotiatedLinkRate;

    [WmiDataId(3), HBAType("HBA_SASPHYSPEED")]
    uint32  ProgrammedMinLinkRate;

    [WmiDataId(4), HBAType("HBA_SASPHYSPEED")]
    uint32  HardwareMinLinkRate;

    [WmiDataId(5), HBAType("HBA_SASPHYSPEED")]
    uint32  ProgrammedMaxLinkRate;

    [WmiDataId(6), HBAType("HBA_SASPHYSPEED")]
    uint32  HardwareMaxLinkRate;

    [WmiDataId(7), HBAType("HBA_WWN") ]
    uint8   domainPortWWN[8];
};
```

このクラスの定義が WMI ツール スイートによってコンパイルされると、次のデータ構造が生成されます。

[**MS\_SMHBA\_SAS\_PHY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_ms_smhba_sas_phy)

この WMI クラスに関連付けられているメソッドはありません。

 

 





