---
title: MS\_SMHBA\_FC\_Port WMI クラス
description: MS\_SMHBA\_FC\_Port WMI クラス
ms.assetid: 671f14e4-c591-4df2-85a1-2db3f802ef5e
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 1149f715e6818d3f05e983d128a85c7438fe733c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380243"
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

[**MS\_SMHBA\_FC\_ポート**](https://msdn.microsoft.com/library/windows/hardware/ff563162)

この WMI クラスに関連付けられているメソッドはありません。

 

 





