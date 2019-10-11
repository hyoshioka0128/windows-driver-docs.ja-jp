---
title: SCSI ミニポート ドライバーの HwScsiAdapterControl ルーチン
description: SCSI ミニポート ドライバーの HwScsiAdapterControl ルーチン
ms.assetid: ccc5aa02-415d-40d1-a1ed-c7d4d881f4ca
keywords:
- SCSI ミニポートドライバー WDK 記憶域、HwScsiAdapterControl
- HwScsiAdapterControl
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1b16bc3dd0a92c41a20bd0f60e578f50b0c2cbae
ms.sourcegitcommit: 5f4252ee4d5a72fa15cf8c68a51982c2bc6c8193
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/10/2019
ms.locfileid: "72252460"
---
# <a name="scsi-miniport-drivers-hwscsiadaptercontrol-routine"></a>SCSI ミニポート ドライバーの HwScsiAdapterControl ルーチン

## <span id="ddk_scsi_miniport_drivers_hwscsiadaptercontrol_routine_kg"></span><span id="DDK_SCSI_MINIPORT_DRIVERS_HWSCSIADAPTERCONTROL_ROUTINE_KG"></span>

NT ベースのオペレーティングシステムでは、ミニポートドライバーでは、このエントリポイントを[**HW @ no__t-3INITIALIZATION @ no__t-4DATA (scsi)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/ns-srb-_hw_initialization_data)で**NULL**に設定する必要があります (「 [scsi ミニポートドライバールーチン](scsi-miniport-driver-routines.md)」を参照)。これは、ミニポートドライバーがプラグアンドプレイをサポートしていない場合です。 それ以外の場合、ミニポートドライバーには、その HBA の PnP および電源管理操作をサポートするための[**HwScsiAdapterControl**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557274(v=vs.85))ルーチンが必要です。

ミニポートドライバーの*HwScsiAdapterControl*ルーチンは、HBA が初期化された**後、** 最初の i/o の前に、ポートドライバーによって最初に呼び出され、ミニポートでサポートされている他の操作を決定します。driver. ミニポートドライバーは、ポートドライバーによって割り当てられた、サポートされている @ no__t-0CONTROL @ no__t-1TYPE @ no__t-2LIST でサポートされる操作を設定します。 この最初の呼び出しから*HwScsiAdapterControl*が戻った後、ポートドライバーはミニポートドライバーによって示された操作に対してのみルーチンを再度呼び出します。

ミニポートドライバーの*HwScsiAdapterControl*ルーチンでは、次の操作のいずれかまたはすべてをサポートできます。

-   **ScsiStopAdapter**は、電源がオフになっている、システムから削除された、または再構成または無効になったときに、HBA をシャットダウンします。

    SCSI ポートドライバーが*HwScsiAdapterControl*を呼び出して HBA を停止した時点で、完了していない要求がないことを確認します。 ミニポートドライバーは、HBA の割り込みを無効にし、割り込みの対象にならないバックグラウンド処理を含むすべての処理を停止し、その HBA を初期化されていない状態にします。 ミニポートドライバーは、そのリソースを解放しないでください。必要に応じて、ポートドライバーはミニポートドライバーに代わってリソースを解放します。 この*HwScsiAdapterControl*の呼び出しの前に SRB @ no__t 関数 @ NO__T-2flush 要求があるため、フラッシュ要求の完了後にデータが変更されていない限り、キャッシュをフラッシュする必要はありません。

    PnP マネージャーによって HBA の再起動が要求されるか、電源管理用にシャットダウンされた HBA の電源が入ってくるまで、この HBA に対してミニポートドライバーが再度呼び出されることはありません。

    HBA がシステムから既に削除された後、HBA を停止するために、ミニポートドライバールーチンと同様に*HwScsiAdapterControl*が呼び出される場合があることに注意してください。

-   **ScsiSetBootConfig**は、bios がシステムを起動するために必要とする可能性のある HBA の設定を復元します。

    このような設定を復元するために[**ScsiPortGetBusData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportgetbusdata)または[**ScsiPortSetBusDataByOffset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportsetbusdatabyoffset)を呼び出す必要がある場合は、ミニポートドライバーで**ScsiSetBootConfig**をサポートする必要があります。 ポートドライバーは、ルーチンを呼び出して HBA を停止した後、 **ScsiSetBootConfig**でミニポートドライバーの*HwScsiAdapterControl*を呼び出します。

-   **ScsiSetRunningConfig**は、システムの実行中にミニポートドライバーが hba の制御を必要とする可能性がある、hba の設定を復元します。

    このような設定を復元するために**ScsiPortGetBusData**または[**ScsiPortSetBusDataByOffset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportsetbusdatabyoffset)を呼び出す必要がある場合は、ミニポートドライバーで**ScsiSetRunningConfig**をサポートする必要があります。 ポートドライバーは、ルーチンを呼び出して HBA を再起動する前に、 **ScsiSetRunningConfig**でミニポートドライバーの*HwScsiAdapterControl*を呼び出します。

-   **ScsiRestartAdapter**は、電源管理用にシャットダウンされた HBA を再起動します。

    ポートドライバーが*HwScsiAdapterControl*を呼び出して HBA を再起動すると、そのミニポートドライバーに以前割り当てられていたすべてのリソースが引き続き使用可能で、そのデバイス拡張機能と論理ユニット拡張がすべてそのまま残ります。 HBA を再起動する場合、ミニポートドライバーは*HwScsiFindAdapter*からのみ呼び出すことができるルーチンを呼び出すことはできません。

    ミニポートドライバーが**ScsiRestartAdapter**をサポートしていない場合、ポートドライバーはミニポートドライバーの*HwScsiFindAdapter*と*HwScsiInitialize*ルーチンを呼び出して、HBA を再起動します。 ただし、このようなルーチンは、再起動時に不要な検出作業を行う場合があります。そのため、このようなミニポートドライバーは、 **ScsiRestartAdapter**をサポートするミニポートドライバーほど迅速に HBA の電源を投入しません。

詳細については、「 [**HwScsiAdapterControl**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557274(v=vs.85)) 」を参照してください。

 

 




