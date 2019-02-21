---
title: ndiskd.mopen
description: Ndiskd.mopen 拡張機能には、ミニポートおよびプロトコル間のバインド情報が表示されます。
ms.assetid: 439c4647-8f3e-4473-aca8-364b5d2206e9
keywords:
- デバッグ ndiskd.mopen Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.mopen
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: bd991b6da9ab80ece3a88a81410effc9099a4bb6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527880"
---
# <a name="ndiskdmopen"></a>! ndiskd.mopen


**! Ndiskd.mopen**拡張機能は、ミニポートおよびプロトコル間のバインドに関する情報を表示します。 パラメーターなしで、この拡張機能を実行する場合。 ndiskd NDIS ミニポート ドライバーとプロトコル ドライバーのすべての開いているバインディングの一覧が表示されます。

```console
!ndiskd.mopen [-handle <x>] [-ref] 
```

## <a name="span-idddkndiskdmopendbgspanspan-idddkndiskdmopendbgspanparameters"></a><span id="ddk__ndiskd_mopen_dbg"></span><span id="DDK__NDISKD_MOPEN_DBG"></span>パラメーター


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span> *-handle*   
NDIS のハンドルは、バインドを開きます。

<span id="_______-ref______"></span><span id="_______-REF______"></span> *-ref*   
開いているバインディングの refcounts を示しています。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd.dll

<a name="examples"></a>例
--------

入力、! ndiskd.mopen コマンドは、開いているすべてのバインドの一覧を取得します。 この例では、Microsoft ISATAP アダプター間のバインドを探します\#2 ミニポートと TCPIP6TUNNEL プロトコル。 そのハンドルは、ffff8083e56b8110 です。

```console
3: kd> !ndiskd.mopen
Open ffff8083e56b8110
  Miniport: ffff8083e02ce1a0 - Microsoft ISATAP Adapter #2
  Protocol: ffff8083e1a95c00 - TCPIP6TUNNEL

Open ffff8083e11902c0
  Miniport: ffff8083e0f501a0 - Microsoft Kernel Debug Network Adapter
  Protocol: ffff8083e3e8f6b0 - RSPNDR

Open ffff8083e55f3010
  Miniport: ffff8083e0f501a0 - Microsoft Kernel Debug Network Adapter
  Protocol: ffff8083e0114730 - NDISUIO

Open ffff8083e15537d0
  Miniport: ffff8083e0f501a0 - Microsoft Kernel Debug Network Adapter
  Protocol: ffff8083e3e90800 - LLTDIO

Open ffff8083e3926010
  Miniport: ffff8083e0f501a0 - Microsoft Kernel Debug Network Adapter
  Protocol: ffff8083e3e90c10 - MSLLDP

Open ffff8083e0c565a0
  Miniport: ffff8083e0f501a0 - Microsoft Kernel Debug Network Adapter
  Protocol: ffff8083e11cec10 - TCPIP

Open ffff8083e504c770
  Miniport: ffff8083e0f501a0 - Microsoft Kernel Debug Network Adapter
  Protocol: ffff8083e19bfc10 - TCPIP6
```

これで、ハンドルをクリックしますか、ハンドルを使用して、入力、 **! ndiskd.mopen-処理**コマンドで、データパス状態などの開いているそのバインドに関する詳細情報を確認し、パス情報を受信することができます。

```console
3: kd> !ndiskd.mopen ffff8083e56b8110


OPEN

    Ndis handle        ffff8083e56b8110
    Flags              [No flags set]
    References         1                   Show detail
    Source             1
    Datapath state     Running

    Protocol           ffff8083e1a95c00 - TCPIP6TUNNEL
    Protocol context   ffff8083e15b62e0

    Miniport           ffff8083e02ce1a0 - Microsoft ISATAP Adapter #2
    Miniport context   ffff8083e0772010


RECEIVE PATH

    Packet filter      [No flags set]
    Frame Type(s)      0x86dd
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[ネットワーク ドライバーの設計ガイド](https://msdn.microsoft.com/windows/hardware/drivers/network/index)

[Windows Vista およびそれ以降のネットワーク リファレンス](https://msdn.microsoft.com/library/windows/hardware/ff571081)

[ネットワーク スタックのデバッグ](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 拡張機能 (Ndiskd.dll)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

 

 






