---
title: MS\_SMHBA\_FC\_Port WMI クラス
description: MS\_SMHBA\_FC\_Port WMI クラス
ms.assetid: 671f14e4-c591-4df2-85a1-2db3f802ef5e
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a280e8c66722218b200801cd16aed55ec87d8b46
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386133"
---
# <a name="mssmhbafcport-wmi-class"></a>MS\_SMHBA\_FC\_Port WMI クラス


記憶域管理 API をサポートする HBA ミニポート ドライバーは、MS を使用して\_SMHBA\_FC\_ポートに関連付けられている FC アダプターのポート属性を公開するクラス。 このクラスの各ポートの 1 つのインスタンスが必要です。

MS\_SMHBA\_FC\_ポート クラスが次のように定義されている*Hbaapi.mof*:

```cpp
class MS_SMHBA_FC_Port 
{
    [HBAType("HBA_WWN"), WmiDataId(1)]
    uint8   NodeWWN[8];

    [HBAType("HBA_WWN"), WmiDataId(2)]
    uint8   PortWWN[8];

    [WmiDataId(3)]
    uint32  FcId;

    [HBAType("HBA_COS"), WmiDataId(4)]
    uint32  PortSupportedClassofService;

    [HBAType("HBA_FC4TYPES"), WmiDataId(5)]
    uint8   PortSupportedFc4Types[32];

    [HBAType("HBA_FC4TYPES"), WmiDataId(6)]
    uint8   PortActiveFc4Types[32];

    [HBAType("HBA_WWN"), WmiDataId(7)]
    uint8   FabricName[8];

    [WmiDataId(8)]
    uint32  NumberofDiscoveredPorts;

    [WmiDataId(9)] 
    uint8   NumberofPhys;

    [MaxLen(256), WmiDataId(10)]
    string  PortSymbolicName;
};
```

このクラスの定義が WMI ツール スイートによってコンパイルされると、次のデータ構造が生成されます。

[**MS\_SMHBA\_FC\_ポート**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_ms_smhba_fc_port)

この WMI クラスに関連付けられているメソッドはありません。

 

 





