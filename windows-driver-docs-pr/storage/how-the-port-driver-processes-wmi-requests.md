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
ms.openlocfilehash: 3ea9f9bb0f6507048ee21111a68fb669b7431125
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570782"
---
# <a name="how-the-port-driver-processes-wmi-requests"></a>ポート ドライバーによる WMI 要求の処理方法


## <span id="ddk_how_the_port_driver_processes_wmi_requests_kg"></span><span id="DDK_HOW_THE_PORT_DRIVER_PROCESSES_WMI_REQUESTS_KG"></span>


Windows の種類の I/O 要求パケット (IRP) を送信することによって WMI 要求の記憶域ポート ドライバーに通知[ **IRP\_MJ\_システム\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff550813) 」の説明に従って、[Windows Management Instrumentation](https://msdn.microsoft.com/library/windows/hardware/ff547139)します。 IRP のシステム コントロールは、WMI の操作を表す IRP のマイナー番号のいずれかを含めることができます。 詳細については、次を参照してください。 [WMI マイナー Irp](https://msdn.microsoft.com/library/windows/hardware/ff566361)します。

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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551731" data-raw-source="[&lt;strong&gt;IRP_MN_REGINFO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551731)"><strong>IRP_MN_REGINFO</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff557344" data-raw-source="[&lt;strong&gt;HwScsiWmiQueryReginfo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557344)"><strong>HwScsiWmiQueryReginfo</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551650" data-raw-source="[&lt;strong&gt;IRP_MN_QUERY_ALL_DATA&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551650)"><strong>IRP_MN_QUERY_ALL_DATA</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff557340" data-raw-source="[&lt;strong&gt;HwScsiWmiQueryDataBlock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557340)"><strong>HwScsiWmiQueryDataBlock</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551718" data-raw-source="[&lt;strong&gt;IRP_MN_QUERY_SINGLE_INSTANCE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551718)"><strong>IRP_MN_QUERY_SINGLE_INSTANCE</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff557340" data-raw-source="[&lt;strong&gt;HwScsiWmiQueryDataBlock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557340)"><strong>HwScsiWmiQueryDataBlock</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550831" data-raw-source="[&lt;strong&gt;IRP_MN_CHANGE_SINGLE_INSTANCE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550831)"><strong>IRP_MN_CHANGE_SINGLE_INSTANCE</strong></a></p></td>
<td align="left"><p><em>HwScsiWmiSetDataBlock</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550836" data-raw-source="[&lt;strong&gt;IRP_MN_CHANGE_SINGLE_ITEM&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550836)"><strong>IRP_MN_CHANGE_SINGLE_ITEM</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff557357" data-raw-source="[&lt;strong&gt;HwScsiWmiSetDataItem&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557357)"><strong>HwScsiWmiSetDataItem</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550868" data-raw-source="[&lt;strong&gt;IRP_MN_EXECUTE_METHOD&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550868)"><strong>IRP_MN_EXECUTE_METHOD</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff557332" data-raw-source="[&lt;strong&gt;HwScsiWmiExecuteMethod&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557332)"><strong>HwScsiWmiExecuteMethod</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550859" data-raw-source="[&lt;strong&gt;IRP_MN_ENABLE_EVENTS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550859)"><strong>IRP_MN_ENABLE_EVENTS</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff557338" data-raw-source="[&lt;strong&gt;HwScsiWmiFunctionControl&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557338)"><strong>HwScsiWmiFunctionControl</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550851" data-raw-source="[&lt;strong&gt;IRP_MN_DISABLE_EVENTS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550851)"><strong>IRP_MN_DISABLE_EVENTS</strong></a></p></td>
<td align="left"><p><em>HwScsiWmiFunctionControl</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550857" data-raw-source="[&lt;strong&gt;IRP_MN_ENABLE_COLLECTION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550857)"><strong>IRP_MN_ENABLE_COLLECTION</strong></a></p></td>
<td align="left"><p><em>HwScsiWmiFunctionControl</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550848" data-raw-source="[&lt;strong&gt;IRP_MN_DISABLE_COLLECTION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550848)"><strong>IRP_MN_DISABLE_COLLECTION</strong></a></p></td>
<td align="left"><p><em>HwScsiWmiFunctionControl</em></p></td>
</tr>
</tbody>
</table>

 

各ミニポート ドライバー コールバック ルーチンが対応する WMI マイナー IRP に関連する機能を提供する必要があります番号。 一部のルーチンなど*HwScsiWmiFunctionControl*、いくつかの WMI マイナー IRP 番号に対応する機能を提供できる必要があります。

SCSI ポート WMI ライブラリのディスパッチ ルーチンを呼び出すには、ミニポート ドライバー [ **ScsiPortWmiDispatchFunction**](https://msdn.microsoft.com/library/windows/hardware/ff564766)、しディスパッチ ルーチンが、適切なミニポート ドライバー コールバック ルーチンを呼び出します。 ポートのドライバーは、ディスパッチ ルーチンを参照してください、SRB を呼び出すには、どのコールバック ルーチンを決定するように WMI マイナー IRP の番号を SRB に転送します。

次の図は、記憶域ミニポート ドライバーが SCSI ポート WMI ライブラリのディスパッチ ルーチンに渡すまでストレージ ポート ドライバー受信した時点から WMI 要求が行われます変更を示します。

![記憶域スタックが wmi の irp でどのように処理する方法 ](images/scsiwmilib.png)

1.  次の手順では、記憶域スタックが、SRB として WMI IRP に再パッケージについて説明します。

2.  Windows の種類の IRP を送信することによって WMI 要求の記憶域ポート ドライバーに通知[ **IRP\_MJ\_システム\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff550813)します。

3.  ポートのドライバーは IRP が WMI の種類の WMI SRB として[ **SCSIWMI\_要求\_コンテキスト**](https://msdn.microsoft.com/library/windows/hardware/ff564946) SRB の値が割り当てられます\_関数\_に WMISRB の**関数**メンバー。 WMI の IRP のマイナー番号を SRB に転送するポート ドライバー **WMISubFunction**メンバー。 呼び出す I/O マネージャー、ミニポート ドライバーの I/O ルーチンの開始を準備および[ **HwScsiStartIo** ](https://msdn.microsoft.com/library/windows/hardware/ff557323)への呼び出しによって[ **IoStartPacket** ](https://msdn.microsoft.com/library/windows/hardware/ff550370).

4.  ミニポート ドライバーは、SRB を処理するには、SCSI ポート WMI ライブラリ ディスパッチ ルーチンを呼び出します。 詳細については、次を参照してください。 [SCSI ポート WMI ライブラリを使用して](using-the-scsi-port-wmi-library.md)します。

 

 




