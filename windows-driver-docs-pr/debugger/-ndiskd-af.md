---
title: ndiskd.af
description: Ndiskd.af 拡張機能では、接続指向の NDIS (CoNDIS アドレスファミリ (AF) が表示されます。
ms.assetid: 737AB46E-DFAA-42D6-A9BD-B7223167D0DD
keywords:
- ndiskd.af Windows のデバッグ
ms.date: 06/15/2020
topic_type:
- apiref
api_name:
- ndiskd.af
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 316dd60189943261ca9567d9714e7a4a2835fe32
ms.sourcegitcommit: 8596782b07c8a71adf38fc2c2da68b75ba0a1259
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85593958"
---
# <a name="ndiskdaf"></a>!ndiskd.af

**! Ndiskd.af**拡張機能では、接続指向の NDIS (condis アドレスファミリ (af) が表示されます。

```console
!ndiskd.af -handle <x>
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメータ

<span id="_______-handle______"></span><span id="_______-HANDLE______"></span>*-ハンドル*   
必須。 CoNDIS アドレスファミリのハンドル。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd.dll

### <a name="remarks"></a>Remarks

CoNDIS 使用する方法の詳細については、「[接続指向の NDIS](https://docs.microsoft.com/windows-hardware/drivers/network/connection-oriented-ndis)」を参照してください。

CoNDIS アドレスファミリの詳細については、「[アドレスファミリ](https://docs.microsoft.com/windows-hardware/drivers/network/address-families)」を参照してください。

### <a name="examples"></a>例

Condis は、VPN への接続などの特定の状況で使用されます。したがって、システム上のミニポートドライバーが CoNDIS 仮想接続を作成してアクティブ化していない限り、 **!** を実行しても結果が表示されません。 次の例は、VPN ネットワークに接続されているコンピューターからの結果を示しています。 最初に、パラメーターを付けずに[**! ndiskd netadapter**](-ndiskd-netadapter.md)拡張機能を実行して、システム上のミニポートドライバーとミニポートドライバーの一覧を表示します。 次の出力で、Marvell AVASTAR ワイヤレス-AC ネットワークコントローラーネットワークアダプターのミニポートドライバーを探します。 そのハンドルは ffffc804af2e3710 です。

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

次に、 **! ndiskd.af**コマンドとミニポートドライバーのハンドルを入力して、このミニポートドライバーのアドレスファミリを確認します。このポートは、接続指向クライアントとして機能します。

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

## <a name="see-also"></a>関連項目

[ネットワーク ドライバー設計ガイド](https://docs.microsoft.com/windows-hardware/drivers/network/index)

[Windows Vista 以降のネットワークリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)

[ネットワークスタックのデバッグ](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-175-Debugging-the-Network-Stack)

[**NDIS 拡張機能 (Ndiskd.dll)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

[接続指向 NDIS](https://docs.microsoft.com/windows-hardware/drivers/network/connection-oriented-ndis)

[アドレス ファミリ](https://docs.microsoft.com/windows-hardware/drivers/network/address-families)
