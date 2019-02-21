---
title: ndiskd.pendingnbls
description: Ndiskd.pendingnbls 拡張機能は、保留中の転送中に含まれる NBLs (NET_BUFFER_LISTs) が表示されます。
ms.assetid: 9137B995-FCCA-4E25-85D3-FCB5B717EBDF
keywords:
- デバッグ ndiskd.pendingnbls Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.pendingnbls
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b236ed37b5fc5d19f7e0b43cb1485f0ba88496f5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537570"
---
# <a name="ndiskdpendingnbls"></a>!ndiskd.pendingnbls


**! Ndiskd.pendingnbls** NBLs 保留中の拡張機能が表示されます ([**NET\_バッファー\_を一覧表示**](https://msdn.microsoft.com/windows/hardware/drivers/network/net-buffer-list-structure)) に転送します。

```console
!ndiskd.pendingnbls [-handle <x>] [-fullstack] [-verbosity <x>] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span> *-handle*   
NDIS ミニポート、フィルター、またはオープンのハンドル。

<span id="_______-fullstack______"></span><span id="_______-FULLSTACK______"></span> *-fullstack*   
保留中の NBLs、ハンドルに関連付けられたスタック全体が表示されます。

<span id="_______-verbosity______"></span><span id="_______-VERBOSITY______"></span> *-verbosity*   
表示する詳細のレベルです。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd.dll

<a name="examples"></a>例
--------

**! ndiskd.pendingnbls** NDIS ミニポート、フィルター、またはオープンのハンドルを渡すことができます。 次の一連の例では、ミニポート ハンドルを使用します。 すべてミニポートと関連付けられている、ミニドライバーの一覧を表示するには、実行、 [ **! ndiskd.netadapter** ](-ndiskd-netadapter.md)パラメーターなしで拡張機能。 次の出力例では、Microsoft カーネル デバッグ ネットワーク アダプターが、そのハンドルは ffffe00bc3f701a0 を探します。 そのミニドライバーのハンドルは、ffffe00bc51b9ae0 です。

```console
0: kd> !ndiskd.netadapter
    Driver             NetAdapter          Name                                 
    ffffe00bc6e12ae0   ffffe00bc6e4e1a0    Microsoft ISATAP Adapter #2
    ffffe00bc51b9ae0   ffffe00bc3f701a0    Microsoft Kernel Debug Network Adapter
```

ミニポートの保留中の NBLs を表示するには、そのミニドライバーの SendNetBufferListsHandler にブレークポイントを設定します。 ミニドライバーのハンドルを使用して実行する、 [ **! ndiskd.minidriver-処理 - ハンドラー** ](-ndiskd-minidriver.md)コマンドをそのハンドラーの一覧を表示し、SendNetBufferListsHandler の右側に"bp"リンクをクリックします。 別の方法として入力することができます、 [ **bp-処理**](bp--bu--bm--set-breakpoint-.md)コマンド ライン コマンド。

```console
0: kd> !ndiskd.minidriver ffffe00bc51b9ae0 -handlers


HANDLERS

    NDIS Handler                           Function pointer   Symbol (if available)
    InitializeHandlerEx                    fffff80ae9618230  bp
    SetOptionsHandler                      fffff80ae9612800  bp
    HaltHandlerEx                          fffff80ae9618040  bp
    ShutdownHandlerEx                      fffff80ae96122c0  bp

    CheckForHangHandlerEx                  fffff80ae9612810  bp
    ResetHandlerEx                         fffff80ae9612f70  bp

    PauseHandler                           fffff80ae9618000  bp
    RestartHandler                         fffff80ae9618940  bp

    OidRequestHandler                      fffff80ae9611c90  bp
    CancelOidRequestHandler                fffff80ae96122c0  bp
    DirectOidRequestHandler                [None]
    CancelDirectOidRequestHandler          [None]
    DevicePnPEventNotifyHandler            fffff80ae96189a0  bp

    SendNetBufferListsHandler              fffff80ae9611870  bp
    ReturnNetBufferListsHandler            fffff80ae9611b50  bp
    CancelSendHandler                      fffff80ae96122c0  bp
```

入力、SendNetBufferListsHandler でブレークポイントを設定した後、 **g**デバッグ対象のターゲット コンピューターを実行し、ブレークポイントにヒットさせるコマンド。

```console
0: kd> bp fffff80ae9611870
0: kd> g
Breakpoint 0 hit
fffff80a`e9611870 4053            push    rbx
```

ここで、ミニドライバーの SendNetBufferListsHandler ブレークポイントをヒットした後の表示できます NBLs 保留中のミニポートを入力して、 **! ndiskd.pendingnbls-処理**ミニポートのハンドルを持つコマンド。

**注**  トラフィックがミニポートのデータパス経由で流れているように、ブレークポイントをヒットしたときにこの例では、デバッグ対象のターゲット コンピューターで web ページが読み込み。 そのため、保留中の NBL を送信する必要があります。 NBL ハンドラーの 1 つ以上で、ミニドライバーのブレークポイントを設定した後でも見えないことがあります、保留中の NBLs データパスにアクティビティが存在しない場合。

 

```console
0: kd> !ndiskd.pendingnbls ffffe00bc3f701a0

PHASE 1/3: Found 20 NBL pool(s).                 
PHASE 2/3: Found 342 freed NBL(s).                                    

    Pending Nbl        Currently held by                                        
    ffffe00bc5545c60   ffffe00bc3f701a0 - Microsoft Kernel Debug Network Adapter  [NetAdapter]                    
    

PHASE 3/3: Found 1 pending NBL(s) of 4817 total NBL(s).                      
Search complete.
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[ネットワーク ドライバーの設計ガイド](https://msdn.microsoft.com/windows/hardware/drivers/network/index)

[Windows Vista およびそれ以降のネットワーク リファレンス](https://msdn.microsoft.com/library/windows/hardware/ff571081)

[ネットワーク スタックのデバッグ](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 拡張機能 (Ndiskd.dll)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

[**NET\_バッファー\_一覧**](https://msdn.microsoft.com/windows/hardware/drivers/network/net-buffer-list-structure)

[**!ndiskd.netadapter**](-ndiskd-netadapter.md)

[**!ndiskd.minidriver**](-ndiskd-minidriver.md)

[**bp、bu、bm (ブレークポイントの設定)**](bp--bu--bm--set-breakpoint-.md)

 

 






