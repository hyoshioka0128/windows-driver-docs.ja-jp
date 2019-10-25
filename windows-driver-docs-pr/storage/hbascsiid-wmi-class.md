---
title: HBAScsiID WMI クラス
description: HBAScsiID WMI クラス
ms.assetid: ca2ebe3f-bc0b-4723-8dff-00478d9baac3
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 194af2ea0d3d7297fb7d74933ed3813c74d384f0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72823800"
---
# <a name="hbascsiid-wmi-class"></a>HBAScsiID WMI クラス


## <span id="ddk_hbascsiid_wmi_class_kr"></span><span id="DDK_HBASCSIID_WMI_CLASS_KR"></span>


T11 委員会の*ファイバーチャネル HBA API*仕様をサポートする hba ミニポートドライバーは、HBAScsiID クラスを使用して、オペレーティングシステムのデバイス名とその SCSI 情報を使用して論理ユニットを識別します。

HBAScsiID クラスは、Hbaapi .mof で次のように定義されています。

```cpp
class HBAScsiID { 
  [WmiDataId(1)] uint32  ScsiBusNumber;
  [WmiDataId(2)] uint32  ScsiTargetNumber;
  [WmiDataId(3)] uint32  ScsiOSLun;
  [WmiDataId(4),MAX(257)] uint16  OSDeviceName[];
};
```

WMI ツールスイートによってコンパイルされた場合、このクラス定義では次のデータ構造が生成されます。

[**HBAScsiID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_hbascsiid)

この WMI クラスに関連付けられているメソッドはありません。

 

 





