---
title: MS\_SMHBA\_SAS\_ポート WMI クラス
description: MS\_SMHBA\_SAS\_ポート WMI クラス
ms.assetid: d3528212-f884-4db8-aadc-eb4ca15814da
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a8ae3e75fbf04d6c323dd57624f7d8e530b30185
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844527"
---
# <a name="ms_smhba_sas_port-wmi-class"></a>MS\_SMHBA\_SAS\_ポート WMI クラス


Storage Management API をサポートする HBA ミニポートドライバーは、MS\_SMHBA\_SAS\_Port クラスを使用して、SAS ポートに関連付けられている属性を公開します。 各ポートには、このクラスのインスタンスが1つ存在する必要があります。

MS\_SMHBA\_SAS\_Port クラスは、 *Hbaapi*の次のように定義されています。

```cpp
class MS_SMHBA_SAS_Port 
{
    [HBAType("HBA_SASPORTPROTOCOL"), WmiDataId(1)]
    uint32  PortProtocol;

    [HBAType("HBA_WWN"), WmiDataId(2)]
    uint8   LocalSASAddress[8];

    [HBAType("HBA_WWN"), WmiDataId(3)]
    uint8   AttachedSASAddress[8];

    [WmiDataId(4)]
    uint32  NumberofDiscoveredPorts;

    [WmiDataId(5)]
    uint32  NumberofPhys;
};
```

このクラス定義が WMI ツールスイートによってコンパイルされると、次のデータ構造が生成されます。

[**MS\_SMHBA\_SAS\_ポート**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_ms_smhba_sas_port)

この WMI クラスに関連付けられているメソッドはありません。

 

 





