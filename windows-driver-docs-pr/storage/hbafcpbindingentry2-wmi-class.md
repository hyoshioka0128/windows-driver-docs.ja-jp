---
title: HBAFCPBindingEntry2 WMI クラス
description: HBAFCPBindingEntry2 WMI クラス
ms.assetid: b9423b59-1d55-4487-bebb-e3eb786fc1be
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: b222dd737c0213c96320535bb8dc19681b208d30
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842745"
---
# <a name="hbafcpbindingentry2-wmi-class"></a>HBAFCPBindingEntry2 WMI クラス


## <span id="ddk_hbafcpbindingentry2_wmi_class_kr"></span><span id="DDK_HBAFCPBINDINGENTRY2_WMI_CLASS_KR"></span>


T11 委員会の*ファイバーチャネル HBA API*仕様をサポートする hba ミニポートドライバーは、HBAFCPBindingEntry2 クラスを使用して、オペレーティングシステムが SCSI デバイスの論理ユニットを識別するために使用する情報と、論理ユニットのファイバーチャネルプロトコル (FCP) 識別子。 FCP の詳細については、「T11 委員会の*Dpans ファイバーチャネル Protocol FOR SCSI* specification」を参照してください。 SCSI および FCP 識別子間のこのバインディングの詳細については、T11 委員会の*ファイバーチャネル HBA API*仕様を参照してください。

HBAFCPBindingEntry2 クラスは、 *Hbaapi .mof*で次のように定義されています。

```cpp
class HBAFCPBindingEntry2 {
  [WmiDataId(1), HBA_BIND_TYPE_QUALIFIERS] HBA_BIND_TYPE  Type;
  [HBAType("HBA_FCPSCSIENTRY"), WmiDataId(4)] HBAScsiID  ScsiId;
  [HBAType("HBA_FCID"), WmiDataId(2)] HBAFCPID  FCPId;
  [HBAType("HBA_LUID"), WmiDataId(3)] uint8  Luid[256];
};
```

WMI ツールスイートによってコンパイルされた場合、このクラス定義では次のデータ構造が生成されます。

[**HBAFCPBindingEntry2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_hbafcpbindingentry2)

この WMI クラスに関連付けられているメソッドはありません。

 

 





