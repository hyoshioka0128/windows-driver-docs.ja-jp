---
title: ndiskd.netqueue
description: Ndiskd.netqueue 拡張機能では、NETTXQUEUE または NETRXQUEUE オブジェクトに関する情報が表示されます。
ms.assetid: 101F29AA-5CEE-41F8-A3EC-AA2E74B8E074
keywords:
- デバッグ ndiskd.netqueue Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.netqueue
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 49913265188f5e821015c673c1974a9e81e2c371
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558068"
---
# <a name="ndiskdnetqueue"></a>!ndiskd.netqueue


**! Ndiskd.netqueue**拡張機能が NETTXQUEUE または NETRXQUEUE オブジェクトに関する情報を表示します。

ネットワーク アダプター WDF クラス拡張 (NetAdapterCx) の詳細については、[ネットワーク アダプター WDF クラスの拡張機能 (Cx)](https://docs.microsoft.com/windows-hardware/drivers/netcx)を参照してください。

```console
!ndiskd.netqueue [-handle <x>] [-basic] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span> *-handle*   
必須。 NETTXQUEUE または NETRXQUEUE のハンドル。

<span id="_______-basic______"></span><span id="_______-BASIC______"></span> *-basic*   
基本的な情報を表示します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd.dll

<a name="examples"></a>例
--------

**注**  を参照してください[オブジェクトの概要](https://docs.microsoft.com/windows-hardware/drivers/netcx/summary-of-objects)NETTXQUEUE と NETRXQUEUE、NetAdapterCx の他のオブジェクトのオブジェクトのリレーションシップを説明する図を参照します。

 

NETTXQUEUE または NETRXQUEUE を識別するハンドルを取得するには、次の手順に従います。

1.  実行、 [ **! ndiskd.netadapter** ](-ndiskd-netadapter.md)拡張機能。
2.  NetAdapterCx ドライバーがインストールされている NetAdapter のハンドルをクリックします。
3.  実行する NetAdapter の NETADAPTER オブジェクトの右側に「詳細情報」リンクをクリックして、 [ **! ndiskd.cxadapter** ](-ndiskd-cxadapter.md)拡張機能。
4.  入力、 **! ndiskd.cxadapter**コマンドと、 *- データパス*パラメーターをその NETADAPTER のデータパス キューを参照してください。

この手順の詳細については、上の例を参照してください。、 **! ndiskd.cxadapter**トピック。
次の例には、この NETADAPTER の NETTXQUEUE、ffffd1022f512700 のハンドルを探します。

```console
0: kd> !ndiskd.cxadapter ffffd1022f1a0720 -basic -datapath


NETADAPTER

    Miniport           ffffd1022d048030 - Realtek PCIe GBE Family Controller NetAdapter Sample Driver #2
    NETADAPTER         00002efdd0e5f988    
    WDFDEVICE          00002efdcf45f2f8   

    Event Callbacks                        Function pointer   Symbol (if available)
    EvtAdapterCreateTxQueue                fffff80034151508   RtEthSample+1508
    EvtAdapterCreateRxQueue                fffff800341510ec   RtEthSample+10ec


DATAPATH QUEUES

    NETTXQUEUE         ffffd1022f512700
    NETRXQUEUE         ffffd1022cc7b0d0
```

NETTXQUEUE のハンドルをクリックするか入力して、 **! ndiskd.netqueue-処理**そのコンパニオンの WDF オブジェクト、リング バッファーを識別するハンドルを識別するハンドルを含む、このキューの詳細を確認できますが、コマンドラインでコマンドと登録済みのコールバックは、関数ポインター。

```console
0: kd> !ndiskd.netqueue ffffd1022f512700

    NETTXQUEUE         00002efdd0aed9a8
    Ring buffer        ffffd1022d000000

    Switch to EC thread

    Event Callbacks                        Function pointer   Symbol (if available)
    EvtQueueAdvance                        fffff80034152af8   RtEthSample+2af8
    EvtQueueArmNotification                fffff80034159a94   RtEthSample+9a94
    EvtQueueCancel                         fffff800341598d8   RtEthSample+98d8
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[ネットワーク ドライバーの設計ガイド](https://msdn.microsoft.com/windows/hardware/drivers/network/index)

[Windows Vista およびそれ以降のネットワーク リファレンス](https://msdn.microsoft.com/library/windows/hardware/ff571081)

[ネットワーク スタックのデバッグ](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 拡張機能 (Ndiskd.dll)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

[ネットワーク アダプター WDF クラスの拡張機能 (Cx)](https://docs.microsoft.com/windows-hardware/drivers/netcx)

[オブジェクトの概要](https://docs.microsoft.com/windows-hardware/drivers/netcx/summary-of-objects)

[**!ndiskd.netadapter**](-ndiskd-netadapter.md)

[**!ndiskd.cxadapter**](-ndiskd-cxadapter.md)

 

 






