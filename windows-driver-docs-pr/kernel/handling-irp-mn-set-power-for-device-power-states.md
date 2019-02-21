---
title: デバイスの電源状態の IRP_MN_SET_POWER の処理
description: デバイスの電源状態の IRP_MN_SET_POWER の処理
ms.assetid: b4a19995-7933-41f7-b951-15ce0e4627da
keywords:
- IRP_MN_SET_POWER
- デバイスの電源状態の WDK カーネル
- セット power Irp WDK カーネル
- DispatchPower ルーチン
- デバイス スタック WDK ダウン Irp を渡す
- デバイスが電源 Irp WDK カーネルを設定
- 電源 Irp WDK カーネル、デバイスの変更
- ディスパッチ ルーチン WDK の電源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f80deda87b323aea0d72b09ec5f2c4af319d3186
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558223"
---
# <a name="handling-irpmnsetpower-for-device-power-states"></a>IRP の処理\_MN\_設定\_電源状態のデバイスの電源





デバイス セット power IRP が 1 つのデバイスの状態の変更を要求され、デバイスのスタック内のすべてのドライバーに送信されます。 このような IRP を指定します**DevicePowerState**で、 **Power.Type** I/O スタックの場所のメンバー。

下位のスタックを移動する、ドライバーは Irp の電源を処理します。 電源投入 Irp、ドライバーのセットの[ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354) Irp としてルーチンで、スタックへ移動で Irp を処理し、 *IoCompletion* Irp としてルーチンがバックアップに移動スタック。 一般的なデバイス スタック ハンドル、デバイスのドライバー セット power IRP を次に示します。

-   ほとんどのフィルター ドライバーは単に呼び出す必要があります[ **IoMarkIrpPending**](https://msdn.microsoft.com/library/windows/hardware/ff549422)、IRP を次の下位ドライバーに渡します (を参照してください[Power Irp を渡して](passing-power-irps.md))、状態を返すと\_保留中、 [ *DispatchPower* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチン。 一部のフィルター ドライバーは、キュー受信 Irp など、デバイスの電源状態を保存またはデバイスに固有のタスクを実行する必要があります最初。

-   関数のドライバーは呼び出し**IoMarkIrpPending**、完了する保留中の I/O 要求では、キューの受信 I/O 要求すると、デバイス コンテキストを保存またはデバイスの電源を変更する) などのデバイス固有のタスクを実行、設定、 *IoCompletion*ルーチンが必要に応じて、次の下位のドライバーにデバイスの電源 IRP を渡します (を参照してください[Power Irp を渡すこと](passing-power-irps.md))。 ステータスを返す\_PENDING からその*DispatchPower*ルーチン。

-   バス ドライバーの操作の対応である場合は、デバイスの電源を変更し、呼び出します[ **PoSetPowerState** ](https://msdn.microsoft.com/library/windows/hardware/ff559765)新しいデバイスの電源状態の電源マネージャーに通知します。 Windows Server 2003、Windows XP、および Windows 2000 でのみ、ドライバーは呼び出す必要がありますも[ **PoStartNextPowerIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff559776)電源の状態を設定した後、[次へ] のパワー IRP を開始します。 ドライバーが完了する IO を指定する、IRP\_いいえ\_インクリメントします。 呼び出す場合は、ドライバーは IRP をすぐに完了できず、 [ **IoMarkIrpPending**](https://msdn.microsoft.com/library/windows/hardware/ff549422)、ステータスを返します\_から PENDING その*DispatchPower*ルーチンとIRP を後で完了します。

場合でも、ターゲット デバイスは、要求された電源の状態では既に、各関数またはフィルター ドライバーは、次の下位ドライバーに IRP を渡す必要があります。 すべてセット power IRP は、これが完了すると、バス ドライバーにデバイス スタックの一番下出張する必要があります。

バス ドライバーの上に配置されている関数とフィルター ドライバーでは、デバイス セット power IRP が失敗する必要があります。 バス ドライバーには、デバイスが失敗する可能性がパワーアップ IRP、デバイスが削除された場合、または削除処理中です。

ドライバー スタックで各ドライバー (関数、フィルター、およびバス ドライバー) を呼び出す必要があります[ **PoSetPowerState** ](https://msdn.microsoft.com/library/windows/hardware/ff559765)対応するデバイス オブジェクトの電源状態が変更された電源マネージャーに通知します。

などのデバイスの電源投入し、電源オフへの呼び出しに関連付けられているその他のドライバー タスク**PoSetPowerState** (新しい状態が、D0) の場合、デバイスの電源投入後、または (新しい状態がその他の状態の場合)、デバイスが切れる前に行う必要があります。

各ドライバーする必要がありますの追跡、デバイスの電源の状態。 電源マネージャーは、ドライバーには、この情報を提供していません。

処理中に、 [ **IRP\_MN\_設定\_POWER** ](https://msdn.microsoft.com/library/windows/hardware/ff551744)からのデバイスの電源状態をドライバーの要求を返す必要があります、 *DispatchPower*できる限り迅速に日常的な。 ドライバーが待機する必要があります、 *DispatchPower*同じ IRP を処理するコードによってルーチンのカーネル イベントがシグナル状態します。 Power Irp がシステム全体で同期されるため、デッドロックが発生する可能性があります。

システム パフォーマンス、特にマルチ メディア アプリケーションの最高レベルを維持するドライバーがパッシブに等しい割り込み要求レベル (IRQL) で時間のかかる操作を実行する必要があります\_レベル。 IRQL で操作を実行するパッシブ =\_、ドライバーを使用して、レベル、[専用スレッド](device-dedicated-threads.md)または[システム ワーカー スレッド](system-worker-threads.md)します。 マルチ メディア プラットフォームに対するドライバーのパフォーマンスの最適化に関するガイドラインについては、次を参照してください。、[ストリーミング メディア デバイスの設計ガイド](https://msdn.microsoft.com/library/windows/hardware/ff568270)します。

次のセクションで説明したようにアップまたはスケール ダウン、デバイスの電源がかどうかによってドライバーが IRP の電源を処理するために実行する必要が正確な手順は異なります。

[デバイスの電源切断 Irp の処理](handling-device-power-down-irps.md)

[デバイスの電源投入 Irp の処理](handling-device-power-up-irps.md)

 

 




