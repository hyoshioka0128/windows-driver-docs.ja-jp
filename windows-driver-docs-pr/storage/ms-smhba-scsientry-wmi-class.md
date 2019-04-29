---
title: MS\_SMHBA\_SCSIENTRY WMI クラス
description: MS\_SMHBA\_SCSIENTRY WMI クラス
ms.assetid: 8ac7a979-b3fe-4da6-a8e7-301c64b27e46
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 3273d333ff381fcdd00e2a4788face80c29dcb52
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325239"
---
# <a name="mssmhbascsientry-wmi-class"></a>MS\_SMHBA\_SCSIENTRY WMI クラス


記憶域管理 API をサポートする HBA ミニポート ドライバーは、MS を使用して\_SMHBA\_SCSIENTRY クラス SCSI 論理ユニットとそのアダプターを一意に識別するオペレーティング システムによって生成される情報を格納します。 このクラスは、論理ユニットのオペレーティング システムの情報と、SSP 識別子の間のバインドを構築に使用されます。

MS\_SMHBA\_SCSIENTRY クラスが次のように定義されている*Hbaapi.mof*:

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

このクラスの定義が WMI ツール スイートによってコンパイルされると、次のデータ構造が生成されます。

[**MS\_SMHBA\_SCSIENTRY**](https://msdn.microsoft.com/library/windows/hardware/ff563191)

この WMI クラスに関連付けられているメソッドはありません。

 

 





