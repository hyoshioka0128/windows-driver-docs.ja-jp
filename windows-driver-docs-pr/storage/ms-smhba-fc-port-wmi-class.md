---
title: MS\_SMHBA\_FC\_ポート WMI クラス
description: MS\_SMHBA\_FC\_ポート WMI クラス
ms.assetid: 671f14e4-c591-4df2-85a1-2db3f802ef5e
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f1bc67601fcca2b7567e7d3800e767f9916f8a2b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844535"
---
# <a name="ms_smhba_fc_port-wmi-class"></a>MS\_SMHBA\_FC\_ポート WMI クラス


Storage Management API をサポートする HBA ミニポートドライバーは、MS\_SMHBA\_FC\_Port クラスを使用して、関連付けられている FC アダプターのポート属性を公開します。 各ポートには、このクラスのインスタンスが1つ存在する必要があります。

MS\_SMHBA\_FC\_Port クラスは、 *Hbaapi. mof*で次のように定義されています。

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

このクラス定義が WMI ツールスイートによってコンパイルされると、次のデータ構造が生成されます。

[**MS\_SMHBA\_FC\_ポート**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_ms_smhba_fc_port)

この WMI クラスに関連付けられているメソッドはありません。

 

 





