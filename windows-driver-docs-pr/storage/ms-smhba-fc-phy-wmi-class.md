---
title: MS\_SMHBA\_FC\_PHY WMI クラス
description: MS\_SMHBA\_FC\_PHY WMI クラス
ms.assetid: 8256eb6a-511f-4954-875e-755bd2bb3d65
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 2c547d1132febbce0f215c65fdae8cf4f03bf46c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386135"
---
# <a name="mssmhbafcphy-wmi-class"></a>MS\_SMHBA\_FC\_PHY WMI クラス


記憶域管理 API をサポートする HBA ミニポート ドライバーは、MS を使用して\_SMHBA\_FC\_PHY クラスに関連付けられている FC ポートの物理属性を公開します。 このクラスの各ポートの 1 つのインスタンスが必要です。

MS\_SMHBA\_FC\_PHY クラスが次のように定義されている*Hbaapi.mof*:

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

このクラスの定義が WMI ツール スイートによってコンパイルされると、次のデータ構造が生成されます。

[**MS\_SMHBA\_FC\_PHY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_ms_smhba_fc_phy)

この WMI クラスに関連付けられているメソッドはありません。

 

 





