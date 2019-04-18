---
title: バグ チェック 0x9F DRIVER_POWER_STATE_FAILURE
description: このバグ チェックでは、0x0000009F の値を持ちます。 このバグ チェックでは、一貫性のない、または無効な電源状態で、ドライバーがあることを示します。
ms.assetid: f767fe80-0ec0-45e4-9949-467f50ac601c
keywords:
- (開発者向けコンテンツ)バグ チェック 0x9F DRIVER_POWER_STATE_FAILURE
- DRIVER_POWER_STATE_FAILURE
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- DRIVER_POWER_STATE_FAILURE
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 43c0f79862ec42515ac8d6a8cdcadd4909cee21b
ms.sourcegitcommit: fb8b1d2e18dd727e8a479b04c9e6051e7e9fa484
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/18/2019
ms.locfileid: "59745871"
---
# <a name="developer-content-bug-check-0x9f-driverpowerstatefailure"></a>(開発者向けコンテンツ)チェック 0x9F バグの。ドライバー\_POWER\_状態\_エラー


ドライバー\_POWER\_状態\_エラーのバグ チェックが 0x0000009F の値を持ちます。 このバグ チェックでは、一貫性のない、または無効な電源状態で、ドライバーがあることを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。
<<<<<<< HEAD

=======
>>>>>>> マスター

## <a name="driverpowerstatefailure-parameters"></a>ドライバー\_POWER\_状態\_エラー パラメーター

パラメーター 1 では、違反の種類を示します。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター 1</th>
<th align="left">パラメータ 2</th>
<th align="left">3 番目のパラメーター</th>
<th align="left">パラメーター 4</th>
<th align="left">原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x1</p></td>
<td align="left"><p>デバイス オブジェクト</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>解放されているデバイス オブジェクトがまだ完了していない未処理の電源要求を使用しています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x2</p></td>
<td align="left"><p>入手可能になった場合は、ターゲット デバイスのデバイス オブジェクト</p></td>
<td align="left"><p>デバイス オブジェクト</p></td>
<td align="left"><p>使用可能になる場合は、ドライバー オブジェクト</p></td>
<td align="left"><p>デバイス オブジェクトは、システム電源の状態要求では、I/O 要求パケット (IRP) を完了しましたが、呼び出されませんでした<strong>PoStartNextPowerIrp</strong>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x3</p></td>
<td align="left"><p>スタックの物理デバイス オブジェクト (PDO)</p></td>
<td align="left"><p>スタックの機能のデバイス オブジェクト (FDO)。 で Windows 7 以降、nt!TRIAGE_9F_POWER します。</p></td>
<td align="left"><p>IRP がブロックされています。</p></td>
<td align="left"><p>デバイス オブジェクトには、時間が長すぎます IRP がブロックされています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x4</p></td>
<td align="left"><p>タイムアウト値 (秒)。</p></td>
<td align="left"><p>プラグ アンド プレイ (PnP) ロックを保持して現在のスレッド。</p></td>
<td align="left"><p>で Windows 7 以降、nt!TRIAGE_9F_POWER します。</p></td>
<td align="left"><p>PnP サブシステムとの同期を待機しているに電源状態の遷移がタイムアウトになりました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x500</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>使用可能な場合に、ターゲット デバイスのデバイス オブジェクト</p></td>
<td align="left"><p>デバイス オブジェクト</p></td>
<td align="left"><p>デバイス オブジェクトには、システム電源の状態要求の IRP が完了しましたが、呼び出されませんでした<strong>PoStartNextPowerIrp</strong>します。</p></td>
</tr>
</tbody>
</table>


## <a name="cause"></a>原因
-----

考えられる原因については、「パラメーター」セクション内の各コードの説明を参照してください。

## <a name="resolution"></a>解決方法
----------


**バグ チェック 0x9F パラメーター 1 が 0x3 ときのデバッグ**

-   カーネル デバッガーを使用して、 [ **!-v を分析**](-analyze.md)初期のバグ チェックの分析を実行するコマンド。 詳細な分析のアドレスを表示する、 **nt!トリアージ\_9F\_POWER** Arg3 では、構造体。

