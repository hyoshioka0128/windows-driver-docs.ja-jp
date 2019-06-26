---
title: IRP_MN_CANCEL_STOP_DEVICE 要求の処理 (Windows 98/Me)
description: IRP_MN_CANCEL_STOP_DEVICE 要求の処理 (Windows 98/Me)
ms.assetid: 04365c65-a68a-48fc-9f7a-bb005518be5b
keywords:
- IRP_MN_CANCEL_STOP_DEVICE
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: d35c35dbedfaacc8c20a05b2fc1ffb3b458ec2e6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384234"
---
# <a name="handling-an-irpmncancelstopdevice-request-windows-98me"></a>IRP の処理\_MN\_キャンセル\_停止\_デバイス要求 (Windows 98/Me)





[ **IRP\_MN\_キャンセル\_停止\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-cancel-stop-device)デバイスの親のバス ドライバー、続いて各次に要求を最初に処理する必要があります高いデバイス スタックのドライバーです。 ドライバーのハンドルに Irp の停止、 [ *DispatchPnP* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチン。

応答、 **IRP\_MN\_キャンセル\_停止\_デバイス**要求、ドライバーは、デバイスを開始状態に戻すし、通常の操作を再開する必要があります。 ドライバーは、キャンセル停止 IRP を成功する必要があります。

ドライバーの処理、 **IRP\_MN\_キャンセル\_停止\_デバイス**次のようなプロシージャを使って要求。

1.  下位のドライバーには、再起動操作が完了するまで、デバイスの再起動を延期します。 (を参照してください[下位のドライバーが完了するまで、PnP IRP の処理を延期する](postponing-pnp-irp-processing-until-lower-drivers-finish.md))。

2.  下位のドライバーが完了すると、デバイスを開始状態に戻します。

    正確な操作は、デバイスとドライバーによって異なります。

3.  I/O を再起動します。

4.  完了の IRP [ **IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)します。

    -   関数またはフィルター ドライバーでは。

        ドライバーの*IoCompletion*ルーチンには、状態が返されました\_詳細\_処理\_」の説明に従って、必要な[を延期する PnP IRP の処理まで低いドライバー完了。](postponing-pnp-irp-processing-until-lower-drivers-finish.md)ため、ドライバーの*DispatchPnP*ルーチンを呼び出す必要があります**IoCompleteRequest** I/O 完了処理を再開します。

        ドライバー セット**Irp -&gt;IoStatus.Status**ステータス\_成功すると、呼び出し**IoCompleteRequest** IO の優先順位を上げると\_いいえ\_インクリメント、ステータスを返す\_成功からその*DispatchPnP*ルーチン。

        ドライバーでは、この操作は失敗する必要があります。 ドライバーが IRP の再起動に失敗した場合、デバイスは不整合な状態でありは正しく動作しません。

    -   親のバス ドライバーの場合。

        ドライバー セット**Irp -&gt;IoStatus.Status**ステータス\_成功と呼び出し**IoCompleteRequest** IO の優先順位を指定する\_いいえ\_増分値です。 バス ドライバーのステータスを返します\_成功からその*DispatchPnP*ルーチン。

        バス ドライバーでは、この操作は失敗する必要があります。 ドライバーが IRP の再起動に失敗した場合、デバイスは不整合な状態でありは正しく動作しません。

ドライバーは、デバイスが開始され、アクティブなときに、誤ったキャンセル停止要求にすることがあります。 これが行われる、たとえば、ドライバー (またはデバイス履歴の上位にドライバー) が失敗した場合、 [ **IRP\_MN\_クエリ\_停止\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-stop-device)要求。 デバイスが開始され、アクティブなとき、ドライバーは、デバイスの誤ったキャンセル停止要求に成功安全になります。

 

 




