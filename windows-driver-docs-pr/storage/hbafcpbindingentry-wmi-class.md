---
title: HBAFCPBindingEntry WMI クラス
description: HBAFCPBindingEntry WMI クラス
ms.assetid: 58993d0d-2044-430d-b8f6-5ea3b68d460b
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 3cc16cb697fa673a08d8d5eef9e066accf44f845
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72823808"
---
# <a name="hbafcpbindingentry-wmi-class"></a>HBAFCPBindingEntry WMI クラス


## <span id="ddk_hbafcpbindingentry_wmi_class_kr"></span><span id="DDK_HBAFCPBINDINGENTRY_WMI_CLASS_KR"></span>


T11 委員会の*ファイバーチャネル HBA API*仕様をサポートする hba ミニポートドライバーは、HBAFCPBindingEntry クラスを使用して、オペレーティングシステムが SCSI デバイスを識別するために使用する情報とのバインドを定義しファイバーチャネルデバイスのプロトコル (FCP) 識別子。 ファイバーチャネルプロトコルの詳細については、「SCSI 仕様」の「T11 委員会の*Dpans ファイバーチャネルプロトコル*」を参照してください。 論理ユニットと FCP 識別子を識別するオペレーティングシステムデータ間のこのバインドの詳細については、「T11 委員会の*ファイバーチャネル HBA API*仕様」を参照してください。

HBAFCPBindingEntry クラスは、 *Hbaapi .mof*で次のように定義されています。

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

WMI ツールスイートによってコンパイルされた場合、このクラス定義では次のデータ構造が生成されます。

[**HBAFCPBindingEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_hbafcpbindingentry)

この WMI クラスに関連付けられているメソッドはありません。

 

 





