---
title: ndiskd.protocol
description: Ndiskd.protocol コマンドでは、NDIS プロトコル ドライバーに関する情報が表示されます。
ms.assetid: c1d349d5-b0ba-4665-a399-1bc5cd55dde6
keywords:
- デバッグ ndiskd.protocol Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.protocol
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9967afc8bcb392bc473b548b84a63da969a5b289
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363108"
---
# <a name="ndiskdprotocol"></a>!ndiskd.protocol


**! Ndiskd.protocol**コマンドは、NDIS プロトコル ドライバーに関する情報を表示します。 パラメーターなしで、この拡張機能を実行する場合。 ndiskd システムでアクティブな NDIS プロトコル ドライバーの一覧が表示されます。

```console
!ndiskd.protocol [-handle <x>] [-findname <any>] 
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメーター


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span> *-handle*   
NDIS のプロトコルのハンドル。

<span id="_______-findname______"></span><span id="_______-FINDNAME______"></span> *-findname*   
プロトコルを名のプレフィックスでフィルター処理します。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Ndiskd.dll

<a name="examples"></a>例
--------

入力、 **! ndiskd.protocol**コマンドをそのハンドルでは、すべての NDIS プロトコルの一覧を表示し、(ある場合)、ミニポートへのバインドを開きます。 次の例では、TCPIP6TUNNEL プロトコルのハンドル、ffff8083e1a95c00 を探します。

```console
3: kd> !ndiskd.protocol
ffff8083e0114730 - NDISUIO
  ffff8083e55f3010 - Microsoft Kernel Debug Network Adapter

ffff8083e3e90c10 - MSLLDP
  ffff8083e3926010 - Microsoft Kernel Debug Network Adapter

ffff8083e3e98c10 - WANARPV6

ffff8083e3e97010 - WANARP

ffff8083e3e8f6b0 - RSPNDR
  ffff8083e11902c0 - Microsoft Kernel Debug Network Adapter

ffff8083e3e90800 - LLTDIO
  ffff8083e15537d0 - Microsoft Kernel Debug Network Adapter

ffff8083e1a9ac10 - RDMANDK

ffff8083e1a95c00 - TCPIP6TUNNEL
  ffff8083e56b8110 - Microsoft ISATAP Adapter #2

ffff8083e19bec10 - TCPIPTUNNEL

ffff8083e19bfc10 - TCPIP6
  ffff8083e504c770 - Microsoft Kernel Debug Network Adapter

ffff8083e11cec10 - TCPIP
  ffff8083e0c565a0 - Microsoft Kernel Debug Network Adapter
```

プロトコルのハンドルを入力できるようになりましたハンドルをクリックしてまたはのいずれかを入力、 **! ndiskd.protocol-処理**コマンドにバインドされているミニポートのハンドルなど、そのプロトコルの情報を確認します。

```console
3: kd> !ndiskd.protocol ffff8083e1a95c00


PROTOCOL

    TCPIP6TUNNEL

    Ndis handle        ffff8083e1a95c00
    Ndis API version   v6.40
    Driver context     fffff80e2e4f9de0
    Driver version     v0.0
    Reference count    2
    Flags              [No flags set]
    Driver image       [Not available]     Why not?


BINDINGS

    Open               Miniport            Miniport Name                        
    ffff8083e56b8110   ffff8083e02ce1a0    Microsoft ISATAP Adapter #2


HANDLERS

    Protocol handler                       Function pointer   Symbol (if available)
    BindAdapterHandlerEx                   fffff80e2e3baab0  bp
    UnbindAdapterHandlerEx                 fffff80e2e3c1c80  bp
    OpenAdapterCompleteHandlerEx           fffff80e2e4bc940  bp
    CloseAdapterCompleteHandlerEx          fffff80e2e3d19b0  bp
    NetPnPEventHandler                     fffff80e2e3bb140  bp
    UninstallHandler                       [None]
    SendNetBufferListsCompleteHandler      fffff80e2e3919a0  bp
    ReceiveNetBufferListsHandler           fffff80e2e3918a0  bp
    StatusHandlerEx                        fffff80e2e3a9550  bp
    OidRequestCompleteHandler              fffff80e2e398120  bp
    DirectOidRequestCompleteHandler        fffff80e2e398120  bp
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[ネットワーク ドライバーの設計ガイド](https://docs.microsoft.com/windows-hardware/drivers/network/index)

[Windows Vista およびそれ以降のネットワーク リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)

[ネットワーク スタックのデバッグ](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 拡張機能 (Ndiskd.dll)** ](ndis-extensions--ndiskd-dll-.md)

[ **!ndiskd.help**](-ndiskd-help.md)

 

 






