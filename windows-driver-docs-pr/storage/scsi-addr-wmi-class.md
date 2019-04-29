---
title: SCSI\_ADDR WMI クラス
description: SCSI\_ADDR WMI クラス
ms.assetid: 720cf803-b004-4c63-8884-66b0e07d82c0
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: d50391a3f01b3ad6a3265bb0f3f8af5d8749950a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323377"
---
# <a name="scsiaddr-wmi-class"></a>SCSI\_ADDR WMI クラス


MPIO ドライバーは、SCSI を使用して\_MPIO ディスクの SCSI アドレスを識別する ADDR WMI クラスです。

```cpp
class SCSI_ADDR
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

このクラスの定義が WMI ツール スイートによってコンパイルされると、生成、 [ **SCSI\_ADDR** ](https://msdn.microsoft.com/library/windows/hardware/ff564952)データ構造体。 この WMI クラスに関連付けられているメソッドはありません。

 

 





