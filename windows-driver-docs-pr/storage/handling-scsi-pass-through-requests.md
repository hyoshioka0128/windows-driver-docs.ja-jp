---
title: SCSI パススルー要求の処理
description: SCSI パススルー要求の処理
ms.assetid: 61f8dc02-b5ae-4be5-b7e1-d8207304ef7c
keywords:
- 周辺機器 WDK ストレージ、SCSI パススルー要求
- ストレージ周辺機器 WDK、SCSI パススルー要求
- SCSI パススルー要求の WDK ストレージ
- パススルー要求 WDK ストレージ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a5a4c09f21d5d6f2ad5680fd59f63cb07949f499
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826266"
---
# <a name="handling-scsi-pass-through-requests"></a>SCSI パススルー要求の処理


## <span id="ddk_handling_scsi_pass_through_requests_kg"></span><span id="DDK_HANDLING_SCSI_PASS_THROUGH_REQUESTS_KG"></span>


要求を通じて\_を通過するか、 [ **\_直接要求によって\_渡される ioctl\_scsi**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddscsi/ni-ntddscsi-ioctl_scsi_pass_through_direct) [ **\_\_scsi**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddscsi/ni-ntddscsi-ioctl_scsi_pass_through)を生成するクラスドライバーは、次のことを担当します。

-   DeviceIoControl のユーザーバッファーの長さを、少なくとも**sizeof**(SCSI\_PASS\_経由) または**sizeof**(SCSI\_パス\_から\_DIRECT) に設定します **。**

-   通常どおりにストレージポートドライバーの i/o スタックの場所を設定する

-   IRP から IRP\_MJ\_デバイス\_コントロールの**Minorfunction**を設定すると、要求がストレージクラスドライバーによって処理されたものとしてマークされます。

\_または IOCTL\_SCSI\_\_SCSI を受信した場合、上位レベルのドライバーから\_直接要求を受けて\_を渡すと、記憶域クラスドライバーの[**DispatchDeviceControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンは、embedded SCSI コマンド (CDB) の有効性を確認し、コマンドがデバイスに対して有効な場合は、ストレージポートドライバーに要求を送信します。

IOCTL\_SCSI\_のポートドライバーの i/o スタックの場所が\_または IOCTL\_SCSI を通過する場合\_直接要求では、\_の**Minorfunction**フィールドが IRP\_MJ に設定されていません。デバイス\_制御\_、ポートドライバーは、要求がアプリケーションから直接送信されたものであり、ターゲットデバイスの種類にはクラスドライバーが存在しないと想定しています。 ストレージクラスドライバーによって要求されたデバイスのポートドライバーに、このような要求を直接送信するアプリケーションエラーです。

ポートドライバーは、このようなパススルー要求に埋め込まれている SCSI コマンドの有効性をチェックしません。

 

 




