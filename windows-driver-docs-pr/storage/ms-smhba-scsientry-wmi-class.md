---
title: MS\_SMHBA\_SCSIENTRY WMI クラス
description: MS\_SMHBA\_SCSIENTRY WMI クラス
ms.assetid: 8ac7a979-b3fe-4da6-a8e7-301c64b27e46
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 156cb6df94d09edf9e531b759e3e7bad996e6365
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844521"
---
# <a name="ms_smhba_scsientry-wmi-class"></a>MS\_SMHBA\_SCSIENTRY WMI クラス


記憶域管理 API をサポートする HBA ミニポートドライバーは、MS\_SMHBA\_SCSIENTRY クラスを使用して、SCSI 論理ユニットとそのアダプターを一意に識別するオペレーティングシステムによって生成される情報を格納します。 このクラスは、オペレーティングシステム情報と、論理ユニットの SSP 識別子との間のバインドを構築するために使用されます。

MS\_SMHBA\_SCSIENTRY クラスは、 *Hbaapi .mof*で次のように定義されています。

```cpp
class MS_SMHBA_SCSIENTRY
{
    [HBAType("MS_SMHBA_PORTLUN"), WmiDataId(1)]
    MS_SMHBA_PORTLUN PortLun;

    [HBAType("HBA_LUID"), WmiDataId(2)]
    uint8  LUID[256];

    [HBAType("HBA_SCSIID"), WmiDataId(3)]
    HBAScsiID ScsiId;
};
```

このクラス定義が WMI ツールスイートによってコンパイルされると、次のデータ構造が生成されます。

[**MS\_SMHBA\_SCSIENTRY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_ms_smhba_scsientry)

この WMI クラスに関連付けられているメソッドはありません。

 

 





