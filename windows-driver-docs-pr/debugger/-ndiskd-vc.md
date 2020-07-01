---
title: ndiskd.vc
description: Ndiskd.vc 拡張機能は、接続指向 (CoNDIS 仮想接続 (VC) を表示します。
ms.assetid: 8F172026-3FBC-4686-A3A4-F54F1A0D08E5
keywords:
- ndiskd.vc Windows のデバッグ
ms.date: 06/26/2020
topic_type:
- apiref
api_name:
- ndiskd.vc
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1227c1386889ee98332a6c037b0a71459896fb9a
ms.sourcegitcommit: 8596782b07c8a71adf38fc2c2da68b75ba0a1259
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85593908"
---
# <a name="ndiskdvc"></a>!ndiskd.vc

**! Ndiskd.vc**拡張機能には、接続指向 (condis 仮想接続 (vc) が表示されます。

```console
!ndiskd.vc -handle <x>
```

## <a name="parameters"></a>パラメーター

<span id="_______-handle______"></span><span id="_______-HANDLE______"></span>*-ハンドル*   
必須。 VC ポインターのハンドル。

### <a name="dll"></a>[DLL]

Ndiskd.dll

### <a name="remarks"></a>Remarks

CoNDIS 使用する方法の詳細については、「[接続指向の NDIS](https://docs.microsoft.com/windows-hardware/drivers/network/connection-oriented-ndis)」を参照してください。

CoNDIS 仮想接続の詳細については、「[仮想接続](https://docs.microsoft.com/windows-hardware/drivers/network/virtual-connections)」を参照してください。

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

次に、ミニポートドライバーのハンドルを使用して **! ndiskd.vc**コマンドを入力し、そのミニポートドライバーによって開かれた仮想接続を確認します。

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

## <a name="see-also"></a>関連項目

[ネットワーク ドライバー設計ガイド](https://docs.microsoft.com/windows-hardware/drivers/network/index)

[Windows Vista 以降のネットワークリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)

[ネットワークスタックのデバッグ](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-175-Debugging-the-Network-Stack)

[**NDIS 拡張機能 (Ndiskd.dll)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

[接続指向 NDIS](https://docs.microsoft.com/windows-hardware/drivers/network/connection-oriented-ndis)

[仮想接続](https://docs.microsoft.com/windows-hardware/drivers/network/virtual-connections)

[**!ndiskd.netadapter**](-ndiskd-netadapter.md)
