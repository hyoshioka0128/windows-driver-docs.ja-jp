---
title: バグチェック 0x9F DRIVER_POWER_STATE_FAILURE
description: このバグチェックの値は0x0000009F です。 このバグチェックは、ドライバーの電源状態が矛盾しているか、無効であることを示します。
ms.assetid: f767fe80-0ec0-45e4-9949-467f50ac601c
keywords:
- (開発者向けコンテンツ)バグチェック 0x9F DRIVER_POWER_STATE_FAILURE
- DRIVER_POWER_STATE_FAILURE
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- DRIVER_POWER_STATE_FAILURE
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8e9754dd7117a745e3d290a29fb54246db49390a
ms.sourcegitcommit: 667b4be765b2eac6bc586d39abef3393a718b23f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/30/2019
ms.locfileid: "70025315"
---
# <a name="developer-content-bug-check-0x9f-driver_power_state_failure"></a>(開発者向けコンテンツ)バグチェック 0x9F: ドライバー\_電源\_状態\_エラー

ドライバー\_電源\_状態\_エラーのバグチェックには、0x0000009F の値が含まれています。 このバグチェックは、ドライバーの電源状態が矛盾しているか、無効であることを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。

## <a name="driver_power_state_failure-parameters"></a>ドライバー\_電源\_状態\_エラーパラメーター

パラメーター1は違反の種類を示します。

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
<th align="left">パラメーター1</th>
<th align="left">パラメータ 2</th>
<th align="left">パラメーター3</th>
<th align="left">パラメーター4</th>
<th align="left">原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x1</p></td>
<td align="left"><p>デバイスオブジェクト</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>解放されているデバイスオブジェクトは、まだ完了していない未処理の電源要求を保持しています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x2</p></td>
<td align="left"><p>ターゲットデバイスのデバイスオブジェクト (使用可能な場合)</p></td>
<td align="left"><p>デバイスオブジェクト</p></td>
<td align="left"><p>ドライバーオブジェクト (使用可能な場合)</p></td>
<td align="left"><p>デバイスオブジェクトは、システム電源状態要求の i/o 要求パケット (IRP) を完了しましたが、 <strong>Postartnextpowerirp</strong>を呼び出しませんでした。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x3</p></td>
<td align="left"><p>スタックの物理デバイスオブジェクト (PDO)</p></td>
<td align="left"><p>スタックの機能デバイスオブジェクト (FDO)。 Windows 7 以降、nt!TRIAGE_9F_POWER。</p></td>
<td align="left"><p>ブロックされた IRP</p></td>
<td align="left"><p>デバイスオブジェクトが IRP を長時間ブロックしています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x4</p></td>
<td align="left"><p>タイムアウト値 (秒単位)。</p></td>
<td align="left"><p>現在、プラグアンドプレイ (PnP) ロックを保持しているスレッド。</p></td>
<td align="left"><p>Windows 7 以降、nt!TRIAGE_9F_POWER。</p></td>
<td align="left"><p>PnP サブシステムとの同期を待機中に、電源状態の移行がタイムアウトしました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x500</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>ターゲットデバイスのデバイスオブジェクト (使用可能な場合)</p></td>
<td align="left"><p>デバイスオブジェクト</p></td>
<td align="left"><p>デバイスオブジェクトはシステム電源状態要求の IRP を完了しましたが、 <strong>Postartnextpowerirp</strong>を呼び出しませんでした。</p></td>
</tr>
</tbody>
</table>

## <a name="cause"></a>原因
-----

考えられる原因の詳細については、「Parameters」セクションの各コードの説明を参照してください。

## <a name="resolution"></a>解決方法
----------

**パラメーター1が0x3 の場合のバグチェック0x9F のデバッグ**

- カーネルデバッガーでは、 [ **! analyze-v**](-analyze.md)コマンドを使用して、バグチェックの初期分析を実行します。 詳細分析では、nt のアドレスが表示されます **。トリアージ\_9F\_の電源**構造は、Arg3 にあります。

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

Nt!9F\_の\_のトリアージでは、このバグチェックの原因を特定するのに役立つ追加のバグチェック情報が提供されます。 構造体は、すべての未処理の電源 Irp の一覧、すべての power IRP ワーカースレッドの一覧、および遅延システムワーカーキューへのポインターを提供します。

- [**Dt (Display Type)** ](dt--display-type-.md)コマンドを使用し、nt! を指定します。Arg3 のアドレスを使用して、9F\_の電源構造をトリアージ\_ます。

```dbgcmd
    0: kd> dt nt!TRIAGE_9F_POWER fffff8000386c3d8
       +0x000 Signature        : 0x8000
       +0x002 Revision         : 1
       +0x008 IrpList          : 0xfffff800`01c78bd0 _LIST_ENTRY [ 0xfffffa80`09f43620 - 0xfffffa80`0ad00170 ]
       +0x010 ThreadList       : 0xfffff800`01c78520 _LIST_ENTRY [ 0xfffff880`009cdb98 - 0xfffff880`181f2b98 ]
       +0x018 DelayedWorkQueue : 0xfffff800`01c6d2d8 _TRIAGE_EX_WORK_QUEUE
