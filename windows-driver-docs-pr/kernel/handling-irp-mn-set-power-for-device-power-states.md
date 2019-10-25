---
title: デバイス電源状態についての IRP_MN_SET_POWER の処理
description: デバイス電源状態についての IRP_MN_SET_POWER の処理
ms.assetid: b4a19995-7933-41f7-b951-15ce0e4627da
keywords:
- IRP_MN_SET_POWER
- デバイスの電源状態 WDK カーネル
- パワー Irp WDK カーネル
- DispatchPower ルーチン
- Irp をデバイススタック WDK に渡す
- デバイスセットの電源 Irp WDK カーネル
- 電源 Irp WDK カーネル、デバイスの変更
- ディスパッチルーチン WDK 電源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: a4ea2f4967b03e08ecbb3fdcc3f33b8d85b84ba6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838655"
---
# <a name="handling-irp_mn_set_power-for-device-power-states"></a>デバイスの電源状態の\_電力\_設定する IRP\_処理





デバイスセット-電源 IRP は、1つのデバイスの状態の変更を要求し、デバイスのスタック内のすべてのドライバーに送信されます。 このような IRP は、i/o スタックの場所の**DevicePowerState**メンバーにあるを指定**します。**

ドライバーは、スタック内を移動するときに、電源ダウン Irp を処理します。 電源設定の Irp の場合、ドライバーは、Irp がスタックを移動するときに[*Iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンを設定し、irp がスタックを移動するときに*iocompletion*ルーチンで irp を処理します。 一般的なデバイススタック内のドライバーは、次のようにデバイスの設定-電源 IRP を処理します。

-   ほとんどのフィルタードライバーは、 [**Iomarkirppending**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending)を呼び出し、IRP を次の下位のドライバーに渡し (「[電源 irp の受け渡し](passing-power-irps.md)」を参照)、 [*DISPATCHPOWER*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンから状態\_PENDING を返します。 ただし、フィルタードライバーによっては、着信 Irp のキューやデバイスの電源状態の保存など、デバイス固有のタスクを最初に実行する必要がある場合があります。

-   関数ドライバーは、 **Iomarkirppending**を呼び出し、デバイス固有のタスク (保留中の i/o 要求の完了、着信 i/o 要求のキュー、デバイスコンテキストの保存、デバイスの電源の変更など) を実行し、必要に応じて*iocompletion*ルーチンを設定します。とは、デバイスの電源 IRP を次の下位のドライバーに渡します (「[電源 irp の受け渡し](passing-power-irps.md)」を参照してください)。 *DispatchPower*ルーチンから状態\_PENDING が返されます。

-   バスドライバーは、可能であればデバイスの電源を変更した後、 [**PoSetPowerState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-posetpowerstate)を呼び出して、新しいデバイスの電源状態を電源マネージャーに通知します。 Windows Server 2003、Windows XP、および Windows 2000 でのみ、ドライバーは[**Postartnextpowerirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-postartnextpowerirp)を呼び出して、電源状態を設定した後、次の電源 IRP を開始する必要もあります。 次に、ドライバーは IRP を完了し、IO\_\_増分を指定します。 ドライバーが IRP をすぐに完了できない場合は、 [**Iomarkirppending**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending)を呼び出し、 *DISPATCHPOWER*ルーチンから状態\_PENDING を返し、後で irp を完了します。

ターゲットデバイスが既に要求された電源状態にある場合でも、各関数またはフィルタードライバーは、IRP を次の下位のドライバーに渡す必要があります。 すべての set-power IRP は、デバイススタックをすべて停止してから、バスドライバーを完了する必要があります。

バスドライバーの上に配置されている関数ドライバーとフィルタードライバーは、デバイスセットの電源 IRP を失敗させることはできません。 デバイスが取り外されているか、削除されている場合、バスドライバーはデバイスの電源投入の IRP を失敗させる可能性があります。

ドライバースタック内の各ドライバー (関数、フィルター、およびバスドライバー) は、対応するデバイスオブジェクトの電源状態の変化を電源マネージャーに通知するために、 [**PoSetPowerState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-posetpowerstate)を呼び出す必要があります。

デバイスの電源投入と電源切断に関連する他のドライバータスクと同様に、 **PoSetPowerState**の呼び出しは、デバイスの電源オン (新しい状態が D0 の場合) またはデバイスの電源オフ (新しい状態が他の状態の場合) の後に行われる必要があります。

各ドライバーは、デバイスの電源状態を追跡する必要があります。 この情報は、電源マネージャーによってドライバーに提供されません。

デバイスの電源状態に対する[**電源要求\_\_設定**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)された IRP\_処理中に、ドライバーはできるだけ早く*DispatchPower*ルーチンからを返します。 ドライバーは、同じ IRP を処理するコードによってシグナルされたカーネルイベントの*DispatchPower*ルーチンを待機することはできません。 システム全体で電源 Irp が同期されるため、デッドロックが発生する可能性があります。

特にマルチメディアアプリケーションで最高レベルのシステムパフォーマンスを確保するには、割り込み要求レベル (IRQL) がパッシブ\_レベルと同じになるように、ドライバーが時間のかかる操作を実行する必要があります。 IRQL = パッシブ\_レベルで操作を実行するには、ドライバーで[専用スレッド](device-dedicated-threads.md)または[システムワーカースレッド](system-worker-threads.md)を使用できます。 マルチメディアプラットフォームのドライバーパフォーマンスを最適化するためのガイドラインについては、[ストリーミングメディアデバイス設計ガイド](https://docs.microsoft.com/windows-hardware/drivers/stream/index)を参照してください。

次のセクションで説明するように、ドライバーが電源 IRP を処理するために必要な手順は、デバイスの電源が入っているかダウンしているかによって異なります。

[デバイスの電源ダウン Irp の処理](handling-device-power-down-irps.md)

[デバイスの電源の Irp を処理する](handling-device-power-up-irps.md)

 

 