```dbgcmd
kd>!analyze -v
*******************************************************************************
*                                                                             *
*                        Bugcheck Analysis                                    *
*                                                                             *
*******************************************************************************

    DRIVER_POWER_STATE_FAILURE (9f)
    A driver has failed to complete a power IRP within a specific time.
    Arguments:
    Arg1: 0000000000000003, A device object has been blocking an Irp for too long a time
    Arg2: fffffa8007b13440, Physical Device Object of the stack
    Arg3: fffff8000386c3d8, nt!TRIAGE_9F_POWER on Win7 and higher, otherwise the Functional Device Object of the stack
    Arg4: fffffa800ab61bd0, The blocked IRP
```

Nt!トリアージ\_9F\_電源構造体がこのバグ チェックの原因を特定するために役立つ追加のバグ チェックの情報を提供します。 構造体には、すべての未処理 power Irp の一覧、すべての power IRP のワーカー スレッド、および遅延システム ワーカー キューへのポインターのリストを提供できます。

- 使用、 [ **dt (表示の種類)** ](dt--display-type-.md)コマンドおよび、nt を指定します。トリアージ\_9F\_Arg3 からアドレスを使用して電源構造体。

```dbgcmd
    0: kd> dt nt!TRIAGE_9F_POWER fffff8000386c3d8
       +0x000 Signature        : 0x8000
       +0x002 Revision         : 1
       +0x008 IrpList          : 0xfffff800`01c78bd0 _LIST_ENTRY [ 0xfffffa80`09f43620 - 0xfffffa80`0ad00170 ]
       +0x010 ThreadList       : 0xfffff800`01c78520 _LIST_ENTRY [ 0xfffff880`009cdb98 - 0xfffff880`181f2b98 ]
       +0x018 DelayedWorkQueue : 0xfffff800`01c6d2d8 _TRIAGE_EX_WORK_QUEUE
```

[ **Dt (表示の種類)** ](dt--display-type-.md)コマンド構造を表示します。 各種のデバッガー コマンドを使用するには、次の一覧を\_エントリ フィールドは、未処理の Irp と電源 IRP のワーカー スレッドの一覧を確認します。

-  使用して、 [ **! irp** ](-irp.md)コマンドがブロックされていた IRP を確認します。 Arg4 が、この IRP のアドレス。

```dbgcmd
    0: kd> !irp fffffa800ab61bd0
    Irp is active with 7 stacks 6 is current (= 0xfffffa800ab61e08)
     No Mdl: No System Buffer: Thread 00000000:  Irp stack trace.  
         cmd  flg cl Device   File     Completion-Context
     [N/A(0), N/A(0)]
                0  0 00000000 00000000 00000000-00000000    

                Args: 00000000 00000000 00000000 00000000
     [N/A(0), N/A(0)]
                0  0 00000000 00000000 00000000-00000000    

                Args: 00000000 00000000 00000000 00000000
     [N/A(0), N/A(0)]
                0  0 00000000 00000000 00000000-00000000    

                Args: 00000000 00000000 00000000 00000000
     [N/A(0), N/A(0)]
                0  0 00000000 00000000 00000000-00000000    

                Args: 00000000 00000000 00000000 00000000
     [N/A(0), N/A(0)]
                0  0 00000000 00000000 00000000-00000000    

                Args: 00000000 00000000 00000000 00000000
    >[IRP_MJ_POWER(16), IRP_MN_SET_POWER(2)]
                0 e1 fffffa800783f060 00000000 00000000-00000000    pending
               \Driver\HidUsb
                Args: 00016600 00000001 00000004 00000006
     [N/A(0), N/A(0)]
                0  0 00000000 00000000 00000000-fffffa800ad00170    

                Args: 00000000 00000000 00000000 00000000
```

- 使用して、 [ **! devstack** ](-devstack.md) Arg2、エラーが発生したドライバーに関連付けられている情報を表示するは、PDO アドレスを持つコマンド。

```dbgcmd
    0: kd> !devstack fffffa8007b13440
      !DevObj           !DrvObj            !DevExt           ObjectName
      fffffa800783f060  \Driver\HidUsb     fffffa800783f1b0  InfoMask field not found for _OBJECT_HEADER at fffffa800783f030

    > fffffa8007b13440  \Driver\usbhub     fffffa8007b13590  Cannot read info offset from nt!ObpInfoMaskToOffset

    !DevNode fffffa8007ac8a00 :
      DeviceInst is "USB\VID_04D8&PID_0033\5&46fa7b7&0&1"
      ServiceName is "HidUsb"