```

[ [**Dt (Display Type)** ](dt--display-type-.md) ] コマンドを実行すると、構造が表示されます。 さまざまなデバッガーコマンドを使用して、リスト\_エントリフィールドに従って、未処理の Irp と power IRP ワーカースレッドの一覧を確認できます。

- [ **! Irp**](-irp.md)コマンドを使用して、ブロックされた irp を調べます。 この IRP のアドレスは、Arg4 にあります。

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

- [ **! Devstack**](-devstack.md)コマンドと、ARG2 の PDO アドレスを使用して、エラーが発生しているドライバーに関連付けられている情報を表示します。

```dbgcmd
    0: kd> !devstack fffffa8007b13440
      !DevObj           !DrvObj            !DevExt           ObjectName
      fffffa800783f060  \Driver\HidUsb     fffffa800783f1b0  InfoMask field not found for _OBJECT_HEADER at fffffa800783f030

    > fffffa8007b13440  \Driver\usbhub     fffffa8007b13590  Cannot read info offset from nt!ObpInfoMaskToOffset

    !DevNode fffffa8007ac8a00 :
      DeviceInst is "USB\VID_04D8&PID_0033\5&46fa7b7&0&1"
      ServiceName is "HidUsb"
```

- ! Poaction コマンドを使用して、電源操作と、割り当てられているすべての電源 Irp を処理するスレッドを表示します。

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

- KMDF ドライバーを使用している場合は、 [Windows Driver Framework Extensions](kernel-mode-driver-framework-extensions--wdfkd-dll-.md) (! wdfkd) を使用して追加情報を収集します。

  [ **! Wdfkd. wdflogdump**](-wdfkd-wdflogdump.md)を使用して、ドライバー名&gt;&lt;し、kmdf が保留中の要求を確認するまで待機しているかどうかを確認します。

  すべての未処理の要求とその状態を確認するには、wdfkd[**キュー**](-wdfkd-wdfdevicequeues.md)を使用して、wdfkd&gt; を使用します。&lt;

- [ **! Stacks**](-stacks.md)拡張機能を使用して、すべてのスレッドの状態を確認し、電源状態の遷移を保持している可能性のあるスレッドを探します。

- エラーの原因を特定するには、次の点を考慮してください。

  - 物理デバイスオブジェクト (PDO) ドライバー (Arg2) の特性はどのようなものですか。
  - ブロックされたスレッドを見つけることができますか。 スレッド[**デバッガーコマンドを使用して**](-thread.md)スレッドを調べると、スレッドはどのように構成されているのでしょうか。
  - ブロックしているスレッドに関連付けられている IO はありますか。 スタックにはどのようなシンボルがありますか。
  - ブロックされている電源 IRP を調べると、何がわかりますか。
  - Power IRP の PnP マイナー関数コードとは何ですか。

**パラメーター1が0x4 に等しい場合のバグチェック0x9F のデバッグ**

- カーネルデバッガーでは、 [ **! analyze-v**](-analyze.md)コマンドを使用して、バグチェックの初期分析を実行します。 詳細分析では、nt のアドレスが表示されます **。トリアージ\_** 、パラメーター 4 (arg4) にある 9F\_PNP 構造を指定します。

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

Nt!トリアージ\_9F\_PNP 構造により、エラーの原因を特定するのに役立つ追加のバグチェック情報が提供されます。 Nt!トリアージ\_9F\_PNP 構造体は、ディスパッチされた (未完了の) PnP Irp の一覧を含む構造体へのポインターを提供し、遅延したシステムワーカーキューへのポインターを提供します。

- [**Dt (Display Type)** ](dt--display-type-.md)コマンドを使用し、nt! を指定します **。9F\_PNP**構造と、Arg4 で見つかったアドレスをトリアージ\_ます。

```dbgcmd
    kd> dt nt!TRIAGE_9F_PNP 82931b24
       +0x000 Signature        : 0x8001
       +0x002 Revision         : 1
       +0x004 CompletionQueue  : 0x82970e20 _TRIAGE_PNP_DEVICE_COMPLETION_QUEUE
       +0x008 DelayedWorkQueue : 0x829455bc _TRIAGE_EX_WORK_QUEUE

```

[ [**Dt (Display Type)** ](dt--display-type-.md) ] コマンドを実行すると、構造が表示されます。 デバッガーコマンドを使用して、一覧の\_入力フィールドに従って、未処理の PnP Irp の一覧を確認できます。

エラーの原因を特定するには、次の点を考慮してください。

- スレッドに関連付けられている IRP があるかどうか。
- このキューには IO がありますか?
- スタックにはどのようなシンボルがありますか。

- 前述の「パラメーター0x3」で説明されている追加の手法を参照してください。

## <a name="remarks"></a>注釈
----------

上記の手法を使用してこの問題をデバッグすることができない場合は、いくつかの基本的なトラブルシューティング手法を使用できます。

- 新しいデバイスドライバーまたはシステムサービスが最近追加された場合は、それらを削除または更新してみてください。 新しいバグチェックコードが表示される原因となったシステムの変更内容を確認します。

- **デバイスマネージャー**を検索して、感嘆符 (!) でマークされているデバイスがあるかどうかを確認します。 [ドライバーのプロパティ] に表示されている、エラーが発生しているドライバーのイベントログを確認します。 関連するドライバーを更新してみてください。

- エラーの原因となっているデバイスまたはドライバーの特定に役立つ可能性のある追加のエラーメッセージについては、イベントビューアーのシステムログを確認してください。 詳細については、「 [Open イベントビューアー](https://support.microsoft.com/hub/4338813/windows-help#1TC=windows-7)」を参照してください。 ブルースクリーンと同じ時間枠内に発生したシステムログの重大なエラーを探します。

- 原因を特定するには、コントロールパネルの [電源オプション] を使用して一時的にを無効にします。 ドライバーに関するいくつかの問題は、システム休止状態のさまざまな状態と、電源の中断と再開に関連しています。

- 最近システムにハードウェアを追加した場合は、削除または交換してみてください。 または、製造元に確認して、修正プログラムが利用可能かどうかを確認してください。

- システムの製造元から提供されているハードウェア診断を実行できます。

- 製造元に確認して、更新されたシステム ACPI/BIOS またはその他のファームウェアが利用可能かどうかを確認してください。
