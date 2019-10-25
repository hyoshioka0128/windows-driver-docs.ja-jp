---
title: PDOSCSI\_ADDR WMI クラス
description: PDOSCSI\_ADDR WMI クラス
ms.assetid: 8fdcfc5a-308a-457f-a015-e082e96f9df7
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 99006f6a85f0561423cd8292501c532b13810531
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842730"
---
# <a name="pdoscsi_addr-wmi-class"></a>PDOSCSI\_ADDR WMI クラス


MPIO ドライバーは、PDOSCSI\_ADDR WMI クラスを使用して、物理デバイスの SCSI アドレスを識別します。

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

このクラス定義が WMI ツールスイートによってコンパイルされると、 [**PDOSCSI\_ADDR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mpiodisk/ns-mpiodisk-_pdoscsi_addr)データ構造が生成されます。 この WMI クラスに関連付けられているメソッドはありません。

 

 





