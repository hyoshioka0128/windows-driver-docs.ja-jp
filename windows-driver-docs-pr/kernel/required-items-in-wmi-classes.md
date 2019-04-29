---
title: WMI のクラスの必須項目
description: WMI のクラスの必須項目
ms.assetid: c978d8d0-5281-481a-b1e5-fd9a57d583d5
keywords:
- WDK の WMI クラス
- WMI の WDK カーネルでは、クラス
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 794cb1bfec53078ab31832c2af6adfa4ecd484b6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324546"
---
# <a name="required-items-in-wmi-classes"></a>WMI のクラスの必須項目





埋め込みクラスは、項目を含める必要がありますを除いて、すべてのクラス定義**InstanceName**と**Active**、正確に示すように表示される必要があります。

```cpp
//WMI class definition
[
    //Class qualifiers
]
ClassName : BaseClassName
{
    [key, read]
     string InstanceName;
    [read] 
     boolean Active;
 
    // Driver-defined data items
}
```

**InstanceName**と**Active**項目が必要なし、WMI によって内部的に使用します。 ドライバーのデータとイベント ブロックの MOF クラスの定義は、これらの項目を含める必要がありますが、ドライバーのデータ ブロックの一部ではないために、データのブロックまたは、イベントを送信するクエリに応答する場合、ドライバーはこれらの項目を設定しない必要があります。

 

 




