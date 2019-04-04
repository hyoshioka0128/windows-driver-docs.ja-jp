---
title: ndiskd.af
description: Ndiskd.af 拡張機能では、Connection-Oriented NDIS (いる CoNDIS) アドレス ファミリ (AF) が表示されます。
ms.assetid: 737AB46E-DFAA-42D6-A9BD-B7223167D0DD
keywords:
- デバッグ ndiskd.af Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.af
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9c6498cfbe425af1020415d90f2421b8f516db4b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558876"
---
# <a name="ndiskdaf"></a>! ndiskd.af


**! Ndiskd.af**拡張子 Connection-Oriented NDIS (いる CoNDIS) アドレス ファミリ (AF) が表示されます。

```console
!ndiskd.af [-handle <x>] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span> *-handle*   
必須。 いる CoNDIS アドレス ファミリのハンドル。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd.dll

<a name="remarks"></a>注釈
-------

いる CoNDIS の詳細については、[Connection-Oriented NDIS](https://msdn.microsoft.com/windows/hardware/drivers/network/connection-oriented-ndis)を参照してください。

いる CoNDIS アドレス ファミリの詳細については、[アドレス ファミリ](https://msdn.microsoft.com/windows/hardware/drivers/network/address-families)を参照してください。

<a name="examples"></a>例
--------

いる CoNDIS が実行されているため、VPN への接続などの特定の状況で使用される **! ndiskd.af**システム上のミニポート ドライバーが作成されいる CoNDIS 仮想接続をアクティブ化しない限りの結果は表示されません。 次の例では、VPN のネットワークに接続されているマシンからの結果を示します。 最初に、実行、 [ **! ndiskd.netadapter** ](-ndiskd-netadapter.md)拡張機能パラメーターのないシステムでミニポートおよびミニポートのドライバーの一覧を参照してください。 次の出力でもの AVASTAR ワイヤレス AC ネットワーク コント ローラーのネットワーク アダプターのミニポート ドライバーを探します。 そのハンドルは、ffffc804af2e3710 です。

```console
1: kd> !ndiskd.netadapter
    Driver             NetAdapter          Name                                 
    ffffc804af2e3710   ffffc804b9e6f1a0    Marvell AVASTAR Wireless-AC Network Controller
    ffffc804b99b9020   ffffc804b9c301a0    WAN Miniport (Network Monitor)
    ffffc804b99b9020   ffffc804b9c2a1a0    WAN Miniport (IPv6)
    ffffc804b99b9020   ffffc804b8a8a1a0    WAN Miniport (IP)
    ffffc804ae9d7020   ffffc804b9ceb1a0    WAN Miniport (PPPOE)
    ffffc804b9ca5900   ffffc804b9e601a0    WAN Miniport (PPTP)
    ffffc804b99dc720   ffffc804b99b01a0    WAN Miniport (L2TP)
    ffffc804b86581b0   ffffc804b9c6c1a0    WAN Miniport (IKEv2)
    ffffc804ad4a7250   ffffc804b99651a0    WAN Miniport (SSTP)
    ffffc804b11c4020   ffffc804b85821a0    Microsoft ISATAP Adapter
    ffffc804b11c4020   ffffc804b71731a0    Microsoft ISATAP Adapter #2
    ffffc804ad725020   ffffc804b05e71a0    Surface Ethernet Adapter #2
    ffffc804b0bf0020   ffffc804b0c011a0    Bluetooth Device (Personal Area Network)
    ffffc804aef695e0   ffffc804aed331a0    TAP-Windows Adapter V9
```

次に、入力、 **! ndiskd.af**コマンドに、ミニポート ドライバーのハンドルは、接続指向のクライアントとして機能するミニポート ドライバーのアドレス ファミリを参照してください。

```console
1: kd> !ndiskd.af ffffc804af2e3710


ADDRESS FAMILY

    Ndis handle        ffffc804af2e3710
    Flags              [Unrecognized flags 399b9020] AF_CLOSING
    References         ffffc804
    Close Requested?   0

    Miniport           0 - [Unreadable NetAdapter]

    Call Manager       ffffc804b90a4ac0 - [Invalid Open]
    Call Manager Context 007a0078

    Client             00060000 - [Unreadable Open]
    Client Context     ffffc804af2e3888


CLIENT HANDLERS

    Client Handler                         Function pointer   Symbol (if available)
    ClCreateVcHandler                      fffff80965fd5888   mrvlpcie8897!Globals+8
    ClDeleteVcHandler                      [None]
    ClRequestHandler                       ffffc804af96fd78
    ClRequestCompleteHandler               ffffc804af96fd78
    ClOpenAfCompleteHandler                [None]
    ClCloseAfCompleteHandler               [None]
    ClRegisterSapCompleteHandler           000132060098028a
    ClDeregisterSapCompleteHandler         [None]
    ClMakeCallCompleteHandler              fffff80965ff9ec0   wdiwifi!MPWrapperSetOptions
    ClCloseCallCompleteHandler             fffff80965ff9c70   wdiwifi!MPWrapperHalt
    ClModifyCallQoSCompleteHandler         fffff80965ff9b50   wdiwifi!MPWrapperInitializeEx
    ClAddPartyCompleteHandler              fffff80965e71a08   mrvlpcie8897!MPUnload
    ClDropPartyCompleteHandler             fffff80965ffa070   wdiwifi!MPWrapperPause
    ClIncomingDropPartyHandler             fffff80965ffaa20   wdiwifi!MPWrapperReturnNetBufferLists
    ClIncomingCallHandler                  fffff80965ffa1e0   wdiwifi!MPWrapperRestart
    ClCallConnectedHandler                 fffff80965ffaad0   wdiwifi!MPWrapperCancelSendNetBufferLists
    ClIncomingCloseCallHandler             fffff80965ffa870   wdiwifi!MPWrapperSendNetBufferLists
    ClIncomingCallQoSChangeHandler         fffff80965ffa610   wdiwifi!MPWrapperOidRequest
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[ネットワーク ドライバーの設計ガイド](https://msdn.microsoft.com/windows/hardware/drivers/network/index)

[Windows Vista およびそれ以降のネットワーク リファレンス](https://msdn.microsoft.com/library/windows/hardware/ff571081)

[ネットワーク スタックのデバッグ](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 拡張機能 (Ndiskd.dll)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

[接続指向の NDIS](https://msdn.microsoft.com/windows/hardware/drivers/network/connection-oriented-ndis)

[アドレス ファミリ](https://msdn.microsoft.com/windows/hardware/drivers/network/address-families)

 

 






