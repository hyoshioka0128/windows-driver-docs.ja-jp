---
title: HBAFCPID WMI クラス
description: HBAFCPID WMI クラス
ms.assetid: 6b0d0f79-a7a8-4341-955b-2c3068936a1d
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f51d8ff3f8e3d8aaf0cf613ffa2418cd8395902f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360218"
---
# <a name="hbafcpid-wmi-class"></a>HBAFCPID WMI クラス


## <span id="ddk_hbafcpid_wmi_class_kr"></span><span id="DDK_HBAFCPID_WMI_CLASS_KR"></span>


T11 委員会をサポートする HBA ミニポート ドライバー*ファイバー チャネル HBA API*仕様では、HBAFCPID クラスを使用して、論理ユニットのファイバー チャネル プロトコル (FCP) 識別子を定義します。 FCP 識別子には、マシン上にある論理ユニットとアクセスできる、HBA ポートの名前を指定します。

ミニポート ドライバーでは、この識別子を使用して、論理ユニットのオペレーティング システムを使用して論理ユニットを識別する情報および FCP 識別子の間のバインドを構築します。 この種類のバインドの詳細については、次を参照してください。 [ **HBAFCPBindingEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_hbafcpbindingentry)します。 ファイバー チャネル プロトコルの詳細については、T11 委員会を参照してください。 *dpANS scsi、ファイバー チャネル プロトコル*仕様。

HBAFCPID クラスは次のように定義されている*Hbaapi.mof*:

```cpp
class HBAFCPID {
  [WmiDataId(1)] uint32  Fcid;
  [HBAType("HBA_WWN"), WmiDataId(2)] uint8  NodeWWN[8];
  [HBAType("HBA_WWN"), WmiDataId(3)] uint8  PortWWN[8];
  [WmiDataId(4)] uint64  FcpLun;
};
```

WMI ツール スイートによってコンパイルされるときに、このクラスの定義には、次のデータ構造が生成されます。

[**HBAFCPID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_hbafcpid)

この WMI クラスに関連付けられているメソッドはありません。

 

 





