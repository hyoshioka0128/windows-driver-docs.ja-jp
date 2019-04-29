---
title: MS\_SMHBA\_SAS\_Port WMI クラス
description: MS\_SMHBA\_SAS\_Port WMI クラス
ms.assetid: d3528212-f884-4db8-aadc-eb4ca15814da
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 170483796e69491975bb9211fb83ed3f1a93b70a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325298"
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

[**MS\_SMHBA\_SAS\_Port**](https://msdn.microsoft.com/library/windows/hardware/ff563186)

この WMI クラスに関連付けられているメソッドはありません。

 

 





