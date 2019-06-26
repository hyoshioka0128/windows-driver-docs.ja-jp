---
title: Storport に SCSI パススルー要求クラス ドライバーをバイパスします。
description: Storport に SCSI パススルー要求クラス ドライバーをバイパスします。
ms.assetid: 1162a1e7-a4f8-446f-8106-527f9b916382
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 38ac6ba120790f9800eeed420e23bde4bfc7245d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362682"
---
# <a name="bypass-a-class-driver-with-scsi-pass-through-requests-to-storport"></a>Storport に SCSI パススルー要求クラス ドライバーをバイパスします。

ほとんどの場合、クラス ドライバーは、Storport と上位レベルのドライバーとアプリケーション間のすべての通信を仲介します。 ただし、一部のターゲット デバイスは、クラス ドライバーを必要はありません。 このようなデバイス ドライバーは、「パススルー」要求と呼ばれる要求のクラスを使用して、Storport と直接通信する必要があります。 パススルーの要求を使用するには、上位のコンポーネントはこれを行うには、クラス ドライバーに基づいて証明書利用者のではなく、CDB、要求で使用される設定に必須です。

クラス ドライバーが存在し、デバイスが要求を「パススルー」要求する必要がありますに送らクラス ドライバーによって、適切なデバイス ハンドルを開きます。 デバイスのクラス ドライバーがなく、デバイスが請求されていない場合は、し、「パススルー」要求を送信できます、アダプターに直接、適切なデバイス ハンドルを開くことで。

SCSI パススルー要求から成る型 IRP の IRP\_MJ\_デバイス\_の IOCTL コードを持つコントロール[ **IOCTL\_SCSI\_渡す\_を通じて** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddscsi/ni-ntddscsi-ioctl_scsi_pass_through)または[ **IOCTL\_SCSI\_渡す\_を通じて\_直接**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddscsi/ni-ntddscsi-ioctl_scsi_pass_through_direct)します。 クラスのドライバーに設定する義務はクラスのドライバーを介して、要求が成功した場合、 **MinorFunction** IRP に IRP のコード\_MJ\_デバイス\_コントロール。 Storport は、パススルー要求がクラス ドライバーをバイパスするかどうかを判断するには、この値を確認します。 記憶域クラス ドライバーによってターゲット デバイスが要求された場合に、Storport に直接パススルーの要求を送信するアプリケーション エラーになります。

Storport パススルー要求に埋め込まれている SCSI コマンドの有効性をチェックしません。

ストレージ クラス ドライバーの観点から SCSI パススルーの要求の詳細については、次を参照してください。 [SCSI パススルー要求の処理](handling-scsi-pass-through-requests.md)します。

 

 




