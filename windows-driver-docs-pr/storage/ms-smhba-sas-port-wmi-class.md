---
title: MS\_SMHBA\_SAS\_Port WMI クラス
description: MS\_SMHBA\_SAS\_Port WMI クラス
ms.assetid: d3528212-f884-4db8-aadc-eb4ca15814da
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: d32fd65f39bf2bd23c3e6f0980f074ce3fef5cd8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386132"
---
# <a name="mssmhbasasport-wmi-class"></a>MS\_SMHBA\_SAS\_Port WMI クラス


記憶域管理 API をサポートする HBA ミニポート ドライバーは、MS を使用して\_SMHBA\_SAS\_ポートの SAS ポートに関連付けられている属性を公開するクラス。 このクラスの各ポートの 1 つのインスタンスが必要です。

MS\_SMHBA\_SAS\_ポート クラスが次のように定義されている*Hbaapi.mof*:

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

このクラスの定義が WMI ツール スイートによってコンパイルされると、次のデータ構造が生成されます。

[**MS\_SMHBA\_SAS\_Port**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_ms_smhba_sas_port)

この WMI クラスに関連付けられているメソッドはありません。

 

 





