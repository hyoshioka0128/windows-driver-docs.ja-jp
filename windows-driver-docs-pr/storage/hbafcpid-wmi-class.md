---
title: HBAFCPID WMI クラス
description: HBAFCPID WMI クラス
ms.assetid: 6b0d0f79-a7a8-4341-955b-2c3068936a1d
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a11b0843b31e1d804c6e9ab47a0d26da778ede40
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557598"
---
# <a name="hbafcpid-wmi-class"></a>HBAFCPID WMI クラス


## <span id="ddk_hbafcpid_wmi_class_kr"></span><span id="DDK_HBAFCPID_WMI_CLASS_KR"></span>


T11 委員会をサポートする HBA ミニポート ドライバー*ファイバー チャネル HBA API*仕様では、HBAFCPID クラスを使用して、論理ユニットのファイバー チャネル プロトコル (FCP) 識別子を定義します。 FCP 識別子には、マシン上にある論理ユニットとアクセスできる、HBA ポートの名前を指定します。

ミニポート ドライバーでは、この識別子を使用して、論理ユニットのオペレーティング システムを使用して論理ユニットを識別する情報および FCP 識別子の間のバインドを構築します。 この種類のバインドの詳細については、[ **HBAFCPBindingEntry**](https://msdn.microsoft.com/library/windows/hardware/ff556034)を参照してください。 ファイバー チャネル プロトコルの詳細については、T11 委員会を参照してください。 *dpANS scsi、ファイバー チャネル プロトコル*仕様。

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

[**HBAFCPID**](https://msdn.microsoft.com/library/windows/hardware/ff556038)

この WMI クラスに関連付けられているメソッドはありません。

 

 





