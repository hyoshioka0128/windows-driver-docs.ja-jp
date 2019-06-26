---
title: SCSI\_ADDR WMI クラス
description: SCSI\_ADDR WMI クラス
ms.assetid: 720cf803-b004-4c63-8884-66b0e07d82c0
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 426eaa6a7ec68dae4b86ed79391baf2391244a63
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384329"
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

このクラスの定義が WMI ツール スイートによってコンパイルされると、生成、 [ **SCSI\_ADDR** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mpiowmi/ns-mpiowmi-_scsi_addr)データ構造体。 この WMI クラスに関連付けられているメソッドはありません。

 

 





