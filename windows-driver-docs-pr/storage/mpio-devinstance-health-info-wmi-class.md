---
title: MPIO\_DEVINSTANCE\_ヘルス\_情報 WMI クラス
description: MPIO\_DEVINSTANCE\_ヘルス\_情報 WMI クラス
ms.assetid: 4d47b41b-eac6-4f8b-801b-76eec8158074
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 9307fe6cb3cbef5b9a98b7333713e21c21d118f8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391427"
---
# <a name="mpiodevinstancehealthinfo-wmi-class"></a>MPIO\_DEVINSTANCE\_ヘルス\_情報 WMI クラス


MPIO ドライバーは、MPIO を使用して\_DEVINSTANCE\_正常性\_情報 WMI クラスを別のパスを基になるを使用して MPIO ディスクの正常性の統計情報を報告します。

```cpp
class MPIO_DEVINSTANCE_HEALTH_INFO
{
    [key, read]
     string InstanceName;
    [read] boolean Active;

    [WmiDataId(1),
     read,
     Description("Number of Health Packets.") : amended
    ] uint32 NumberDevInstancePackets;

    [WmiDataId(2),
     read,
     Description("Reserved for future use.") : amended
    ] uint32 Reserved;

    [WmiDataId(3),
     read,
     Description("Multi-Path Health Info Array.") : amended,
     WmiSizeIs("NumberDevInstancePackets")
    ] MPIO_DEVINSTANCE_HEALTH_CLASS DevInstanceHealthPackets[];
};
```

このクラスの定義が WMI ツール スイートによってコンパイルされると、生成、 [ **MPIO\_DEVINSTANCE\_正常性\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff562343)データ構造体。 この WMI クラスに関連付けられているメソッドはありません。

 

 





