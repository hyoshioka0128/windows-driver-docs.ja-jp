---
title: SCSI ポート I/O モデル
description: SCSI ポート I/O モデル
ms.assetid: c79fdc99-30ae-4c4a-a130-2b8743bbff7f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c87f3c9203e3ab07955c6f9f6163c8b39278ddc0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842656"
---
# <a name="scsi-port-io-model"></a>SCSI ポート I/O モデル


## <span id="ddk_scsi_port_i_o_model_kg"></span><span id="DDK_SCSI_PORT_I_O_MODEL_KG"></span>


SCSI ポートドライバーは、そのディスパッチテーブルおよびドライバーオブジェクト内のミニポートドライバーコールバックルーチンへの一連のポインターを使用して、ミニポートドライバーと通信します。 ミニポートドライバーは、その[**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)ルーチンから[**ScsiPortInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportinitialize)を呼び出し、これらのコールバックポインターを使用して SCSI ポートのディスパッチテーブルとドライバーオブジェクトを初期化します。 このようなコールバックポインターの1つは、i/o 要求を処理するために使用されるミニポートドライバーの開始 i/o ルーチンのエントリポイントです。 ポートドライバーは、このポインターを driver オブジェクトの**DriverStartIo**メンバーに割り当てます。

SCSI ポートは、上位レベルのドライバーから i/o 要求を受信するたびに、内部キューで要求をキューに格納します。 SCSI ポートの内部キューの詳細については、「 [Scsi ポートドライバーのキュー管理](scsi-port-driver-s-queue-management.md)」を参照してください。

ターゲットデバイスが次の i/o 要求を受信する準備が整うと、SCSI ポートは[**Iostartpacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostartpacket)を呼び出します。これに**より、driverobject-&gt;DriverStartIo**に格納されているミニポートドライバーの開始 i/o コールバックルーチンが呼び出されます。 この操作およびミニポートドライバーの開始 i/o ルーチンの必要な特性の詳細については、「 [SCSI ミニポートドライバーの HwScsiStartIo ルーチン](scsi-miniport-driver-s-hwscsistartio-routine.md)」を参照してください。

SCSI ポートは、ミニポートドライバーの開始 i/o ルーチンを呼び出す前にプロセッサの IRQL を発生させます。これは、割り込みをマスクアウトし、開始 i/o ルーチンが重要なオペレーティングシステムとドライバー構造へのアクセスを同期していることを保証するために行います。

ストレージクラスドライバーと SCSI ポートドライバー間の i/o 要求パケットのフローは非同期ですが、SCSI ポートドライバーとターゲットデバイス間の i/o 要求パケットのフローは同期されています。 SCSI ポートは、前の i/o 要求が完了する前に、クラスドライバーが新しい i/o 要求を SCSI ポートに送信できるようにする内部キューシステムを使用します。 ただし、SCSI ポートは、ミニポートドライバーから次の i/o 要求を受信する準備ができていることをミニポートドライバーから受信するまで、次の i/o 要求をターゲットデバイスに送信しません。 ミニポートドライバーは、 [**ScsiPortNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportnotification)ライブラリルーチンを呼び出すことによって、SCSI ポートに通知します。

Storport ドライバーでは、特に割り込みのマスキングに関して、より柔軟な i/o モデルが提供されます。 Storport i/o モデルと SCSI ポート i/o モデルの違いについては、「 [storport I/o モデル](storport-i-o-model.md)」を参照してください。

 

 