```

- 使用して、! poaction コマンドと電源操作を処理するスレッドを表示するには、電源 Irp が割り当てられています。

```dbgcmd
    3: kd> !poaction
    PopAction: fffff801332f3fe0
      State..........: 0 - Idle
      Updates........: 0 
      Action.........: None
      Lightest State.: Unspecified
      Flags..........: 10000003 QueryApps|UIAllowed
      Irp minor......: ??
      System State...: Unspecified
      Hiber Context..: 0000000000000000

    Allocated power irps (PopIrpList - fffff801332f44f0)
      IRP: ffffe0001d53d8f0 (wait-wake/S0), PDO: ffffe00013cae060
      IRP: ffffe0001049a5d0 (wait-wake/S0), PDO: ffffe00012d42050
      IRP: ffffe00013d07420 (set/D3,), PDO: ffffe00012daf840, CURRENT: ffffe00012dd5040
      IRP: ffffe0001e5ac5d0 (wait-wake/S0), PDO: ffffe00013d33060
      IRP: ffffe0001ed3e420 (wait-wake/S0), PDO: ffffe00013c96060
      IRP: ffffe000195fe010 (wait-wake/S0), PDO: ffffe00012d32050

    Irp worker threads (PopIrpThreadList - fffff801332f3100)
      THREAD: ffffe0000ef5d040 (static)
      THREAD: ffffe0000ef5e040 (static), IRP: ffffe00013d07420, DEVICE: ffffe00012dd5040

    PopAction: fffff801332f3fe0
      State..........: 0 - Idle
      Updates........: 0 
      Action.........: None
      Lightest State.: Unspecified
      Flags..........: 10000003 QueryApps|UIAllowed
      Irp minor......: ??
      System State...: Unspecified
      Hiber Context..: 0000000000000000

    Allocated power irps (PopIrpList - fffff801332f44f0)
      IRP: ffffe0001d53d8f0 (wait-wake/S0), PDO: ffffe00013cae060
      IRP: ffffe0001049a5d0 (wait-wake/S0), PDO: ffffe00012d42050
      IRP: ffffe00013d07420 (set/D3,), PDO: ffffe00012daf840, CURRENT: ffffe00012dd5040
      IRP: ffffe0001e5ac5d0 (wait-wake/S0), PDO: ffffe00013d33060
      IRP: ffffe0001ed3e420 (wait-wake/S0), PDO: ffffe00013c96060
      IRP: ffffe000195fe010 (wait-wake/S0), PDO: ffffe00012d32050

    Irp worker threads (PopIrpThreadList - fffff801332f3100)
      THREAD: ffffe0000ef5d040 (static)
      THREAD: ffffe0000ef5e040 (static), IRP: ffffe00013d07420, DEVICE: ffffe00012dd5040
```

- KMDF ドライバーを使用する場合は、使用、 [Windows ドライバー フレームワークの拡張機能](kernel-mode-driver-framework-extensions--wdfkd-dll-.md)(! wdfkd) 追加情報を収集します。

  使用[ **! wdfkd.wdflogdump** ](-wdfkd-wdflogdump.md) &lt;、ドライバー名&gt;してかどうか KMDF を待機していることの確認保留中の要求を表示します。

  使用[ **! wdfkd.wdfdevicequeues** ](-wdfkd-wdfdevicequeues.md) &lt;、WDFDEVICE&gt;すべて未処理の要求とがどの状態を確認します。

- 使用して、 [ **! スタック**](-stacks.md)拡張機能をすべてのスレッドの状態を確認し、電源状態の遷移を保持するスレッドを探します。

- エラーの原因を特定するために、次の質問を考慮してください。

  -   物理デバイス オブジェクト (PDO) ドライバー (Arg2) の特性を挙げてください。
  -   ブロックされたスレッドを入手できますか。 スレッドを確認すると、 [ **! スレッド**](-thread.md)デバッガーのコマンドは、何がスレッドで構成されているのでしょうか。
  -   これをブロックしているスレッドに関連付けられた IO はありますか。 どのようなシンボルは、スタックにあるでしょうか。
  -   ブロックされている電源 IRP を確認するときにどのようなことがわかりますか。
  -   電源 IRP の PnP マイナー関数のコードとは何ですか。

**パラメーター 1 がの場合 0x4 0x9F のバグ チェックのデバッグ**

-   カーネル デバッガーを使用して、 [ **!-v を分析**](-analyze.md)初期のバグ チェックの分析を実行するコマンド。 詳細な分析のアドレスを表示する、 **nt!トリアージ\_9F\_PNP**パラメーター 4 (arg4) では、構造体。

```dbgcmd
    kd> !analyze -v
    *******************************************************************************
    *                                                                             *
    *                        Bugcheck Analysis                                    *
    *                                                                             *
    *******************************************************************************

    DRIVER_POWER_STATE_FAILURE (9f)
    A driver has failed to complete a power IRP within a specific time (usually 10 minutes).
    Arguments:
    Arg1: 00000004, The power transition timed out waiting to synchronize with the Pnp
            subsystem.
    Arg2: 00000258, Timeout in seconds.
    Arg3: 84e01a70, The thread currently holding on to the Pnp lock.
    Arg4: 82931b24, nt!TRIAGE_9F_PNP on Win7

