---
title: ndiskd netqueue
description: Ndiskd netqueue 拡張機能には、NETTXQUEUE オブジェクトまたは NETRXQUEUE オブジェクトに関する情報が表示されます。
ms.assetid: 101F29AA-5CEE-41F8-A3EC-AA2E74B8E074
keywords:
- ndiskd netqueue Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.netqueue
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2a94e3d761fc7437faec4816c40db7aca2f49124
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534909"
---
# <a name="ndiskdnetqueue"></a>!ndiskd.netqueue


**! Ndiskd netqueue**拡張機能には、nettxqueue オブジェクトまたは NETRXQUEUE オブジェクトに関する情報が表示されます。

ネットワークアダプターの WDF クラス拡張 (NetAdapterCx) の詳細については、「 [Network ADAPTER WDF Class extension (Cx)](https://docs.microsoft.com/windows-hardware/drivers/netcx)」を参照してください。

```console
!ndiskd.netqueue [-handle <x>] [-basic] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメータ


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span>*-ハンドル*   
必須。 NETTXQUEUE または NETRXQUEUE のハンドル。

<span id="_______-basic______"></span><span id="_______-BASIC______"></span>*-基本*   
基本情報を表示します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd .dll

<a name="examples"></a>例
--------

**メモ**   「[オブジェクトの概要](https://docs.microsoft.com/windows-hardware/drivers/netcx/summary-of-objects)」を参照して、nettxqueue オブジェクトと NETRXQUEUE オブジェクトと NetAdapterCx 内の他のオブジェクトとの関係を説明する図を参照してください。

 

NETTXQUEUE または NETRXQUEUE のハンドルを取得するには、次の手順を実行します。

1.  [**! Ndiskd netadapter**](-ndiskd-netadapter.md)拡張機能を実行します。
2.  NetAdapterCx ドライバーがインストールされている NetAdapter のハンドルをクリックします。
3.  NetAdapter の NETADAPTER オブジェクトの右側にある [詳細情報] リンクをクリックして、 [**! ndiskd cxadapter**](-ndiskd-cxadapter.md)拡張機能を実行します。
4.  *-データパス*パラメーターを指定して **! ndiskd cxadapter**コマンドを入力すると、netadapter のデータパスキューが表示されます。

この手順の詳細については、 **! ndiskd cxadapter**のトピックの例を参照してください。
次の例では、この NETADAPTER の NETTXQUEUE、ffffd1022f512700 のハンドルを探します。

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

NETTXQUEUE のハンドルをクリックするか、コマンドラインで **! ndiskd**ハンドルコマンドを入力することにより、このキューの詳細を確認できます。これには、コンパニオン WDF オブジェクトへのハンドル、リングバッファーへのハンドル、および登録されているコールバックの関数ポインターが含まれます。

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

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[ネットワーク ドライバー設計ガイド](https://docs.microsoft.com/windows-hardware/drivers/network/index)

[Windows Vista 以降のネットワークリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)

[ネットワークスタックのデバッグ](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-175-Debugging-the-Network-Stack)

[**NDIS 拡張機能 (Ndiskd .dll)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

[ネットワークアダプターの WDF クラス拡張 (Cx)](https://docs.microsoft.com/windows-hardware/drivers/netcx)

[オブジェクトの概要](https://docs.microsoft.com/windows-hardware/drivers/netcx/summary-of-objects)

[**!ndiskd.netadapter**](-ndiskd-netadapter.md)

[**!ndiskd.cxadapter**](-ndiskd-cxadapter.md)

 

 






