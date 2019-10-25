---
title: HBAFCPID WMI クラス
description: HBAFCPID WMI クラス
ms.assetid: 6b0d0f79-a7a8-4341-955b-2c3068936a1d
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f2b8d5193f9afad12b778eea527e8c23c9c02a8a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72823802"
---
# <a name="hbafcpid-wmi-class"></a>HBAFCPID WMI クラス


## <span id="ddk_hbafcpid_wmi_class_kr"></span><span id="DDK_HBAFCPID_WMI_CLASS_KR"></span>


T11 委員会の*ファイバーチャネル HBA API*仕様をサポートする hba ミニポートドライバーは、HBAFCPID クラスを使用して、論理ユニットのファイバーチャネルプロトコル (FCP) 識別子を定義します。 FCP 識別子は、論理ユニットが配置されているコンピューターの名前と、それにアクセスできる HBA ポートを指定します。

ミニポートドライバーは、この識別子を使用して、オペレーティングシステムが論理ユニットを識別するために使用する情報と論理ユニットの FCP 識別子との間のバインドを作成します。 この種類のバインドの詳細については、「 [**Hbafcpbindingentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_hbafcpbindingentry)」を参照してください。 ファイバーチャネルプロトコルの詳細については、「SCSI 仕様」の「T11 委員会の*Dpans ファイバーチャネルプロトコル*」を参照してください。

HBAFCPID クラスは、 *Hbaapi .mof*で次のように定義されています。

```cpp
class HBAFCPID {
  [WmiDataId(1)] uint32  Fcid;
  [HBAType("HBA_WWN"), WmiDataId(2)] uint8  NodeWWN[8];
  [HBAType("HBA_WWN"), WmiDataId(3)] uint8  PortWWN[8];
  [WmiDataId(4)] uint64  FcpLun;
};
```

WMI ツールスイートによってコンパイルされた場合、このクラス定義では次のデータ構造が生成されます。

[**HBAFCPID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_hbafcpid)

この WMI クラスに関連付けられているメソッドはありません。

 

 





