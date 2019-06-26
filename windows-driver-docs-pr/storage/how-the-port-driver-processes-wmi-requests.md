---
title: ポート ドライバーによる WMI 要求の処理方法
description: ポート ドライバーによる WMI 要求の処理方法
ms.assetid: 0b56d382-3c4b-4192-be49-3bad50b0a0ed
keywords:
- WMI される Srb WDK ストレージ、WMI 要求の処理
- コールバック ルーチン WDK WMI される Srb
- WMI の Irp WDK ストレージ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 52b34b9fd955e4f4a181ceeebb326386a816f18a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385950"
---
# <a name="how-the-port-driver-processes-wmi-requests"></a>ポート ドライバーによる WMI 要求の処理方法


## <span id="ddk_how_the_port_driver_processes_wmi_requests_kg"></span><span id="DDK_HOW_THE_PORT_DRIVER_PROCESSES_WMI_REQUESTS_KG"></span>


Windows の種類の I/O 要求パケット (IRP) を送信することによって WMI 要求の記憶域ポート ドライバーに通知[ **IRP\_MJ\_システム\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-system-control) 」の説明に従って、[Windows Management Instrumentation](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-wmi)します。 IRP のシステム コントロールは、WMI の操作を表す IRP のマイナー番号のいずれかを含めることができます。 詳細については、次を参照してください。 [WMI マイナー Irp](https://docs.microsoft.com/windows-hardware/drivers/kernel/wmi-minor-irps)します。

使用する、 [SCSI ポート WMI ライブラリを使用して](using-the-scsi-port-wmi-library.md)WMI される Srb を処理する、SCSI ミニポート ドライバーは、WMI マイナー IRP の番号を一連の対応するコールバック ルーチンを提供する必要があります。 次の表は、ミニポート ドライバーのコールバック ルーチンと対応する WMI マイナー IRP 番号間のリレーションシップを示しています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">WMI の IRP のマイナー番号</th>
<th align="left">ミニポート ドライバー コールバック ルーチン</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-reginfo" data-raw-source="[&lt;strong&gt;IRP_MN_REGINFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-reginfo)"><strong>IRP_MN_REGINFO</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nc-scsiwmi-pscsiwmi_query_reginfo" data-raw-source="[&lt;strong&gt;HwScsiWmiQueryReginfo&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nc-scsiwmi-pscsiwmi_query_reginfo)"><strong>HwScsiWmiQueryReginfo</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-all-data" data-raw-source="[&lt;strong&gt;IRP_MN_QUERY_ALL_DATA&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-all-data)"><strong>IRP_MN_QUERY_ALL_DATA</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nc-scsiwmi-pscsiwmi_query_datablock" data-raw-source="[&lt;strong&gt;HwScsiWmiQueryDataBlock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nc-scsiwmi-pscsiwmi_query_datablock)"><strong>HwScsiWmiQueryDataBlock</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-single-instance" data-raw-source="[&lt;strong&gt;IRP_MN_QUERY_SINGLE_INSTANCE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-single-instance)"><strong>IRP_MN_QUERY_SINGLE_INSTANCE</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nc-scsiwmi-pscsiwmi_query_datablock" data-raw-source="[&lt;strong&gt;HwScsiWmiQueryDataBlock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nc-scsiwmi-pscsiwmi_query_datablock)"><strong>HwScsiWmiQueryDataBlock</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-change-single-instance" data-raw-source="[&lt;strong&gt;IRP_MN_CHANGE_SINGLE_INSTANCE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-change-single-instance)"><strong>IRP_MN_CHANGE_SINGLE_INSTANCE</strong></a></p></td>
<td align="left"><p><em>HwScsiWmiSetDataBlock</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-change-single-item" data-raw-source="[&lt;strong&gt;IRP_MN_CHANGE_SINGLE_ITEM&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-change-single-item)"><strong>IRP_MN_CHANGE_SINGLE_ITEM</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nc-scsiwmi-pscsiwmi_set_dataitem" data-raw-source="[&lt;strong&gt;HwScsiWmiSetDataItem&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nc-scsiwmi-pscsiwmi_set_dataitem)"><strong>HwScsiWmiSetDataItem</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-execute-method" data-raw-source="[&lt;strong&gt;IRP_MN_EXECUTE_METHOD&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-execute-method)"><strong>IRP_MN_EXECUTE_METHOD</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nc-scsiwmi-pscsiwmi_execute_method" data-raw-source="[&lt;strong&gt;HwScsiWmiExecuteMethod&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nc-scsiwmi-pscsiwmi_execute_method)"><strong>HwScsiWmiExecuteMethod</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-enable-events" data-raw-source="[&lt;strong&gt;IRP_MN_ENABLE_EVENTS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-enable-events)"><strong>IRP_MN_ENABLE_EVENTS</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nc-scsiwmi-pscsiwmi_function_control" data-raw-source="[&lt;strong&gt;HwScsiWmiFunctionControl&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nc-scsiwmi-pscsiwmi_function_control)"><strong>HwScsiWmiFunctionControl</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-disable-events" data-raw-source="[&lt;strong&gt;IRP_MN_DISABLE_EVENTS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-disable-events)"><strong>IRP_MN_DISABLE_EVENTS</strong></a></p></td>
<td align="left"><p><em>HwScsiWmiFunctionControl</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-enable-collection" data-raw-source="[&lt;strong&gt;IRP_MN_ENABLE_COLLECTION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-enable-collection)"><strong>IRP_MN_ENABLE_COLLECTION</strong></a></p></td>
<td align="left"><p><em>HwScsiWmiFunctionControl</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-disable-collection" data-raw-source="[&lt;strong&gt;IRP_MN_DISABLE_COLLECTION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-disable-collection)"><strong>IRP_MN_DISABLE_COLLECTION</strong></a></p></td>
<td align="left"><p><em>HwScsiWmiFunctionControl</em></p></td>
</tr>
</tbody>
</table>

 

各ミニポート ドライバー コールバック ルーチンが対応する WMI マイナー IRP に関連する機能を提供する必要があります番号。 一部のルーチンなど*HwScsiWmiFunctionControl*、いくつかの WMI マイナー IRP 番号に対応する機能を提供できる必要があります。

SCSI ポート WMI ライブラリのディスパッチ ルーチンを呼び出すには、ミニポート ドライバー [ **ScsiPortWmiDispatchFunction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nf-scsiwmi-scsiportwmidispatchfunction)、しディスパッチ ルーチンが、適切なミニポート ドライバー コールバック ルーチンを呼び出します。 ポートのドライバーは、ディスパッチ ルーチンを参照してください、SRB を呼び出すには、どのコールバック ルーチンを決定するように WMI マイナー IRP の番号を SRB に転送します。

次の図は、記憶域ミニポート ドライバーが SCSI ポート WMI ライブラリのディスパッチ ルーチンに渡すまでストレージ ポート ドライバー受信した時点から WMI 要求が行われます変更を示します。

![記憶域スタックが wmi の irp でどのように処理する方法 ](images/scsiwmilib.png)

1.  次の手順では、記憶域スタックが、SRB として WMI IRP に再パッケージについて説明します。

2.  Windows の種類の IRP を送信することによって WMI 要求の記憶域ポート ドライバーに通知[ **IRP\_MJ\_システム\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-system-control)します。

3.  ポートのドライバーは IRP が WMI の種類の WMI SRB として[ **SCSIWMI\_要求\_コンテキスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/ns-scsiwmi-scsiwmi_request_context) SRB の値が割り当てられます\_関数\_に WMISRB の**関数**メンバー。 WMI の IRP のマイナー番号を SRB に転送するポート ドライバー **WMISubFunction**メンバー。 呼び出す I/O マネージャー、ミニポート ドライバーの I/O ルーチンの開始を準備および[ **HwScsiStartIo** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557323(v=vs.85))への呼び出しによって[ **IoStartPacket** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iostartpacket).

4.  ミニポート ドライバーは、SRB を処理するには、SCSI ポート WMI ライブラリ ディスパッチ ルーチンを呼び出します。 詳細については、次を参照してください。 [SCSI ポート WMI ライブラリを使用して](using-the-scsi-port-wmi-library.md)します。

 

 




