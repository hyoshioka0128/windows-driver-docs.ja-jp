---
title: ndiskd.ndisrwlock
description: Ndiskd.ndisrwlock 拡張機能では、NDIS_RW_LOCK_EX のロック構造に関する情報が表示されます。
ms.assetid: 853CBAFE-3899-4983-BFC7-933D3BC7ADA1
keywords:
- デバッグ ndiskd.ndisrwlock Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.ndisrwlock
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 439c293357ae150db5c40810ee2a49fde318a78f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364254"
---
# <a name="ndiskdndisrwlock"></a>!ndiskd.ndisrwlock


**! Ndiskd.ndisrwlock**拡張機能に関する情報を表示する、 [ **NDIS\_RW\_ロック\_EX** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff567279(v=vs.85))構造体をロックします。

```console
!ndiskd.ndisrwlock [-handle <x>] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span> *-handle*   
必須。 ロック構造のハンドル。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd.dll

<a name="examples"></a>例
--------

使用して、 **! ndiskd.ndisrwlock** RW ロックを作成してそれを検査する場合、拡張機能。 RW ロック ハンドルを取得するには、使用、 *poi*ドライバーのロックのアドレスを逆参照するコマンド。 次のスニペットでは、TCIPIP プロトコルを使用していた時の例では、ロックを確認する方法を示します。

```console
0: kd> !ndiskd.ndisrwlock poi(tcpip!gAleHashtableLock)


NDIS READ-WRITE LOCK

    Allocated by       [NDIS generic object]
    Exclusive access   Not acquired
    Read-only access   0 references

    Set a breakpoint on acquire/release
```

この RW ロックを使用してドライバーを確認するには、「取得/解除にブレークポイントを設定する」RW ロックの詳細の下部にあるリンクをクリックします。 ブレークポイントを設定した後は、入力、 **g**デバッグ対象のマシンを実行し、ブレークポイントにヒットさせるコマンド。

```console
0: kd> ba r4 ffffe00bc3fc22f8
0: kd> g
Breakpoint 0 hit
nt!KeTestSpinLock+0x3:
fffff802`0d69eb53 4885c0          test    rax,rax
```

これで、同じを再実行できます **! ndiskd.ndisrwlock**コマンドをこの RW ロックが 1 つの読み取り専用アクセス リファレンスを参照してください。

```console
0: kd> !ndiskd.ndisrwlock poi(tcpip!gAleHashtableLock)


NDIS READ-WRITE LOCK

    Allocated by       [NDIS generic object]
    Exclusive access   Not acquired
    Read-only access   1 reference

    Set a breakpoint on acquire/release
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[ネットワーク ドライバーの設計ガイド](https://docs.microsoft.com/windows-hardware/drivers/network/index)

[Windows Vista およびそれ以降のネットワーク リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)

[ネットワーク スタックのデバッグ](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 拡張機能 (Ndiskd.dll)** ](ndis-extensions--ndiskd-dll-.md)

[ **!ndiskd.help**](-ndiskd-help.md)

[**NDIS\_RW\_ロック\_例**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff567279(v=vs.85))

 

 






