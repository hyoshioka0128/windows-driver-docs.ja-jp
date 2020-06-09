---
title: ndiskd mopen
description: Ndiskd mopen 拡張機能は、ミニポートとプロトコルの間のバインディングに関する情報を表示します。
ms.assetid: 439c4647-8f3e-4473-aca8-364b5d2206e9
keywords:
- ndiskd mopen Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.mopen
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d3407e5f652bf63ecade29eb4552c49d8c02d8da
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534923"
---
# <a name="ndiskdmopen"></a>!ndiskd.mopen


**! Ndiskd mopen**拡張機能には、ミニポートとプロトコルの間のバインディングに関する情報が表示されます。 パラメーターを使用せずにこの拡張機能を実行すると、NDIS ミニポートドライバーとプロトコルドライバーの間のすべての開いているバインドの一覧が表示されます。

```console
!ndiskd.mopen [-handle <x>] [-ref] 
```

## <a name="span-idddk__ndiskd_mopen_dbgspanspan-idddk__ndiskd_mopen_dbgspanparameters"></a><span id="ddk__ndiskd_mopen_dbg"></span><span id="DDK__NDISKD_MOPEN_DBG"></span>パラメータ


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span>*-ハンドル*   
NDIS オープンバインドのハンドル。

<span id="_______-ref______"></span><span id="_______-REF______"></span>*-ref*   
開いているバインドの refcounts を表示します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd .dll

<a name="examples"></a>例
--------

! Ndiskd mopen コマンドを入力して、開いているすべてのバインドの一覧を取得します。 この例では、Microsoft ISATAP アダプター \# 2 のミニポートと TCPIP6TUNNEL プロトコルの間のバインドを探します。 そのハンドルは ffff8083e56b8110 です。

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

これでハンドルをクリックするか、ハンドルを使用して **! ndiskd. mopen-handle**コマンドを入力することができます。これにより、データパスの状態や受信パスの情報など、開いているバインドの詳細を確認できます。

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

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[ネットワーク ドライバー設計ガイド](https://docs.microsoft.com/windows-hardware/drivers/network/index)

[Windows Vista 以降のネットワークリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)

[ネットワークスタックのデバッグ](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-175-Debugging-the-Network-Stack)

[**NDIS 拡張機能 (Ndiskd .dll)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

 

 






