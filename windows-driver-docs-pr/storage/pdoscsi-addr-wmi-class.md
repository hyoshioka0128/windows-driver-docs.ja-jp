---
title: PDOSCSI\_ADDR WMI クラス
description: PDOSCSI\_ADDR WMI クラス
ms.assetid: 8fdcfc5a-308a-457f-a015-e082e96f9df7
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 26957953dcf7a61a925390fffd07c4ede6757eb2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63389420"
---
# <a name="pdoscsiaddr-wmi-class"></a>PDOSCSI\_ADDR WMI クラス


MPIO ドライバーの使用、PDOSCSI\_ADDR WMI クラスは、物理デバイスの SCSI アドレスを識別します。

```cpp
class PDOSCSI_ADDR
{
    //
    // ScsiAddress: Port, Bus, Target, Lun
    //
    [WmiDataId(1)] uint8 PortNumber;
    [WmiDataId(2)] uint8 ScsiPathId;
    [WmiDataId(3)] uint8 TargetId;
    [WmiDataId(4)] uint8 Lun;
};
```

生成が WMI ツールのスイートでクラス定義 iscompiled このとき、 [ **PDOSCSI\_ADDR** ](https://msdn.microsoft.com/library/windows/hardware/ff563809)データ構造体。 この WMI クラスに関連付けられているメソッドはありません。

 

 





