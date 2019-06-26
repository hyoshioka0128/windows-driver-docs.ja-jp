---
title: ndiskd.vc
description: Ndiskd.vc 拡張機能では、接続指向 (いる CoNDIS) 仮想接続 (VC) が表示されます。
ms.assetid: 8F172026-3FBC-4686-A3A4-F54F1A0D08E5
keywords:
- デバッグ ndiskd.vc Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.vc
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7b1f767a18e84678f46cdda78d0d428c41fce80c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363097"
---
# <a name="ndiskdvc"></a>!ndiskd.vc


**! Ndiskd.vc**拡張機能には、接続指向 (いる CoNDIS) 仮想接続 (VC) が表示されます。

```console
!ndiskd.vc [-handle <x>] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span> *-handle*   
必須。 VC のポインターのハンドル。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd.dll

<a name="remarks"></a>注釈
-------

いる CoNDIS の詳細については、次を参照してください。 [Connection-Oriented NDIS](https://docs.microsoft.com/windows-hardware/drivers/network/connection-oriented-ndis)します。

いる CoNDIS 仮想接続の詳細については、次を参照してください。[仮想接続](https://docs.microsoft.com/windows-hardware/drivers/network/virtual-connections)します。

<a name="examples"></a>使用例
--------

いる CoNDIS が実行されているため、VPN への接続などの特定の状況で使用される **! ndiskd.vc**システム上のミニポート ドライバーが作成されいる CoNDIS 仮想接続をアクティブ化しない限りの結果は表示されません。 次の例では、VPN のネットワークに接続されているマシンからの結果を示します。 最初に、実行、 [ **! ndiskd.netadapter** ](-ndiskd-netadapter.md)拡張機能パラメーターのないシステムでミニポートおよびミニポートのドライバーの一覧を参照してください。 次の出力でもの AVASTAR ワイヤレス AC ネットワーク コント ローラーのネットワーク アダプターのミニポート ドライバーを探します。 そのハンドルは、ffffc804af2e3710 です。

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

次に、入力、 **! ndiskd.vc**ミニポート ドライバーで開かれている仮想接続を表示する、ミニポート ドライバーのハンドルを持つコマンド。

```console
1: kd> !ndiskd.vc ffffc804af2e3710


VIRTUAL CALL

    [Zero-length string]
    Ndis handle        ffffc804af2e3710
    VC Index           0

    AF                 fffff80965fd5888
    Call Flags         [No flags set]
    VC Flags           [Unrecognized flags 04a80100] VC_ACTIVATE_PENDING

    Miniport           fffff80965ffaa20 - [Invalid NetAdapter]
    Miniport Context   fffff80965ffaad0

    Call Manager       fffff80965ff9b50 - [Invalid Open]
    Call Manager Context fffff80965ff9c70

    Client             ffffc804af96fd78 - [Invalid Open]
    Client Context     00003206
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[ネットワーク ドライバーの設計ガイド](https://docs.microsoft.com/windows-hardware/drivers/network/index)

[Windows Vista およびそれ以降のネットワーク リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)

[ネットワーク スタックのデバッグ](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 拡張機能 (Ndiskd.dll)** ](ndis-extensions--ndiskd-dll-.md)

[ **!ndiskd.help**](-ndiskd-help.md)

[接続指向の NDIS](https://docs.microsoft.com/windows-hardware/drivers/network/connection-oriented-ndis)

[仮想接続](https://docs.microsoft.com/windows-hardware/drivers/network/virtual-connections)

[ **!ndiskd.netadapter**](-ndiskd-netadapter.md)

 

 






