---
title: WMI SRB をサポートするための記憶域ミニポート ドライバー ルーチンの変更
description: WMI SRB をサポートするための記憶域ミニポート ドライバー ルーチンの変更
ms.assetid: c3a222e8-dd02-4e45-b3e2-cec35d3abfdc
keywords:
- WMI SRBs WDK storage、サポートするルーチンの変更
ms.date: 10/08/2019
ms.localizationpriority: medium
ms.openlocfilehash: 70c268140086c01a1d72eb89ed5d87e3af41271b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841610"
---
# <a name="modifying-storage-miniport-driver-routines-to-support-wmi-srbs"></a>WMI SRB をサポートするための記憶域ミニポート ドライバー ルーチンの変更

ミニポートドライバーが WMI SRBs をサポートできるようにするには、ミニポートドライバーに必要な[*HwScsiWmiQueryReginfo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/scsiwmi/nc-scsiwmi-pscsiwmi_query_reginfo)ルーチンが含まれていること、および次のルーチンに対して指定されたアクションを実行していることを確認する必要があります。

[**SCSI ミニポートドライバールーチンの Driverentry**](driverentry-of-scsi-miniport-driver.md) :

- ミニポートドライバーが SCSI ポート WMI ライブラリを使用している場合は、「 [Scsi ポート Wmi ライブラリの使用](using-the-scsi-port-wmi-library.md)」に示されているように、 [SCSI_WMILIB_CONTEXT](https://docs.microsoft.com/windows-hardware/drivers/ddi/scsiwmi/ns-scsiwmi-_scsiwmilib_context)構造体を初期化します。

- SRB 拡張にメモリを割り当てる必要があるかどうかをポートドライバーに指示します。 ミニポートドライバーは、 [**HW_INITIALIZATION_DATA (SCSI)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/ns-srb-_hw_initialization_data)構造体の**Srbextensionsize**メンバーを0以外の値に設定することによって、SRB 拡張機能を割り当てる必要があることを示しています。

[*HwScsiFindAdapter*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557300(v=vs.85))ルーチン:

- [PORT_CONFIGURATION_INFORMATION (SCSI)](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/ns-srb-_port_configuration_information)構造体の [設定] の [構成 **] メンバーを** **TRUE**に設定します。

[*HwScsiStartIo*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557323(v=vs.85))ルーチン:

- SRB の**関数**メンバーをテストして、SRB_FUNCTION_WMI と等しいかどうかを確認します。 この条件が**TRUE**の場合、ミニポートドライバーは、種類が[**SCSI_REQUEST_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/ns-srb-_scsi_request_block)の SRB ではなく[**SCSI_WMI_REQUEST_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/ns-srb-_scsi_wmi_request_block)型の SRB を処理する必要があります。

- SRB CONTEXT を保持する[SCSIWMI_REQUEST_CONTEXT](https://docs.microsoft.com/windows-hardware/drivers/ddi/scsiwmi/ns-scsiwmi-scsiwmi_request_context)構造体にメモリを割り当てます。 ミニポートドライバーが WMI 要求を保留する場合は、SRB 拡張機能からメモリを割り当てて、ミニポートドライバーが SRB の処理中に要求コンテキストを維持できるようにします。 それ以外の場合、要求が保留される可能性がない場合は、スタックからコンテキストのメモリを割り当てます。

- **> Srb**を確認して、要求がアダプターまたは論理ユニットのどちらであるかを判断します。

- SCSI ポート WMI ライブラリディスパッチルーチン、 [**ScsiPortWmiDispatchFunction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/scsiwmi/nf-scsiwmi-scsiportwmidispatchfunction)を呼び出します。 このディスパッチルーチンを呼び出す方法の詳細については、「 [SCSI ポート WMI ライブラリの使用](using-the-scsi-port-wmi-library.md)」を参照してください。

- 要求がドライバーによって保留されている場合は、要求の処理後に[**ScsiPortWmiPostProcess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/scsiwmi/nf-scsiwmi-scsiportwmipostprocess)を呼び出します。 ドライバーが要求を保留していない場合は、ミニポートドライバーの開始 i/o ルーチンではなく、ミニポートドライバーのコールバックルーチンで**ScsiPortWmiPostProcess**を呼び出す必要があります。

- **Srb-> DatatransSrb length**と **> srbstatus**をそれぞれ[**ScsiPortWmiGetReturnSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/scsiwmi/nf-scsiwmi-scsiportwmigetreturnsize)と[**ScsiPortWmiGetReturnStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/scsiwmi/nf-scsiwmi-scsiportwmigetreturnstatus)によって返される値に設定します。

- **Requestcomplete**と**nextrequest**または (**nextlurequest**) を使用して、 [**ScsiPortNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportnotification)を呼び出します。