```

Nt!トリアージ\_9F\_PNP 構造体は、参考に、エラーの原因を特定して追加のバグ チェック情報を提供します。 Nt!トリアージ\_9F\_PNP 構造がディスパッチされた (ただし、完了していません) の PnP Irp の一覧を格納し、遅延システム ワーカー キューへのポインターを提供する構造体へのポインターを提供します。

-  使用して、 [ **dt (表示の種類)** ](dt--display-type-.md)コマンドを指定、 **nt!トリアージ\_9F\_PNP**構造と Arg4 で見つけたアドレス。

```dbgcmd
    kd> dt nt!TRIAGE_9F_PNP 82931b24
       +0x000 Signature        : 0x8001
       +0x002 Revision         : 1
       +0x004 CompletionQueue  : 0x82970e20 _TRIAGE_PNP_DEVICE_COMPLETION_QUEUE
       +0x008 DelayedWorkQueue : 0x829455bc _TRIAGE_EX_WORK_QUEUE

```

[ **Dt (表示の種類)** ](dt--display-type-.md)コマンド構造を表示します。 デバッガー コマンドを使用するには、次の一覧を\_エントリ フィールドは、未処理の PnP Irp の一覧を確認します。

エラーの原因を特定するために、次の質問を考慮してください。

-  スレッドに関連付けられた IRP ではありますか。
-  CompletionQueue ですべての IO はありますか。
-  どのようなシンボルは、スタックにあるでしょうか。

-   パラメーター 0x3 上記で説明したその他の方法を参照してください。

**旅行時間のトレース**

バグ チェックはオンデマンドで再現できる場合は、WinDbg のプレビューを使用してタイム トラベル トレースを取ることの可能性を調査します。 詳細については、次を参照してください。[タイム トラベルのデバッグ - 概要](time-travel-debugging-overview.md)します。


## <a name="remarks"></a>注釈
----------

上記で説明した手法を使用してこの問題をデバッグする備えていない場合は、基本的なトラブルシューティングの手法を使用できます。

- 新しいデバイス ドライバまたはシステム サービスを最近では、追加されている場合を削除するか、それらを更新してみてください。 表示する新しいチェック コードをバグの原因となったシステムで変更内容を調べてください。

- 検索対象**デバイス マネージャー**を任意のデバイスの感嘆符 (!) が付いてを参照してください。 任意のエラーが発生したドライバーのドライバーのプロパティに表示されるイベント ログを確認します。 関連するドライバーを更新してみてください。

- デバイスまたはエラーの原因となっているドライバーの特定に役立つ可能性がある追加のエラー メッセージをイベント ビューアーのシステム ログを確認します。 詳細については、次を参照してください。[イベント ビューアーを開く](https://windows.microsoft.com/windows/what-information-event-logs-event-viewer#1TC=windows-7)します。 ブルー スクリーンに同じ期間に発生したシステム ログの重大なエラーを探します。

- 原因を特定して、コントロール パネルの 電源オプションを使用して省電力が一時的に無効にします。 ドライバーのいくつかの問題のシステムの休止状態と、中断と再開 power のさまざまな状態に関連しています。

- 最近削除または置換することをお試し、システムにハードウェアを追加した場合 または、更新プログラムが利用可能な製造元に確認します。

- システム製造元から提供されたハードウェア診断を実行して確認することができます。

- 更新されたシステム/の ACPI BIOS またはその他のファームウェアが使用できるかどうかを製造元に確認してください。
