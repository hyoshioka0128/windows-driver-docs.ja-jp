---
title: MS\_SMHBA\_BINDINGENTRY WMI クラス
description: MS\_SMHBA\_BINDINGENTRY WMI クラス
ms.assetid: b7b2315f-21db-41a4-8390-3c413cb39f5b
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f9dcb5d829ae0473fb41177da7060d0f66802be1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574638"
---
# <a name="mssmhbabindingentry-wmi-class"></a>MS\_SMHBA\_BINDINGENTRY WMI クラス


記憶域管理 API をサポートする HBA ミニポート ドライバーは、MS を使用して\_SMHBA\_SCSI デバイスを識別するために、オペレーティング システムを使用するデータと SSP のプロトコルの識別子の間のバインド情報を公開する BINDINGENTRY クラスデバイス

MS\_SMHBA\_Hbaapi.mof で BINDINGENTRY クラスは、次のように定義されています。

```cpp
class MS_SMHBA_BINDINGENTRY
{
    [SMHBA_BIND_TYPE_QUALIFIERS, WmiDataId(1)]
    uint32 type;

    [HBAType("MS_SMHBA_PORTLUN"), WmiDataId(2)]
    MS_SMHBA_PORTLUN  PortLun;

    [HBAType("HBA_LUID"), WmiDataId(3)]
    uint8  LUID[256];

    [HBA_STATUS_QUALIFIERS, WmiDataId(4)]
    HBA_STATUS Status;

    [HBAType("HBA_SCSIID"), WmiDataId(5)]
    HBAScsiID ScsiId;
};
```

このクラスの定義が WMI ツール スイートによってコンパイルされると、次のデータ構造が生成されます。

MS\_SMHBA\_BINDINGENTRY hbapiwmi.h に記載します。

この WMI クラスに関連付けられているメソッドはありません。

 

 





