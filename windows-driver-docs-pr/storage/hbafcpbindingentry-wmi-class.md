---
title: HBAFCPBindingEntry WMI クラス
description: HBAFCPBindingEntry WMI クラス
ms.assetid: 58993d0d-2044-430d-b8f6-5ea3b68d460b
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f41288392d17d8e8f78775a76a2ed0ad5f6de83a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353498"
---
# <a name="hbafcpbindingentry-wmi-class"></a>HBAFCPBindingEntry WMI クラス


## <span id="ddk_hbafcpbindingentry_wmi_class_kr"></span><span id="DDK_HBAFCPBINDINGENTRY_WMI_CLASS_KR"></span>


T11 委員会をサポートする HBA ミニポート ドライバー*ファイバー チャネル HBA API*仕様では、HBAFCPBindingEntry クラスを使用して、オペレーティング システムが SCSI デバイスを識別するために使用する情報の間のバインドを定義し、ファイバー チャネル プロトコル (FCP) は、デバイスの識別子。 ファイバー チャネル プロトコルの詳細については、T11 委員会を参照してください。 *dpANS scsi、ファイバー チャネル プロトコル*仕様。 論理ユニットを識別するオペレーティング システムのデータと FCP id の間には、このバインディングの詳細については、T11 委員会を参照してください。*ファイバー チャネル HBA API*仕様。

HBAFCPBindingEntry クラスは次のように定義されている*Hbaapi.mof*:

```cpp
class HBAFCPBindingEntry {
  [HBAType("HBA_FCPBINDINGTYPE"),
    Values{"TO_D_ID", "TO_WWN", "TO_OTHER"},
    ValueMap{"0", "1", "2"},
    WmiDataId(1)] uint32  Type;
  [HBAType("HBA_FCPSCSIENTRY"), WmiDataId(3)] HBAScsiID  ScsiId;
  [HBAType("HBA_FCID"), WmiDataId(2)] HBAFCPID  FCPId;
};
```

WMI ツール スイートによってコンパイルされるときに、このクラスの定義には、次のデータ構造が生成されます。

[**HBAFCPBindingEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_hbafcpbindingentry)

この WMI クラスに関連付けられているメソッドはありません。

 

 





