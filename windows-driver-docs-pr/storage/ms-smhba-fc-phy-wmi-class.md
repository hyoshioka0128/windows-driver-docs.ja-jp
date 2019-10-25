---
title: MS\_SMHBA\_FC\_PHY WMI クラス
description: MS\_SMHBA\_FC\_PHY WMI クラス
ms.assetid: 8256eb6a-511f-4954-875e-755bd2bb3d65
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f8a03b6970ab4614904340403ffe2c7ec07fa768
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844537"
---
# <a name="ms_smhba_fc_phy-wmi-class"></a>MS\_SMHBA\_FC\_PHY WMI クラス


Storage Management API をサポートする HBA ミニポートドライバーは、MS\_SMHBA\_FC\_PHY クラスを使用して、関連付けられている FC ポートの物理属性を公開します。 各ポートには、このクラスのインスタンスが1つ存在する必要があります。

MS\_SMHBA\_FC\_PHY クラスは、 *Hbaapi .mof*で次のように定義されています。

```cpp
class MS_SMHBA_FC_PHY 
{
    [WmiDataId(1), HBAType("HBA_FCPHYSPEED")]
    uint32  PhySupportSpeed;

    [WmiDataId(2), HBAType("HBA_FCPHYSPEED")]
    uint32  PhySpeed;      

    [WmiDataId(3), HBAType("HBA_FCPHYTYPE")]
    uint8   PhyType;

    [WmiDataId(4)]
    uint32  MaxFrameSize; 
};
```

このクラス定義が WMI ツールスイートによってコンパイルされると、次のデータ構造が生成されます。

[**MS\_SMHBA\_FC\_PHY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_ms_smhba_fc_phy)

この WMI クラスに関連付けられているメソッドはありません。

 

 





