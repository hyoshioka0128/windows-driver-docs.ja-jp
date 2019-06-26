---
title: HBAScsiID WMI クラス
description: HBAScsiID WMI クラス
ms.assetid: ca2ebe3f-bc0b-4723-8dff-00478d9baac3
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 781e5e91d9b470e463c55de93078bf62f5e20f93
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385222"
---
# <a name="hbascsiid-wmi-class"></a>HBAScsiID WMI クラス


## <span id="ddk_hbascsiid_wmi_class_kr"></span><span id="DDK_HBASCSIID_WMI_CLASS_KR"></span>


T11 委員会をサポートする HBA ミニポート ドライバー*ファイバー チャネル HBA API*仕様 HBAScsiID クラスを使用してデバイスの名前を使用して論理ユニットを識別するために、オペレーティング システムとの SCSI 情報。

HBAScsiID クラスは、Hbaapi.mof で次のように定義されます。

```cpp
class HBAScsiID { 
  [WmiDataId(1)] uint32  ScsiBusNumber;
  [WmiDataId(2)] uint32  ScsiTargetNumber;
  [WmiDataId(3)] uint32  ScsiOSLun;
  [WmiDataId(4),MAX(257)] uint16  OSDeviceName[];
};
```

WMI ツール スイートによってコンパイルされるときに、このクラスの定義には、次のデータ構造が生成されます。

[**HBAScsiID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_hbascsiid)

この WMI クラスに関連付けられているメソッドはありません。

 

 





