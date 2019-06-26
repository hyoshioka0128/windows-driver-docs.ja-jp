---
title: システム電源設定 IRP への応答におけるデバイス電源設定 IRP の送信
description: システム電源設定 IRP への応答におけるデバイス電源設定 IRP の送信
ms.assetid: b2029292-d770-4095-8bd7-9358b282216c
keywords:
- セット power Irp を送信します。
- セット power Irp WDK の電源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8e43072a78f8f01794e1f3db5466a035ea23328f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364090"
---
# <a name="sending-a-device-set-power-irp-in-response-to-a-system-set-power-irp"></a>システム電源設定 IRP への応答におけるデバイス電源設定 IRP の送信





デバイスの電源ポリシー所有者は、システムに応答する以下の手順を実行する必要があります IRP の出力を設定します。

1.  呼び出す[ **IoAcquireRemoveLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioacquireremovelock)、として現在 IRP を渡して、*タグ*パラメーターは、ドライバーがプラグ アンド プレイを受信しないことを確認する[ **IRP\_MN\_削除\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device) power IRP の処理中に要求します。

    場合**IoAcquireRemoveLock** 、エラー状態が返されるドライバーは IRP の処理を続行しないでください。 代わりに、Windows Vista 以降、ドライバー、呼び出す必要があります[ **IoCompleteRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)要求を完了し、エラー状態を返します。 Windows Server 2003、Windows XP、および Windows 2000 では、ドライバーは呼び出す必要がありますまず[ **PoStartNextPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-postartnextpowerirp)、呼び出す**IoCompleteRequest** IRP の完了にし、エラー状態を返します。

2.  呼び出すことによって、次の下位のドライバーの IRP スタックの場所を設定[ **IoCopyCurrentIrpStackLocationToNext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocopycurrentirpstacklocationtonext)します。

3.  設定、 [ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)システムで日常的な IRP の出力を設定します。

4.  呼び出す[ **IoMarkIrpPending** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iomarkirppending)システムをマークする保留中として設定 power IRP します。

5.  呼び出す[**保留**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver) (Windows Vista 以降) または[ **PoCallDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-pocalldriver) (Windows Server 2003、Windows XP、および Windows 2000) にするシステムに渡す次の下位のドライバー セット power IRP します。

6.  状態を返す\_PENDING からその[ *DispatchPower* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチン。

*IoCompletion*ルーチン (上記の手順 3 を参照します) デバイスの電源ポリシー所有者は、デバイスを送信します次のようにセット power IRP:。

1.  システムの検査セット power IRP を要求されたシステムの電源状態を取得します。 そのシステムの電源状態で、適切なデバイスの電源状態を選択します。 詳細については、次を参照してください。[正しいデバイスの電源状態を判断する](determining-the-correct-device-power-state.md)します。

2.  呼び出す[ **PoRequestPowerIrp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-porequestpowerirp)を送信する、 [ **IRP\_MN\_設定\_POWER** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)用、デバイスの電源状態がステップ 1 で決定されます。 電源ポリシー所有者は、デバイスがその状態で既に場合でもデバイス セット power 要求を送信する必要があります。

3.  電源完了コールバック ルーチンを指定 (*CompletionFunction*) への呼び出しで**PoRequestPowerIrp**させ、システムでセット power IRP、*コンテキスト*バッファー。

4.  状態を返す\_詳細\_処理\_から必要な*IoCompletion*ドライバーは、システムの処理を完了できるように日常的なセット power IRP power 完了コールバック ルーチンでします。

デバイスの電源ポリシーの所有者だけでなく、デバイスが送信ことに注意してくださいセット power IRP もデバイス スタックを介してやり取りする際に、この IRP を処理する必要があります。 その結果、デバイスの電源ポリシー所有者はだけでなく、デバイスに関連付けられた power 完了コールバック ルーチンを必要がありますセット power IRP と*IoCompletion*システムの日常的なセット power の IRP も、 *IoCompletion*デバイスの日常的な IRP の出力を設定します。 詳細については、次を参照してください。 [IRP の処理\_MN\_設定\_デバイスの電源状態のための電力](handling-irp-mn-set-power-for-device-power-states.md)します。

マネージャーはすべて、後の I/O、 *IoCompletion*セット power IRP を結ぶデバイス スタックをデバイスとして設定されたルーチンでは、I/O マネージャーが電源完了コールバック ルーチンを呼び出します。 この時点で、スタック内のすべてのドライバーがデバイスを完了したセット power IRP とデバイスの電源の移行が完了します。

電源完了コールバック ルーチンでは、次の操作を行う必要があります。

1.  呼び出す[ **PoStartNextPowerIrp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-postartnextpowerirp) IRP の [次へ] のパワーを開始します。 (Windows Server 2003、Windows XP、および Windows 2000 のみ。)

2.  システムを完了セット power IRP ([**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)) デバイスに対して返される状態 IRP の出力を設定します。

3.  呼び出す[ **IoReleaseRemoveLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioreleaseremovelock)を以前に取得したロックを解放します。

4.  セット power Irp の完了がステータスを返します。

 

 




