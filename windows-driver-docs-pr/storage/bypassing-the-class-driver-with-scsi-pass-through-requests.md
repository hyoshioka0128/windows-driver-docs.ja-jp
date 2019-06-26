---
title: SCSI パススルー要求を使用したクラス ドライバーのバイパス
description: SCSI パススルー要求を使用したクラス ドライバーのバイパス
ms.assetid: 7f26e0bc-f01b-4430-aa9f-0f684fdbc2ec
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fe7404bb612d108552ef4e8c4a02361f680e9784
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368370"
---
# <a name="bypassing-the-class-driver-with-scsi-pass-through-requests"></a>SCSI パススルー要求を使用したクラス ドライバーのバイパス


## <span id="ddk_bypassing_the_class_driver_with_scsi_pass_through_requests_kg"></span><span id="DDK_BYPASSING_THE_CLASS_DRIVER_WITH_SCSI_PASS_THROUGH_REQUESTS_KG"></span>


ほとんどの場合は、クラス ドライバーは、SCSI ポートと上位レベルのドライバーとアプリケーション間のすべての通信を仲介します。 ただし、一部のターゲット デバイスは、クラス ドライバーを必要はありません。 このようなデバイス ドライバーは、「パススルー」要求と呼ばれる要求のクラスを使用して SCSI ポートと直接通信する必要があります。 パススルーの要求を使用するには、上位のコンポーネントはこれを行うには、クラス ドライバーに基づいて証明書利用者のではなく、CDB、要求で使用される設定に必須です。

SCSI パススルー要求から成る型 IRP の IRP\_MJ\_デバイス\_の IOCTL コードによるコントロール[ **IOCTL\_SCSI\_渡す\_経由**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddscsi/ni-ntddscsi-ioctl_scsi_pass_through)または[ **IOCTL\_SCSI\_渡す\_を通じて\_直接**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddscsi/ni-ntddscsi-ioctl_scsi_pass_through_direct)します。 クラスのドライバーが IRP を設定する義務はクラスのドライバーを介して、要求が成功した場合**MinorFunction**コード IRP を\_MJ\_デバイス\_コントロール。 SCSI ポートは、パススルー要求がクラス ドライバーをバイパスするかどうかを判断するには、この値を確認します。 記憶域クラス ドライバーによってターゲット デバイスが要求された場合は、SCSI ポートに直接パススルーの要求を送信するアプリケーション エラーになります。

SCSI ポートでは、パススルーの要求に埋め込まれている SCSI コマンドの有効性はチェックされません。

ストレージ クラス ドライバーの観点から SCSI パススルーの要求の詳細については、次を参照してください[SCSI パススルー要求の処理。](handling-scsi-pass-through-requests.md)

 

 




