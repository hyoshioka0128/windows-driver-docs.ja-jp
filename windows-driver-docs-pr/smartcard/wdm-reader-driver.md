---
title: WDM リーダーのドライバー
description: WDM リーダーのドライバー
ms.assetid: ead76f5f-1d28-4343-99c0-e7974fa4c3da
keywords:
- ベンダーから提供されたドライバー WDK スマート カード、必須のルーチン
- WDM WDK スマート カード
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 85cd0bf8e273d015fec7c3002e140ced8df8fc31
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548778"
---
# <a name="wdm-reader-driver"></a>WDM リーダーのドライバー


## <span id="_ntovr_wdm_reader_driver"></span><span id="_NTOVR_WDM_READER_DRIVER"></span>


WDM リーダーのドライバーに必要なルーチンを次の表に示します。

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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff544113" data-raw-source="[&lt;strong&gt;DriverEntry&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544113)"><strong>DriverEntry</strong></a></p></td>
<td align="left"><p>ドライバー オブジェクトとディスパッチ テーブルを初期化します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540521" data-raw-source="[&lt;em&gt;AddDevice&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540521)"><em>AddDevice</em></a></p></td>
<td align="left"><p>スマート カード リーダーのデバイス オブジェクトを作成します。 さらに、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff540521" data-raw-source="[&lt;em&gt;AddDevice&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540521)"> <em>AddDevice</em> </a>ライブラリ ルーチンを呼び出す次のドライバーのいずれかのことができます。</p>
<ul>
<li><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548944" data-raw-source="[&lt;strong&gt;SmartcardInitialize (WDM)&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548944)"><strong>SmartcardInitialize (WDM)</strong> </a>ドライバーの初期化を完了します。 このルーチンを呼び出す<a href="https://msdn.microsoft.com/library/windows/hardware/ff540521" data-raw-source="[&lt;em&gt;AddDevice&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540521)"> <em>AddDevice</em> </a>は必須です。</p></li>
<li><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548947" data-raw-source="[&lt;strong&gt;SmartcardLogError (WDM)&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548947)"><strong>SmartcardLogError (WDM)</strong> </a>エラーを記録します。 ドライバーこのルーチンを呼び出す必要があります<a href="https://msdn.microsoft.com/library/windows/hardware/ff540521" data-raw-source="[&lt;em&gt;AddDevice&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540521)"> <em>AddDevice</em> </a>場合<a href="https://msdn.microsoft.com/library/windows/hardware/ff548944" data-raw-source="[&lt;strong&gt;SmartcardInitialize (WDM)&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548944)"> <strong>SmartcardInitialize (WDM)</strong> </a>は失敗します。</p></li>
<li><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548935" data-raw-source="[&lt;strong&gt;SmartcardCreateLink (WDM)&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548935)"><strong>SmartcardCreateLink (WDM)</strong> </a>レジストリで、リーダー デバイスのシンボリック リンクを作成します。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564886" data-raw-source="[&lt;em&gt;Unload&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564886)"><em>アンロード</em></a></p></td>
<td align="left"><p>システムからドライバーを削除します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543266" data-raw-source="[&lt;em&gt;DispatchCreate&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543266)"><em>DispatchCreate</em></a></p>
<p>および</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch" data-raw-source="[&lt;em&gt;DispatchClose&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)"><em>DispatchClose</em></a></p></td>
<td align="left"><p>サポート<a href="https://msdn.microsoft.com/library/windows/hardware/ff550729" data-raw-source="[&lt;strong&gt;IRP_MJ_CREATE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550729)"> <strong>irp_mj_create 用</strong></a>と<a href="https://msdn.microsoft.com/library/windows/hardware/ff550720" data-raw-source="[&lt;strong&gt;IRP_MJ_CLOSE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550720)"><strong>未完了</strong></a>、それぞれします。 リーダーへの接続を確立するために、リソース マネージャーが送信<strong>irp_mj_create 用</strong>リーダーのドライバーにします。 リソース マネージャーが送信接続を切断するには、<strong>未完了</strong>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch" data-raw-source="[&lt;em&gt;DispatchCleanup&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)"><em>DispatchCleanup</em></a></p></td>
<td align="left"><p>サポート<a href="https://msdn.microsoft.com/library/windows/hardware/ff550718" data-raw-source="[&lt;strong&gt;IRP_MJ_CLEANUP&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550718)"> <strong>IRP_MJ_CLEANUP</strong></a>、保留中の I/O 要求をキャンセルするリーダーのドライバー リソース マネージャーに送信します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch" data-raw-source="[&lt;em&gt;DispatchPnP&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)"><em>DispatchPnP</em></a></p></td>
<td align="left"><p>サポート<a href="https://msdn.microsoft.com/library/windows/hardware/ff550772" data-raw-source="[&lt;strong&gt;IRP_MJ_PNP&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550772)"> <strong>IRP_MJ_PNP</strong></a>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch" data-raw-source="[&lt;em&gt;DispatchPower&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)"><em>DispatchPower</em></a></p></td>
<td align="left"><p>サポート<a href="https://msdn.microsoft.com/library/windows/hardware/ff550784" data-raw-source="[&lt;strong&gt;IRP_MJ_POWER&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550784)"><strong>対し、IRP_MJ_POWER</strong></a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch" data-raw-source="[&lt;em&gt;DispatchDeviceControl&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)"><em>DispatchDeviceControl</em></a></p></td>
<td align="left"><p>サポート<a href="https://msdn.microsoft.com/library/windows/hardware/ff550744" data-raw-source="[&lt;strong&gt;IRP_MJ_DEVICE_CONTROL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550744)"> <strong>IRP_MJ_DEVICE_CONTROL</strong> </a>とスマート カードの要求のメイン エントリ ポイントです。 受け取った IRP_MJ_DEVICE_CONTROL、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch" data-raw-source="[&lt;em&gt;DispatchDeviceControl&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)"> <em>DispatchDeviceControl</em> </a>すぐに呼び出す必要があります<a href="https://msdn.microsoft.com/library/windows/hardware/ff548939" data-raw-source="[&lt;strong&gt;SmartcardDeviceControl (WDM)&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548939)"> <strong>SmartcardDeviceControl (WDM)</strong></a>、これは、デバイス制御の要求を処理するスマート カードのドライバー ライブラリのルーチンです。 次のコード例では、このライブラリのルーチンを WDM ドライバーから呼び出す方法を示します。</p>
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
<p>呼び出しで示されている特定の IOCTL を処理することがない場合<strong>SmartcardDeviceControl</strong>ドライバーを呼び出す&#39;IOCTL の不明な要求のコールバック。</p></td>
</tr>
</tbody>
</table>

 

 

 





