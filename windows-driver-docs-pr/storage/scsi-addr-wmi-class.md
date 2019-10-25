---
title: SCSI\_ADDR WMI クラス
description: SCSI\_ADDR WMI クラス
ms.assetid: 720cf803-b004-4c63-8884-66b0e07d82c0
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: b1cdb41bff2866d0eab081d3f4b0cd227738eae5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842682"
---
# <a name="scsi_addr-wmi-class"></a>SCSI\_ADDR WMI クラス


MPIO ドライバーは、SCSI\_ADDR WMI クラスを使用して、MPIO ディスクの SCSI アドレスを識別します。

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

このクラス定義が WMI ツールスイートによってコンパイルされると、 [**SCSI\_ADDR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mpiowmi/ns-mpiowmi-_scsi_addr)データ構造が生成されます。 この WMI クラスに関連付けられているメソッドはありません。

 

 





