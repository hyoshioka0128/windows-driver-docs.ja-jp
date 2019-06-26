---
title: HBAFCPBindingEntry2 WMI クラス
description: HBAFCPBindingEntry2 WMI クラス
ms.assetid: b9423b59-1d55-4487-bebb-e3eb786fc1be
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f1b53177172ba9e3ecdc3acdc9a5c05c78dfe001
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353499"
---
# <a name="hbafcpbindingentry2-wmi-class"></a>HBAFCPBindingEntry2 WMI クラス


## <span id="ddk_hbafcpbindingentry2_wmi_class_kr"></span><span id="DDK_HBAFCPBINDINGENTRY2_WMI_CLASS_KR"></span>


T11 委員会をサポートする HBA ミニポート ドライバー*ファイバー チャネル HBA API*仕様では、HBAFCPBindingEntry2 クラスを使用して、論理ユニットを識別するために、オペレーティング システムを使用する情報との間のバインディングを定義します。SCSI デバイスおよび論理ユニットのファイバー チャネル プロトコル (FCP) 識別子。 T11 委員会を参照してください、FCP の詳細については、 *dpANS scsi、ファイバー チャネル プロトコル*仕様。 SCSI と FCP 識別子の間のバインドの詳細については、T11 委員会を参照してください。*ファイバー チャネル HBA API*仕様。

HBAFCPBindingEntry2 クラスは次のように定義されている*Hbaapi.mof*:

```cpp
class HBAFCPBindingEntry2 {
  [WmiDataId(1), HBA_BIND_TYPE_QUALIFIERS] HBA_BIND_TYPE  Type;
  [HBAType("HBA_FCPSCSIENTRY"), WmiDataId(4)] HBAScsiID  ScsiId;
  [HBAType("HBA_FCID"), WmiDataId(2)] HBAFCPID  FCPId;
  [HBAType("HBA_LUID"), WmiDataId(3)] uint8  Luid[256];
};
```

WMI ツール スイートによってコンパイルされるときに、このクラスの定義には、次のデータ構造が生成されます。

[**HBAFCPBindingEntry2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_hbafcpbindingentry2)

この WMI クラスに関連付けられているメソッドはありません。

 

 





