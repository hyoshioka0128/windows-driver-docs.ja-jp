---
title: HBAFCPScsiEntry WMI クラス
description: HBAFCPScsiEntry WMI クラス
ms.assetid: b20b1e07-38b4-47b0-a870-51e0865fd256
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 1922e4454e52ccff899fb8ae9bfefb7246b3cbca
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353503"
---
# <a name="hbafcpscsientry-wmi-class"></a>HBAFCPScsiEntry WMI クラス


## <span id="ddk_hbafcpscsientry_wmi_class_kr"></span><span id="DDK_HBAFCPSCSIENTRY_WMI_CLASS_KR"></span>


T11 委員会をサポートする HBA ミニポート ドライバー*ファイバー チャネル HBA API*仕様では、HBAFCPScsiEntry クラスを使用して、SCSI 論理ユニットを一意に識別するオペレーティング システムによって生成される情報を格納し、そのアダプター。 このクラスは、論理ユニットのオペレーティング システムの情報と FCP 識別子間のバインディングを構築に使用されます。 このバインディングの詳細については、次を参照してください。 [ **HBAFCPBindingEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_hbafcpbindingentry)します。 ファイバー チャネル プロトコルの詳細については、T11 委員会を参照してください。 *dpANS scsi、ファイバー チャネル プロトコル*仕様。

HBAFCPScsiEntry クラスは次のように定義されている*Hbaapi.mof*:

```cpp
class HBAFCPScsiEntry {
  [HBAType("HBA_FCPID"), WmiDataId(1)] HBAFCPID  FCPId;
  [HBAType("HBA_LUID"), WmiDataId(2)] uint8  Luid[256];
  [HBAType("HBA_SCSIID"), WmiDataId(3)] HBAScsiID  ScsiId;
};
```

WMI ツール スイートによってコンパイルされるときに、このクラスの定義には、次のデータ構造が生成されます。

[**HBAFCPScsiEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_hbafcpscsientry)

この WMI クラスに関連付けられているメソッドはありません。

 

 





