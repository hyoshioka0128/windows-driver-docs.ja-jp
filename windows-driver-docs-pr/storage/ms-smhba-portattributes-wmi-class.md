---
title: MS\_SMHBA\_PORTATTRIBUTES WMI クラス
description: MS\_SMHBA\_PORTATTRIBUTES WMI クラス
ms.assetid: 26f17443-cb89-4c93-9b67-35acb75b6d03
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: cd06c0dc605a2adc429b4bae37494a2627597b55
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844533"
---
# <a name="ms_smhba_portattributes-wmi-class"></a>MS\_SMHBA\_PORTATTRIBUTES WMI クラス


Storage Management API をサポートする HBA ミニポートドライバーは、MS\_SMHBA\_PORTATTRIBUTES クラスを使用してポート属性を公開します。 各ポートには、このクラスのインスタンスが1つ存在する必要があります。

MS\_SMHBA\_PORTATTRIBUTES クラスは、 *Hbaapi .mof*で次のように定義されています。

```cpp
class MS_SMHBA_PORTATTRIBUTES 
{
    [HBA_PORTTYPE_QUALIFIERS, WmiDataId(1)]
    uint32 PortType;

    [HBA_PORTSTATE_QUALIFIERS, WmiDataId(2)]
    uint32 PortState;

    [WmiDataId(3),
     Description("Size of MS_SMHBA_SAS_Port or MS_SMHBA_FC_Port")
    ]
    uint32 PortSpecificAttributesSize;

    [MaxLen(256), WmiDataId(4)]
    string OSDeviceName;

    [WmiDataId(5)]
    uint64 Reserved;

    [WmiDataId(6),
     Description(" MS_SMHBA_SAS_Port or MS_SMHBA_FC_Port Buffer"),
     WmiSizeIs("PortSpecificAttributesSize")
    ]
    uint8 PortSpecificAttributes[];
};
```

このクラス定義が WMI ツールスイートによってコンパイルされると、次のデータ構造が生成されます。

[**MS\_SMHBA\_PORTATTRIBUTES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_ms_smhba_portattributes)

この WMI クラスに関連付けられているメソッドはありません。

 

 





