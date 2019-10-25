---
title: MS\_SMHBA\_SAS\_PHY WMI クラス
description: MS\_SMHBA\_SAS\_PHY WMI クラス
ms.assetid: c4fcf9ae-d2ab-4791-bf1e-55087fe03185
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a8fceb02d1cf943250552d8136a26d977393dc65
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844529"
---
# <a name="ms_smhba_sas_phy-wmi-class"></a>MS\_SMHBA\_SAS\_PHY WMI クラス


Storage Management API をサポートする HBA ミニポートドライバーは、MS\_SMHBA\_SAS\_PHY クラスを使用して、関連付けられている SAS ポートの物理属性を公開します。 各ポートには、このクラスのインスタンスが1つ存在する必要があります。

MS\_SMHBA\_SAS\_PHY クラスは、 *Hbaapi .mof*で次のように定義されています。

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

このクラス定義が WMI ツールスイートによってコンパイルされると、次のデータ構造が生成されます。

[**MS\_SMHBA\_SAS\_PHY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_ms_smhba_sas_phy)

この WMI クラスに関連付けられているメソッドはありません。

 

 





