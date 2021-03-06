---
title: MS\_SMHBA\_PORTATTRIBUTES WMI クラス
description: MS\_SMHBA\_PORTATTRIBUTES WMI クラス
ms.assetid: 26f17443-cb89-4c93-9b67-35acb75b6d03
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 6a43e54d1c942ad23b96cd1283a01c0f59c6aeb0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386139"
---
# <a name="mssmhbaportattributes-wmi-class"></a>MS\_SMHBA\_PORTATTRIBUTES WMI クラス


記憶域管理 API をサポートする HBA ミニポート ドライバーは、MS を使用して\_SMHBA\_PORTATTRIBUTES クラスは、ポート属性を公開します。 このクラスの各ポートの 1 つのインスタンスが必要です。

MS\_SMHBA\_PORTATTRIBUTES クラスが次のように定義されている*Hbaapi.mof*:

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

このクラスの定義が WMI ツール スイートによってコンパイルされると、次のデータ構造が生成されます。

[**MS\_SMHBA\_PORTATTRIBUTES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_ms_smhba_portattributes)

この WMI クラスに関連付けられているメソッドはありません。

 

 





