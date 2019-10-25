---
title: WDM リーダー ドライバー
description: WDM リーダー ドライバー
ms.assetid: ead76f5f-1d28-4343-99c0-e7974fa4c3da
keywords:
- ベンダー提供のドライバー WDK スマートカード、必須ルーチン
- WDM WDK スマートカード
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 191d39bc0cca370677add795636a09328d9ad75a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842612"
---
# <a name="wdm-reader-driver"></a>WDM リーダー ドライバー


## <span id="_ntovr_wdm_reader_driver"></span><span id="_NTOVR_WDM_READER_DRIVER"></span>


次の表に、WDM リーダードライバーで必要とされるルーチンの一覧を示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ルーチン</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize" data-raw-source="[&lt;strong&gt;DriverEntry&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)"><strong>DriverEntry</strong></a></p></td>
<td align="left"><p>ドライバーオブジェクトとディスパッチテーブルを初期化します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device" data-raw-source="[&lt;em&gt;AddDevice&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)"><em>AddDevice</em></a></p></td>
<td align="left"><p>スマートカードリーダーのデバイスオブジェクトを作成します。 また、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device" data-raw-source="[&lt;em&gt;AddDevice&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)"><em>AddDevice</em></a>は、次のいずれかのドライバーライブラリルーチンを呼び出すことができます。</p>
<ul>
<li><p><a href="https://docs.microsoft.com/previous-versions/ff548944(v=vs.85)" data-raw-source="[&lt;strong&gt;SmartcardInitialize (WDM)&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff548944(v=vs.85))"><strong>Smartcardinitialize (WDM)</strong></a>を実行してドライバーの初期化を完了します。 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device" data-raw-source="[&lt;em&gt;AddDevice&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)"><em>AddDevice</em></a>でこのルーチンを呼び出すと、加えるになります。</p></li>
<li><p><a href="https://docs.microsoft.com/previous-versions/ff548947(v=vs.85)" data-raw-source="[&lt;strong&gt;SmartcardLogError (WDM)&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff548947(v=vs.85))"><strong>Smartcardlogerror (WDM)</strong></a>によってエラーがログに記録されます。 <a href="https://docs.microsoft.com/previous-versions/ff548944(v=vs.85)" data-raw-source="[&lt;strong&gt;SmartcardInitialize (WDM)&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff548944(v=vs.85))"><strong>Smartcardinitialize (WDM)</strong></a>が失敗した場合、ドライバーは<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device" data-raw-source="[&lt;em&gt;AddDevice&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)"><em>AddDevice</em></a>でこのルーチンを呼び出す必要があります。</p></li>
<li><p><a href="https://docs.microsoft.com/previous-versions/ff548935(v=vs.85)" data-raw-source="[&lt;strong&gt;SmartcardCreateLink (WDM)&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff548935(v=vs.85))"><strong>Smartcardcreatelink (WDM)</strong></a>を使用して、レジストリにリーダーデバイスのシンボリックリンクを作成します。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload" data-raw-source="[&lt;em&gt;Unload&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)"><em>取り除き</em></a></p></td>
<td align="left"><p>システムからドライバーを削除します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543266" data-raw-source="[&lt;em&gt;DispatchCreate&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543266)"><em>DispatchCreate</em></a></p>
<p>および</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch" data-raw-source="[&lt;em&gt;DispatchClose&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)"><em>DispatchClose</em></a></p></td>
<td align="left"><p>では、 <a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-create" data-raw-source="[&lt;strong&gt;IRP_MJ_CREATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-create)"><strong>IRP_MJ_CREATE</strong></a>と<a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-close" data-raw-source="[&lt;strong&gt;IRP_MJ_CLOSE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-close)"><strong>IRP_MJ_CLOSE</strong></a>をそれぞれサポートしています。 リーダーへの接続を確立するために、リソースマネージャーは<strong>IRP_MJ_CREATE</strong>をリーダードライバーに送信します。 接続をサーバーに送信するために、リソースマネージャーは<strong>IRP_MJ_CLOSE</strong>を送信します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch" data-raw-source="[&lt;em&gt;DispatchCleanup&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)"><em>DispatchCleanup</em></a></p></td>
<td align="left"><p>は、 <a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-cleanup" data-raw-source="[&lt;strong&gt;IRP_MJ_CLEANUP&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-cleanup)"><strong>IRP_MJ_CLEANUP</strong></a>をサポートしています。これは、リソースマネージャーがリーダードライバーに送信し、保留中の i/o 要求をキャンセルします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch" data-raw-source="[&lt;em&gt;DispatchPnP&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)"><em>DispatchPnP</em></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-pnp" data-raw-source="[&lt;strong&gt;IRP_MJ_PNP&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-pnp)"><strong>IRP_MJ_PNP</strong></a>をサポートします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch" data-raw-source="[&lt;em&gt;DispatchPower&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)"><em>DispatchPower</em></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power" data-raw-source="[&lt;strong&gt;IRP_MJ_POWER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power)"><strong>IRP_MJ_POWER</strong></a>をサポートします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch" data-raw-source="[&lt;em&gt;DispatchDeviceControl&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)"><em>DispatchDeviceControl</em></a></p></td>
<td align="left"><p>は<a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control" data-raw-source="[&lt;strong&gt;IRP_MJ_DEVICE_CONTROL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)"><strong>IRP_MJ_DEVICE_CONTROL</strong></a>をサポートしており、スマートカード要求のメインエントリポイントです。 IRP_MJ_DEVICE_CONTROL を受信すると、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch" data-raw-source="[&lt;em&gt;DispatchDeviceControl&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)"><em>DispatchDeviceControl</em></a>は<a href="https://docs.microsoft.com/previous-versions/ff548939(v=vs.85)" data-raw-source="[&lt;strong&gt;SmartcardDeviceControl (WDM)&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff548939(v=vs.85))"><strong>Smartcarddevicecontrol (WDM)</strong></a>をすぐに呼び出す必要があります。これは、デバイス制御要求を処理するスマートカードドライバーライブラリルーチンです。 次のコード例は、WDM ドライバーからこのライブラリルーチンを呼び出す方法を示しています。</p>
<pre space="preserve"><code>NTSTATUS
DriverDeviceControl(
    PDEVICE_OBJECT DeviceObject,
    PIRP Irp
    )
{
    PDEVICE_EXTENSION deviceExtension = DeviceObject -&gt; DeviceExtension;

    return SmartcardDeviceControl(
        &(deviceExtension-&gt;SmartcardExtension),
        Irp
        );
}</code></pre>
<p>呼び出しで示されている特定の IOCTL を処理できない場合、 <strong>Smartcarddevicecontrol</strong>は、不明な ioctl 要求に対してドライバーのコールバックを呼び出します。</p></td>
</tr>
</tbody>
</table>

 

 

 





