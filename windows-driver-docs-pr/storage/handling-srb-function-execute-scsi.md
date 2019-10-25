---
title: SRB_FUNCTION_EXECUTE_SCSI の処理
description: SRB_FUNCTION_EXECUTE_SCSI の処理
ms.assetid: 221e1070-12d8-4870-a23c-426ed4a25b84
keywords:
- SCSI ミニポートドライバー WDK 記憶域、HwScsiStartIo
- HwScsiStartIo
- SRB_FUNCTION_EXECUTE_SCSI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 60ce582d44ec879b42c166c9bdc1fb42bd1a03cc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826240"
---
# <a name="handling-srb_function_execute_scsi"></a>SCSI\_実行\_SRB\_関数の処理


## <span id="ddk_handling_srb_function_execute_scsi_kg"></span><span id="DDK_HANDLING_SRB_FUNCTION_EXECUTE_SCSI_KG"></span>


上位レベルのストレージクラスドライバーが読み込まれた後、 [**HwScsiStartIo**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557323(v=vs.85))ルーチンに送信されるほとんどの SRBs では、**関数**メンバーが SRB\_\_関数に設定されて\_SCSI が実行されます。

\_SCSI 要求を実行\_SRB\_関数を受け取ると、ミニポートドライバーの*HwScsiStartIo*ルーチンは次のことを行います。

-   ミニポートドライバーがデバイス、論理ユニット、または SRB 拡張機能で保持するコンテキストを取得または設定します。

    たとえば、ミニポートドライバーでは、SRB 自体へのポインター、SRB **DataBuffer**ポインター、SRB **Datatransの長さ**の値、およびドライバーで定義された値 (または CDB SCSIOP\_*XXX*値) を含む論理ユニット拡張機能を設定する場合があります。HBA で実行される操作を示します。

-   要求された操作のために、内部ルーチンを呼び出して、 **Srbflags**によって部分的に指示された HBA をプログラミングします。

    デバイスの i/o 操作の場合、このような内部ルーチンは通常、ターゲットデバイスを選択し、バスを介してターゲット論理ユニットに CDB を送信します。

ミニポートドライバーがシステム DMA を使用する場合は、データを転送するために HBA をプログラミングする*前に* [**ScsiPortIoMapTransfer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportiomaptransfer)を呼び出す必要があります。 **ScsiPortIoMapTransfer**は、後で[SCSI ミニポートドライバーの HwScsiDmaStarted ルーチン](scsi-miniport-driver-s-hwscsidmastarted-routine.md)で説明されているように、システム DMA コントローラーを設定し、ミニポートドライバーの*HwScsiDmaStarted*ルーチンを呼び出します。

NT ベースのオペレーティングシステムストレージクラスに送信されるすべてのシステム定義の必須デバイス i/o 制御要求は、SRBs にマップされます。この**関数メンバーは**SRB\_関数に設定され、SCSI\_実行\_ます。

 

 




