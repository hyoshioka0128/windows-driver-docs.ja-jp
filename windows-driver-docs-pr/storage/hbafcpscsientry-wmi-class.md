---
title: HBAFCPScsiEntry WMI クラス
description: HBAFCPScsiEntry WMI クラス
ms.assetid: b20b1e07-38b4-47b0-a870-51e0865fd256
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 1b32ed1fae4a96c40c5ded2a8bb6bf2393b393ad
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842524"
---
# <a name="hbafcpscsientry-wmi-class"></a>HBAFCPScsiEntry WMI クラス


## <span id="ddk_hbafcpscsientry_wmi_class_kr"></span><span id="DDK_HBAFCPSCSIENTRY_WMI_CLASS_KR"></span>


T11 委員会の*ファイバーチャネル HBA API*仕様をサポートする hba ミニポートドライバーは、HBAFCPScsiEntry クラスを使用して、SCSI 論理ユニットとそのアダプターを一意に識別するオペレーティングシステムによって生成された情報を格納します。 このクラスは、オペレーティングシステム情報と、論理ユニットの FCP 識別子との間のバインドを構築するために使用されます。 このバインディングの詳細については、「 [**Hbafcpbindingentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_hbafcpbindingentry)」を参照してください。 ファイバーチャネルプロトコルの詳細については、「SCSI 仕様」の「T11 委員会の*Dpans ファイバーチャネルプロトコル*」を参照してください。

HBAFCPScsiEntry クラスは、 *Hbaapi .mof*で次のように定義されています。

```cpp
class HBAFCPScsiEntry {
  [HBAType("HBA_FCPID"), WmiDataId(1)] HBAFCPID  FCPId;
  [HBAType("HBA_LUID"), WmiDataId(2)] uint8  Luid[256];
  [HBAType("HBA_SCSIID"), WmiDataId(3)] HBAScsiID  ScsiId;
};
```

WMI ツールスイートによってコンパイルされた場合、このクラス定義では次のデータ構造が生成されます。

[**HBAFCPScsiEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_hbafcpscsientry)

この WMI クラスに関連付けられているメソッドはありません。

 

 





