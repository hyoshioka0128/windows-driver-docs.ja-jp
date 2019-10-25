---
title: ndiskd pendingnbls
description: Pendingnbls 拡張機能は、転送中の保留中の NBLs (NET_BUFFER_LISTs) を表示します。
ms.assetid: 9137B995-FCCA-4E25-85D3-FCB5B717EBDF
keywords:
- pendingnbls Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.pendingnbls
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8e2721e2ea83a9b14c18be328d1ce2e511d5ce24
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826540"
---
# <a name="ndiskdpendingnbls"></a>!ndiskd.pendingnbls


**! Ndiskd pendingnbls**拡張機能には、転送中の保留中の NBLs ([**NET\_BUFFER\_list**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-structure)) が表示されます。

```console
!ndiskd.pendingnbls [-handle <x>] [-fullstack] [-verbosity <x>] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメータ


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span> *-  を処理*します  
NDIS ミニポート、フィルター、またはオープンのハンドル。

<span id="_______-fullstack______"></span><span id="_______-FULLSTACK______"></span> *-fullstack*   
ハンドルに関連付けられているスタック全体から保留中の NBLs を表示します。

<span id="_______-verbosity______"></span><span id="_______-VERBOSITY______"></span> *-詳細*   
表示する詳細レベル。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd .dll

<a name="examples"></a>例
--------

**! pendingnbls**には、NDIS ミニポート、フィルター、またはオープンのハンドルを渡すことができます。 次の一連の例では、ミニポートハンドルを使用します。 すべてのミニポートとそれに関連付けられているミニドライバーの一覧を表示するには、パラメーターを使用せずに[ **! ndiskd netadapter**](-ndiskd-netadapter.md)拡張機能を実行します。 次の出力例では、ffffe00bc3f701a0 というハンドルを持つ Microsoft カーネルデバッグネットワークアダプターを探します。 ミニドライバーのハンドルは ffffe00bc51b9ae0 です。

```console
0: kd> !ndiskd.netadapter
    Driver             NetAdapter          Name                                 
    ffffe00bc6e12ae0   ffffe00bc6e4e1a0    Microsoft ISATAP Adapter #2
    ffffe00bc51b9ae0   ffffe00bc3f701a0    Microsoft Kernel Debug Network Adapter
```

ミニポートの保留中の NBLs を表示するには、ミニドライバーの SendNetBufferListsHandler にブレークポイントを設定します。 ミニドライバーのハンドルを使用して[ **! ndiskd**](-ndiskd-minidriver.md)コマンドを実行し、ハンドラーの一覧を表示します。次に、SendNetBufferListsHandler の右側にある "bp" リンクをクリックします。 または、コマンドラインで[**bp-handle**](bp--bu--bm--set-breakpoint-.md)コマンドを入力することもできます。

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

SendNetBufferListsHandler にブレークポイントを設定した後、 **g**コマンドを入力して、デバッグ対象対象コンピューターが実行されるようにし、ブレークポイントにヒットします。

```console
0: kd> bp fffff80ae9611870
0: kd> g
Breakpoint 0 hit
fffff80a`e9611870 4053            push    rbx
```

これで、ミニドライバーの SendNetBufferListsHandler ブレークポイントに達した後、ミニポートのハンドルを使用して **! ndiskd pendingnbls**コマンドを入力することで、ミニポートの保留中の NBLs を確認できます。

この例のデバッグ対象ターゲットコンピューターは、ブレークポイントにヒットしたときに web ページを読み込んでいたので、ミニポートのデータパスを経由してトラフィックが流れています **。  ** そのため、保留中の NBL が送信されました。 ミニドライバーの1つ以上の NBL ハンドラーにブレークポイントを設定した後でも、データパスにアクティビティがない場合は、保留中の NBLs が表示されないことがあります。

 

```console
0: kd> !ndiskd.pendingnbls ffffe00bc3f701a0

PHASE 1/3: Found 20 NBL pool(s).                 
PHASE 2/3: Found 342 freed NBL(s).                                    

    Pending Nbl        Currently held by                                        
    ffffe00bc5545c60   ffffe00bc3f701a0 - Microsoft Kernel Debug Network Adapter  [NetAdapter]                    
    

PHASE 3/3: Found 1 pending NBL(s) of 4817 total NBL(s).                      
Search complete.
```

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[ネットワークドライバーの設計ガイド](https://docs.microsoft.com/windows-hardware/drivers/network/index)

[Windows Vista 以降のネットワークリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)

[ネットワークスタックのデバッグ](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 拡張機能 (Ndiskd .dll)** ](ndis-extensions--ndiskd-dll-.md)

[ **! ndiskd ヘルプ**](-ndiskd-help.md)

[**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-structure)

[ **! ndiskd netadapter**](-ndiskd-netadapter.md)

[ **! ndiskd ミニドライバー**](-ndiskd-minidriver.md)

[**bp、bu、bm (ブレークポイントの設定)** ](bp--bu--bm--set-breakpoint-.md)

 

 






