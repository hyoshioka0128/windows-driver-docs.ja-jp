---
title: ライブ ローカル デバッグ
description: ライブ ローカル デバッグ
ms.assetid: ec76a71e-f173-4b66-beaf-d57a1c991acd
keywords:
- カーネル デバッグは、ストリーミング ライブのローカル デバッグ
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8d57332b86f9aef90fa20abf6ad82ab94baa132e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529587"
---
# <a name="live-local-debugging"></a>ライブ ローカル デバッグ


Microsoft Windows XP およびそれ以降のオペレーティング システムでローカル カーネルをカーネル デバッガー (KD) または WinDbg を起動してデバッグを実行することは、 **-kl**コマンド ライン オプション。

```console
kd [-y SymbolPath] -kl 
```

または

```console
windbg [-y SymbolPath] -kl 
```

Windows Vista 以降では、ローカル カーネル デバッグが必要です、コンピューターを起動する、 **/debug**オプション。 管理者は、コマンド プロンプト ウィンドウを開き、入力**の bcdedit/debug**します。 コンピューターを再起動します。

> [!IMPORTANT]
> BCDEdit を使用してブート情報を変更する前に、テスト用のコンピューターの BitLocker とセキュア ブートなどの Windows セキュリティ機能を一時的に中断する必要があります。
> テストが完了すると、これらのセキュリティ機能を再度有効にし、適切なセキュリティ機能を無効にするテスト PC を管理します。

Windows Vista 以降では、ローカル カーネル デバッグ、デバッガーを管理者として実行する必要があります。

デバッガーがアタッチされている; 場合の再現が難しい問題のデバッグで非常に便利ですがライブのローカル デバッグただし、パケット、IRP、SRB など、時間の機密情報の知識を必要とするすべてのデータがハングまたは失速に問題がない限り動作することができます。

ローカル デバッグを実行する場合は、次の変数を考慮してください。

-   **全体的な状態です。** ストリームはたとえば、実行しているでしょうか。 ストリームが一時停止しますか。

-   **パケットをカウントします。** たとえばが Irp がストリームにキューに置かれたでしょうか。

-   **パケットの数に変更します。** ストリームを移動しますか。

-   **パケットのリストに変更します。**

-   **ハングしたカーネル スレッド。**

これらの最後のタスクを検討してください。

### <a name="span-idexaminingahungthreadinlkdspanspan-idexaminingahungthreadinlkdspanexamining-a-hung-thread-in-lkd"></a><span id="examining_a_hung_thread_in_lkd"></span><span id="EXAMINING_A_HUNG_THREAD_IN_LKD"></span>LKD でハングしたスレッドを調べる

まず、使用して、 [ **! process 0 0** ](-process.md)ハングしたスレッドを格納しているプロセスを識別する拡張機能。 次に、発行 **! プロセス**もう一度そのスレッドの詳細については。

```dbgcmd
lkd> !process 816a550 7
        THREAD 81705da8  Cid 0b5c.0b60  Teb: 7ffde000 Win32Thread: e1b2d890 WAIT: (Suspended)
        IRP List:
            816c9ad8: (0006,0190) Flags: 00000030  Mdl: 00000000
        Start Address kernel32!BaseProcessStartThunk (0x77e5c650)
        Win32 Start Address 0x0101c9be
        Stack Init f50bf000 Current f50bea74 Base f50bf000 Limit f50b9000 Call 0
        Priority 10 BasePriority 8 PriorityDecrement 0
```

スレッドは表示されませんが、スタックのアドレスします。 使用して、 [ **dds** ](dds--dps--dqs--display-words-and-symbols-.md) (または**ddq**) のどのプロセスを呼び出すことが指定されているため、スタック上の現在のアドレスでのコマンドは、さらに調査の開始点が生成されます。

```dbgcmd
lkd> dds f50bea74
f50bea74  f50bebc4
f50bea78  00000000
f50bea7c  80805795 nt!KiSwapContext+0x25
f50beab4  8080ece0 nt!KeWaitForSingleObject
f50beabc  f942afda ks!CKsQueue::CancelAllIrps+0x14
f50bead8  f94406c4 ks!CKsQueue::SetDeviceState+0x170
f50beb00  f943f6f1 ks!CKsPipeSection::DistributeDeviceStateChange+0x1d
f50beb24  f943fb1e ks!CKsPipeSection::SetDeviceState+0xb2
```

 

 





