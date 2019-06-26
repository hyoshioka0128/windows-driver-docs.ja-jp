---
title: WMI SRB をサポートするための記憶域ミニポート ドライバー ルーチンの変更
description: WMI SRB をサポートするための記憶域ミニポート ドライバー ルーチンの変更
ms.assetid: c3a222e8-dd02-4e45-b3e2-cec35d3abfdc
keywords:
- WMI される Srb WDK の記憶域をサポートするルーチンの変更
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d13ab66ddaed2a2e7c0fba641bb0aff3f534963d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386179"
---
# <a name="modifying-storage-miniport-driver-routines-to-support-wmi-srbs"></a>WMI SRB をサポートするための記憶域ミニポート ドライバー ルーチンの変更


## <span id="ddk_modifying_storage_miniport_driver_routines_to_support_wmi_srbs_kg"></span><span id="DDK_MODIFYING_STORAGE_MINIPORT_DRIVER_ROUTINES_TO_SUPPORT_WMI_SRBS_KG"></span>


ミニポート ドライバーでは、WMI される Srb をサポートできますが、前に、ミニポート ドライバーが必要なに含まれていることを確認する必要があります[ **HwScsiWmiQueryReginfo** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nc-scsiwmi-pscsiwmi_query_reginfo)ルーチンとに指定されたアクションが実行される、次のルーチン:

[ **SCSI ミニポート ドライバーの DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)ルーチン。

-   ミニポート ドライバーでは、SCSI ポート WMI ライブラリを使用する場合は、初期化、 [ **SCSI\_WMILIB\_コンテキスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/ns-scsiwmi-_scsiwmilib_context)に記載されている構造体[SCSI ポート WMI を使用ライブラリ](using-the-scsi-port-wmi-library.md)します。

-   ポート ドライバーに SRB の拡張機能のメモリを割り当てる必要があるかどうかを示します。 ミニポート ドライバーでは、SRB の拡張機能を設定して割り当てる必要があることを示します、 **SrbExtensionSize**のメンバー、 [ **HW\_初期化\_データ (SCSI)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/ns-srb-_hw_initialization_data) 0 以外の値構造体。

[ *HwScsiFindAdapter* ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557300(v=vs.85))ルーチン。

-   設定、 **WmiDataProvider**のメンバー、 [**ポート\_構成\_情報 (SCSI)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/ns-srb-_port_configuration_information)構造体と等しい**は TRUE。** .

[ **HwScsiStartIo** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557323(v=vs.85))ルーチン。

-   テスト**関数**SRB と等しいかどうかを SRB のメンバー\_関数\_WMI します。 この条件は、場合**TRUE**、ミニポート ドライバーは、SRB の型を処理する必要があります[ **SCSI\_WMI\_要求\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/ns-srb-_scsi_wmi_request_block)ではなく型の SRB より[ **SCSI\_要求\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/ns-srb-_scsi_request_block)します。

-   メモリを割り当てる、 [ **SCSIWMI\_要求\_コンテキスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/ns-scsiwmi-scsiwmi_request_context) SRB のコンテキストを保持する構造体。 場合は、ミニポート ドライバーには、WMI 要求の保留が可能性があります、ミニポート ドライバーが、SRB の処理全体での要求コンテキストを維持できるように、SRB の拡張機能からメモリを割り当てます。 それ以外の場合、要求は、これまで保留にする可能性がない場合、スタックからコンテキストのメモリを割り当てます。

-   確認**Srb**-&gt;**WMIFlags**要求が、アダプターまたは論理ユニットのかどうかを判断します。

-   SCSI ポート WMI ライブラリのディスパッチ ルーチンを呼び出す[ **ScsiPortWmiDispatchFunction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nf-scsiwmi-scsiportwmidispatchfunction)します。 このディスパッチ ルーチンを呼び出す方法の詳細については、次を参照してください。 [SCSI ポート WMI ライブラリを使用して](using-the-scsi-port-wmi-library.md)します。

-   呼び出す[ **ScsiPortWmiPostProcess** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nf-scsiwmi-scsiportwmipostprocess)ドライバーによって保留された場合、要求を処理した後。 かどうか、ドライバーが保留されません、要求し**ScsiPortWmiPostProcess**ミニポート ドライバーの I/O ルーチンを開始するのではなく、ミニポート ドライバー コールバック ルーチンを呼び出す必要があります。

-   設定**Srb**-&gt;**DataTransferLength**と**Srb**-&gt;**SrbStatus**によって返される値に[ **ScsiPortWmiGetReturnSize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nf-scsiwmi-scsiportwmigetreturnsize)と[ **ScsiPortWmiGetReturnStatus** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nf-scsiwmi-scsiportwmigetreturnstatus)それぞれします。

-   呼び出す[ **ScsiPortNotification** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportnotification)で**RequestComplete**ときのこ**NextRequest**または (**NextLuRequest**).

 

 




