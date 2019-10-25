---
title: SCSI パススルー要求を使用したクラス ドライバーのバイパス
description: SCSI パススルー要求を使用したクラス ドライバーのバイパス
ms.assetid: 7f26e0bc-f01b-4430-aa9f-0f684fdbc2ec
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 46668169e6911e62dc4cbccee4f507643d72cca6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845095"
---
# <a name="bypassing-the-class-driver-with-scsi-pass-through-requests"></a>SCSI パススルー要求を使用したクラス ドライバーのバイパス


## <span id="ddk_bypassing_the_class_driver_with_scsi_pass_through_requests_kg"></span><span id="DDK_BYPASSING_THE_CLASS_DRIVER_WITH_SCSI_PASS_THROUGH_REQUESTS_KG"></span>


ほとんどの場合、クラスドライバーは SCSI ポートと上位レベルのドライバーおよびアプリケーション間のすべての通信を仲介します。 ただし、一部のターゲットデバイスにはクラスドライバーがありません。 このようなデバイスのドライバーは、"パススルー" 要求と呼ばれる要求のクラスを使用して、SCSI ポートと直接通信する必要があります。 パススルー要求を使用するには、クラスドライバーに依存せずに、要求で使用される CDB を設定するために、上位レベルのコンポーネントが必要です。

SCSI パススルー要求は、irp の種類が irp\_MJ\_デバイス\_コントロールであり、ioctl の ioctl コードを使用して[ **\_scsi\_パス\_経由**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddscsi/ni-ntddscsi-ioctl_scsi_pass_through)または ioctl\_を通過\_[ **\_DIRECT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddscsi/ni-ntddscsi-ioctl_scsi_pass_through_direct)。 要求がクラスドライバーを介して渡される場合、クラスドライバーは、IRP の**Minorfunction**コードを IRP\_MJ\_デバイス\_コントロールに設定する義務があります。 SCSI ポートは、この値をチェックして、パススルー要求がクラスドライバーをバイパスしたかどうかを判断します。 ターゲットデバイスがストレージクラスドライバーによって要求されている場合、パススルー要求を直接 SCSI ポートに送信するアプリケーションエラーです。

SCSI ポートは、パススルー要求に埋め込まれている SCSI コマンドの有効性をチェックしません。

ストレージクラスドライバーから見た SCSI パススルー要求の詳細については、「 [Scsi パススルー要求の処理](handling-scsi-pass-through-requests.md)」を参照してください。

 

 




