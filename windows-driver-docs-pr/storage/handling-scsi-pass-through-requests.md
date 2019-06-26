---
title: SCSI パススルー要求の処理
description: SCSI パススルー要求の処理
ms.assetid: 61f8dc02-b5ae-4be5-b7e1-d8207304ef7c
keywords:
- 記憶域 WDK 周辺機器、SCSI パススルー要求
- 記憶域周辺機器 WDK、SCSI パススルー要求
- SCSI パススルー要求 WDK ストレージ
- パススルー要求 WDK ストレージ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9c232392803ca359610f199dd644eb5022b3f0f5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378467"
---
# <a name="handling-scsi-pass-through-requests"></a>SCSI パススルー要求の処理


## <span id="ddk_handling_scsi_pass_through_requests_kg"></span><span id="DDK_HANDLING_SCSI_PASS_THROUGH_REQUESTS_KG"></span>


によって生成されるクラス ドライバー、 [ **IOCTL\_SCSI\_渡す\_を通じて**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddscsi/ni-ntddscsi-ioctl_scsi_pass_through)要求または[ **IOCTL\_SCSI\_渡す\_を通じて\_直接**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddscsi/ni-ntddscsi-ioctl_scsi_pass_through_direct)要求は、次を担当します。

-   ユーザー バッファーの長さを設定**Parameters.DeviceIoControl.InputBufferLength**に少なくとも**sizeof**(SCSI\_渡す\_を通じて) または**sizeof**(SCSI\_渡す\_を通じて\_ダイレクト)

-   通常どおり、記憶域ポート ドライバーの I/O スタックの場所の設定

-   設定、 **MinorFunction** IRP に IRP の\_MJ\_デバイス\_コントロールで、記憶域クラス ドライバーによって処理されたことと、要求をマークします。

IOCTL の受信時に\_SCSI\_渡す\_を通じてまたは IOCTL\_SCSI\_渡す\_を通じて\_上位レベルのドライバーを記憶域クラス ドライバーから直接要求[**DispatchDeviceControl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチンは、埋め込みの SCSI コマンド (CDB) の有効性をチェックすると、コマンドがそのデバイスに対して有効な場合は、記憶域ポート ドライバーに要求を送信します。

場合は、ポート ドライバーの I/O は、IOCTL の場所をスタック\_SCSI\_渡す\_を通じてまたは IOCTL\_SCSI\_渡す\_を通じて\_要求には、そのはありませんダイレクト **。MinorFunction**フィールド セット IRP\_MJ\_デバイス\_コントロール、ポート ドライバーは、アプリケーションから直接要求のソースとターゲット デバイスの種類のクラス ドライバーが存在しないこと. デバイスのストレージ クラス ドライバーによって要求されている場合、ポート ドライバーに直接このような要求を送信するアプリケーション エラーになります。

ポートのドライバーでは、このようなパススルー要求に埋め込まれている SCSI コマンドの有効性はチェックしません。

 

 




