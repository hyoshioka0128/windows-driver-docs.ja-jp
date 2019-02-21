---
title: WDM Irp と WDF イベントのコールバック関数
description: WDM Irp と WDF イベントのコールバック関数
ms.assetid: 9B9A01FD-AA15-4C30-B19D-2F6451014EAD
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b72c2c9791ce9dfca31067ef36b915905468ef89
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553698"
---
# <a name="wdm-irps-and-wdf-event-callback-functions"></a>WDM Irp と WDF イベントのコールバック関数


カーネル モード ドライバー フレームワーク (KMDF) とユーザー モード ドライバー フレームワーク (UMDF) は、Windows の Irp のサブセットをサポートします。 次の表には、主な WDM IRP 型と対応するフレームワーク イベントのコールバック関数が一覧表示します。 指定しない場合、コールバックは、KMDF と UMDF の両方に適用されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">主要な IRP コード</th>
<th align="left">WDF イベントのコールバック関数</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550718" data-raw-source="[&lt;strong&gt;IRP_MJ_CLEANUP&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550718)"><strong>IRP_MJ_CLEANUP</strong></a></td>
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff541700" data-raw-source="[&lt;em&gt;EvtFileCleanup&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541700)"><em>EvtFileCleanup</em></a></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550720" data-raw-source="[&lt;strong&gt;IRP_MJ_CLOSE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550720)"><strong>IRP_MJ_CLOSE</strong></a></td>
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff541702" data-raw-source="[&lt;em&gt;EvtFileClose&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541702)"><em>EvtFileClose</em></a></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550729" data-raw-source="[&lt;strong&gt;IRP_MJ_CREATE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550729)"><strong>IRP_MJ_CREATE</strong></a></td>
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff540868" data-raw-source="[&lt;em&gt;EvtDeviceFileCreate&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540868)"><em>EvtDeviceFileCreate</em> </a>または<a href="https://msdn.microsoft.com/library/windows/hardware/ff541757" data-raw-source="[&lt;em&gt;EvtIoDefault&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541757)"> <em>EvtIoDefault</em></a></td>
</tr>
<tr class="even">
<td align="left">IRP_MJ_CREATE_MAILSLOT</td>
<td align="left">直接サポートはありません。実装<a href="https://msdn.microsoft.com/library/windows/hardware/ff540925" data-raw-source="[&lt;em&gt;EvtDeviceWdmIrpPreprocess (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540925)"> <em>EvtDeviceWdmIrpPreprocess (KMDF のみ)</em></a></td>
</tr>
<tr class="odd">
<td align="left">IRP_MJ_DEVICE_CHANGE</td>
<td align="left">直接サポートはありません。実装<a href="https://msdn.microsoft.com/library/windows/hardware/ff540925" data-raw-source="[&lt;em&gt;EvtDeviceWdmIrpPreprocess (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540925)"> <em>EvtDeviceWdmIrpPreprocess (KMDF のみ)</em></a></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550744" data-raw-source="[&lt;strong&gt;IRP_MJ_DEVICE_CONTROL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550744)"><strong>IRP_MJ_DEVICE_CONTROL</strong></a></td>
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff541758" data-raw-source="[&lt;em&gt;EvtIoDeviceControl&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541758)"><em>EvtIoDeviceControl</em> </a>または<a href="https://msdn.microsoft.com/library/windows/hardware/ff541757" data-raw-source="[&lt;em&gt;EvtIoDefault&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541757)"> <em>EvtIoDefault</em></a></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff548658" data-raw-source="[&lt;strong&gt;IRP_MJ_DIRECTORY_CONTROL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548658)"><strong>IRP_MJ_DIRECTORY_CONTROL</strong></a></td>
<td align="left">直接サポートはありません。実装<a href="https://msdn.microsoft.com/library/windows/hardware/ff540925" data-raw-source="[&lt;em&gt;EvtDeviceWdmIrpPreprocess (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540925)"> <em>EvtDeviceWdmIrpPreprocess (KMDF のみ)</em></a></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550751" data-raw-source="[&lt;strong&gt;IRP_MJ_FILE_SYSTEM_CONTROL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550751)"><strong>IRP_MJ_FILE_SYSTEM_CONTROL</strong></a></td>
<td align="left">直接サポートはありません。実装<a href="https://msdn.microsoft.com/library/windows/hardware/ff540925" data-raw-source="[&lt;em&gt;EvtDeviceWdmIrpPreprocess (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540925)"> <em>EvtDeviceWdmIrpPreprocess (KMDF のみ)</em></a></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550760" data-raw-source="[&lt;strong&gt;IRP_MJ_FLUSH_BUFFERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550760)"><strong>IRP_MJ_FLUSH_BUFFERS</strong></a></td>
<td align="left">直接サポートはありません。実装<a href="https://msdn.microsoft.com/library/windows/hardware/ff540925" data-raw-source="[&lt;em&gt;EvtDeviceWdmIrpPreprocess (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540925)"> <em>EvtDeviceWdmIrpPreprocess (KMDF のみ)</em></a></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550766" data-raw-source="[&lt;strong&gt;IRP_MJ_INTERNAL_DEVICE_CONTROL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550766)"><strong>IRP_MJ_INTERNAL_DEVICE_CONTROL</strong></a></td>
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff541768" data-raw-source="[&lt;em&gt;EvtIoInternalDeviceControl&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541768)"><em>EvtIoInternalDeviceControl</em> </a>または<a href="https://msdn.microsoft.com/library/windows/hardware/ff541757" data-raw-source="[&lt;em&gt;EvtIoDefault&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541757)"> <em>EvtIoDefault</em></a></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff549251" data-raw-source="[&lt;strong&gt;IRP_MJ_LOCK_CONTROL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549251)"><strong>IRP_MJ_LOCK_CONTROL</strong></a></td>
<td align="left">直接サポートはありません。実装<a href="https://msdn.microsoft.com/library/windows/hardware/ff540925" data-raw-source="[&lt;em&gt;EvtDeviceWdmIrpPreprocess (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540925)"> <em>EvtDeviceWdmIrpPreprocess (KMDF のみ)</em></a></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550772" data-raw-source="[&lt;strong&gt;IRP_MJ_PNP&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550772)"><strong>IRP_MJ_PNP</strong></a></td>
<td align="left">多くの場合。参照してください<a href="#pnp" data-raw-source="[KMDF Callbacks for IRP_MJ_PNP](#pnp)">IRP_MJ_PNP の KMDF コールバック</a>します。</td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550784" data-raw-source="[&lt;strong&gt;IRP_MJ_POWER&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550784)"><strong>IRP_MJ_POWER</strong></a></td>
<td align="left">多くの場合。参照してください<a href="#power" data-raw-source="[KMDF Callbacks for IRP_MJ_POWER](#power)">KMDF コールバックに対し、IRP_MJ_POWER</a>します。</td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff549279" data-raw-source="[&lt;strong&gt;IRP_MJ_QUERY_EA&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549279)"><strong>IRP_MJ_QUERY_EA</strong></a></td>
<td align="left">直接サポートはありません。実装<a href="https://msdn.microsoft.com/library/windows/hardware/ff540925" data-raw-source="[&lt;em&gt;EvtDeviceWdmIrpPreprocess (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540925)"> <em>EvtDeviceWdmIrpPreprocess (KMDF のみ)</em></a></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550788" data-raw-source="[&lt;strong&gt;IRP_MJ_QUERY_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550788)"><strong>IRP_MJ_QUERY_INFORMATION</strong></a></td>
<td align="left">直接サポートはありません。実装<a href="https://msdn.microsoft.com/library/windows/hardware/ff540925" data-raw-source="[&lt;em&gt;EvtDeviceWdmIrpPreprocess (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540925)"> <em>EvtDeviceWdmIrpPreprocess (KMDF のみ)</em></a></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff549293" data-raw-source="[&lt;strong&gt;IRP_MJ_QUERY_QUOTA&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549293)"><strong>IRP_MJ_QUERY_QUOTA</strong></a></td>
<td align="left">直接サポートはありません。実装<a href="https://msdn.microsoft.com/library/windows/hardware/ff540925" data-raw-source="[&lt;em&gt;EvtDeviceWdmIrpPreprocess (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540925)"> <em>EvtDeviceWdmIrpPreprocess (KMDF のみ)</em></a></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff549298" data-raw-source="[&lt;strong&gt;IRP_MJ_QUERY_SECURITY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549298)"><strong>IRP_MJ_QUERY_SECURITY</strong></a></td>
<td align="left">直接サポートはありません。実装<a href="https://msdn.microsoft.com/library/windows/hardware/ff540925" data-raw-source="[&lt;em&gt;EvtDeviceWdmIrpPreprocess (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540925)"> <em>EvtDeviceWdmIrpPreprocess (KMDF のみ)</em></a></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff549318" data-raw-source="[&lt;strong&gt;IRP_MJ_QUERY_VOLUME_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549318)"><strong>IRP_MJ_QUERY_VOLUME_INFORMATION</strong></a></td>
<td align="left">直接サポートはありません。実装<a href="https://msdn.microsoft.com/library/windows/hardware/ff540925" data-raw-source="[&lt;em&gt;EvtDeviceWdmIrpPreprocess (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540925)"> <em>EvtDeviceWdmIrpPreprocess (KMDF のみ)</em></a></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550794" data-raw-source="[&lt;strong&gt;IRP_MJ_READ&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550794)"><strong>IRP_MJ_READ</strong></a></td>
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff541776" data-raw-source="[&lt;em&gt;EvtIoRead&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541776)"><em>EvtIoRead</em> </a>または<a href="https://msdn.microsoft.com/library/windows/hardware/ff541757" data-raw-source="[&lt;em&gt;EvtIoDefault&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541757)"> <em>EvtIoDefault</em></a></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff549346" data-raw-source="[&lt;strong&gt;IRP_MJ_SET_EA&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549346)"><strong>IRP_MJ_SET_EA</strong></a></td>
<td align="left">直接サポートはありません。実装<a href="https://msdn.microsoft.com/library/windows/hardware/ff540925" data-raw-source="[&lt;em&gt;EvtDeviceWdmIrpPreprocess (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540925)"> <em>EvtDeviceWdmIrpPreprocess (KMDF のみ)</em></a></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550799" data-raw-source="[&lt;strong&gt;IRP_MJ_SET_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550799)"><strong>IRP_MJ_SET_INFORMATION</strong></a></td>
<td align="left">直接サポートはありません。実装<a href="https://msdn.microsoft.com/library/windows/hardware/ff540925" data-raw-source="[&lt;em&gt;EvtDeviceWdmIrpPreprocess (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540925)"> <em>EvtDeviceWdmIrpPreprocess (KMDF のみ)</em></a></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff549401" data-raw-source="[&lt;strong&gt;IRP_MJ_SET_QUOTA&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549401)"><strong>IRP_MJ_SET_QUOTA</strong></a></td>
<td align="left">直接サポートはありません。実装<a href="https://msdn.microsoft.com/library/windows/hardware/ff540925" data-raw-source="[&lt;em&gt;EvtDeviceWdmIrpPreprocess (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540925)"> <em>EvtDeviceWdmIrpPreprocess (KMDF のみ)</em></a></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff549407" data-raw-source="[&lt;strong&gt;IRP_MJ_SET_SECURITY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549407)"><strong>IRP_MJ_SET_SECURITY</strong></a></td>
<td align="left">直接サポートはありません。実装<a href="https://msdn.microsoft.com/library/windows/hardware/ff540925" data-raw-source="[&lt;em&gt;EvtDeviceWdmIrpPreprocess (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540925)"> <em>EvtDeviceWdmIrpPreprocess (KMDF のみ)</em></a></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff549415" data-raw-source="[&lt;strong&gt;IRP_MJ_SET_VOLUME_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549415)"><strong>IRP_MJ_SET_VOLUME_INFORMATION</strong></a></td>
<td align="left">直接サポートはありません。実装<a href="https://msdn.microsoft.com/library/windows/hardware/ff540925" data-raw-source="[&lt;em&gt;EvtDeviceWdmIrpPreprocess (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540925)"> <em>EvtDeviceWdmIrpPreprocess (KMDF のみ)</em></a></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550807" data-raw-source="[&lt;strong&gt;IRP_MJ_SHUTDOWN&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550807)"><strong>IRP_MJ_SHUTDOWN</strong></a></td>
<td align="left"><p>デバイス オブジェクトのコントロール実装<a href="https://msdn.microsoft.com/library/windows/hardware/ff540911" data-raw-source="[&lt;em&gt;EvtDeviceShutdownNotification (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540911)"> <em>EvtDeviceShutdownNotification (KMDF のみ)</em></a></p>
<p>すべてのプラグ アンド プレイ デバイスのオブジェクト。サポートされていません。実装<a href="https://msdn.microsoft.com/library/windows/hardware/ff540925" data-raw-source="[&lt;em&gt;EvtDeviceWdmIrpPreprocess (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540925)"> <em>EvtDeviceWdmIrpPreprocess (KMDF のみ)</em></a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550813" data-raw-source="[&lt;strong&gt;IRP_MJ_SYSTEM_CONTROL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550813)"><strong>IRP_MJ_SYSTEM_CONTROL</strong></a></td>
<td align="left">WDFWMIPROVIDER と WDFWMIINSTANCE オブジェクトの作成し、実装<strong>EvtWmiXxx (KMDF のみ)</strong>コールバック。</td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550819" data-raw-source="[&lt;strong&gt;IRP_MJ_WRITE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550819)"><strong>IRP_MJ_WRITE</strong></a></td>
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff541813" data-raw-source="[&lt;em&gt;EvtIoWrite&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541813)"><em>EvtIoWrite</em> </a>または<a href="https://msdn.microsoft.com/library/windows/hardware/ff541757" data-raw-source="[&lt;em&gt;EvtIoDefault&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541757)"> <em>EvtIoDefault</em></a></td>
</tr>
</tbody>
</table>

 

## <a name="kmdf-callbacks-for-irpmjpnp"></a>IRP のコールバックを KMDF\_MJ\_PNP


次の表に、マイナー IRP のコードに対応する KMDF コールバックの実行の順序でリスト、 [ **IRP\_MJ\_PNP**](https://msdn.microsoft.com/library/windows/hardware/ff550772)します。 矢印は、スタックの上下をたどる際 WDM FDO が IRP を処理するかどうかを示します。

**注**  で、KMDF ドライバー、プラグ アンド プレイおよび電源管理が統合操作と、ドライバーは、個々 のマイナーを受信しません[ **IRP\_MJ\_PNP**](https://msdn.microsoft.com/library/windows/hardware/ff550772)または[ **IRP\_MJ\_POWER** ](https://msdn.microsoft.com/library/windows/hardware/ff550784)要求。 代わりに、フレームワークは、電源アップ、対応する、電源設定でコールバックのコア セットの呼び出しをこのコアの個別のプラグ アンド プレイ要求ごとに適切な設定の前後に追加のコールバックを呼び出します。 電源投入し、電源ダウン シーケンスを示す包括的な図を参照してください。 [PnP 移植し、電源管理機能](porting-pnp-and-power-management-functionality.md)します。

 

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">コードの軽微な IRP_MJ_PNP</th>
<th align="left">KMDF コールバック</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">↓<a href="https://msdn.microsoft.com/library/windows/hardware/ff550823" data-raw-source="[&lt;strong&gt;IRP_MN_CANCEL_REMOVE_DEVICE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550823)"><strong>IRP_MN_CANCEL_REMOVE_DEVICE</strong></a></td>
<td align="left">なし</td>
</tr>
<tr class="even">
<td align="left">↓<a href="https://msdn.microsoft.com/library/windows/hardware/ff550826" data-raw-source="[&lt;strong&gt;IRP_MN_CANCEL_STOP_DEVICE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550826)"><strong>IRP_MN_CANCEL_STOP_DEVICE</strong></a></td>
<td align="left">なし</td>
</tr>
<tr class="odd">
<td align="left">↑<a href="https://msdn.microsoft.com/library/windows/hardware/ff550841" data-raw-source="[&lt;strong&gt;IRP_MN_DEVICE_USAGE_NOTIFICATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550841)"><strong>IRP_MN_DEVICE_USAGE_NOTIFICATION</strong></a></td>
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff540915" data-raw-source="[&lt;em&gt;EvtDeviceUsageNotification&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540915)"><em>EvtDeviceUsageNotification</em></a></td>
</tr>
<tr class="even">
<td align="left">↓<a href="https://msdn.microsoft.com/library/windows/hardware/ff550853" data-raw-source="[&lt;strong&gt;IRP_MN_EJECT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550853)"><strong>IRP_MN_EJECT</strong></a></td>
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff540863" data-raw-source="[&lt;em&gt;EvtDeviceEject (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540863)"><em>EvtDeviceEject (KMDF のみ)</em></a></td>
</tr>
<tr class="odd">
<td align="left">↓<a href="https://msdn.microsoft.com/library/windows/hardware/ff550874" data-raw-source="[&lt;strong&gt;IRP_MN_FILTER_RESOURCE_REQUIREMENTS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550874)"><strong>IRP_MN_FILTER_RESOURCE_REQUIREMENTS</strong></a></td>
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff540872" data-raw-source="[&lt;em&gt;EvtDeviceFilterRemoveResourceRequirements (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540872)"><em>EvtDeviceFilterRemoveResourceRequirements (KMDF のみ)</em></a></td>
</tr>
<tr class="even">
<td align="left">↑<a href="https://msdn.microsoft.com/library/windows/hardware/ff550874" data-raw-source="[&lt;strong&gt;IRP_MN_FILTER_RESOURCE_REQUIREMENTS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550874)"><strong>IRP_MN_FILTER_RESOURCE_REQUIREMENTS</strong></a></td>
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff540870" data-raw-source="[&lt;em&gt;EvtDeviceFilterAddResourceRequirements (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540870)"><em>EvtDeviceFilterAddResourceRequirements (KMDF のみ)</em></a></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff551654" data-raw-source="[&lt;strong&gt;IRP_MN_QUERY_BUS_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551654)"><strong>IRP_MN_QUERY_BUS_INFORMATION</strong></a></td>
<td align="left">なし。 KMDF ドライバー呼び出し<strong>WdfDeviceInitXxx</strong>フレームワークは、ドライバーを通知することがなく独自のこのクエリに応答できるように、初期化中にデバイスのプロパティを設定する方法。</td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff551664" data-raw-source="[&lt;strong&gt;IRP_MN_QUERY_CAPABILITIES&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551664)"><strong>IRP_MN_QUERY_CAPABILITIES</strong></a></td>
<td align="left">なし。 KMDF ドライバー呼び出し<strong>WdfDeviceInitXxx</strong>フレームワークは、ドライバーを通知することがなく独自のこのクエリに応答できるように、初期化中にデバイスのプロパティを設定する方法。</td>
</tr>
<tr class="odd">
<td align="left">↓<a href="https://msdn.microsoft.com/library/windows/hardware/ff551670" data-raw-source="[&lt;strong&gt;IRP_MN_QUERY_DEVICE_RELATIONS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551670)"><strong>IRP_MN_QUERY_DEVICE_RELATIONS</strong> </a> (バス、削除、および取り出しリレーション)</td>
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff540886" data-raw-source="[&lt;em&gt;EvtDeviceRelationsQuery&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540886)"><em>EvtDeviceRelationsQuery</em></a></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff551674" data-raw-source="[&lt;strong&gt;IRP_MN_QUERY_DEVICE_TEXT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551674)"><strong>IRP_MN_QUERY_DEVICE_TEXT</strong></a></td>
<td align="left">なし。 KMDF ドライバー呼び出し<strong>WdfDeviceInitXxx</strong>フレームワークは、ドライバーを通知することがなく独自のこのクエリに応答できるように、初期化中にデバイスのプロパティを設定する方法。</td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff551679" data-raw-source="[&lt;strong&gt;IRP_MN_QUERY_ID&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551679)"><strong>IRP_MN_QUERY_ID</strong></a></td>
<td align="left">なし。 KMDF ドライバー呼び出し<strong>WdfDeviceInitXxx</strong>フレームワークは、ドライバーを通知することがなく独自のこのクエリに応答できるように、初期化中にデバイスのプロパティを設定する方法。</td>
</tr>
<tr class="even">
<td align="left">↓<a href="https://msdn.microsoft.com/library/windows/hardware/ff551687" data-raw-source="[&lt;strong&gt;IRP_MN_QUERY_INTERFACE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551687)"><strong>IRP_MN_QUERY_INTERFACE</strong></a></td>
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff540882" data-raw-source="[&lt;em&gt;EvtDeviceProcessQueryInterfaceRequest (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540882)"><em>EvtDeviceProcessQueryInterfaceRequest (KMDF のみ)</em></a></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff551698" data-raw-source="[&lt;strong&gt;IRP_MN_QUERY_PNP_DEVICE_STATE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551698)"><strong>IRP_MN_QUERY_PNP_DEVICE_STATE</strong></a></td>
<td align="left">なし。 KMDF ドライバー呼び出し<strong>WdfDeviceInitXxx</strong>フレームワークは、ドライバーを通知することがなく独自のこのクエリに応答できるように、初期化中にデバイスのプロパティを設定する方法。</td>
</tr>
<tr class="even">
<td align="left">↓<a href="https://msdn.microsoft.com/library/windows/hardware/ff551705" data-raw-source="[&lt;strong&gt;IRP_MN_QUERY_REMOVE_DEVICE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551705)"><strong>IRP_MN_QUERY_REMOVE_DEVICE</strong></a></td>
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff540883" data-raw-source="[&lt;em&gt;EvtDeviceQueryRemove&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540883)"><em>EvtDeviceQueryRemove</em></a></td>
</tr>
<tr class="odd">
<td align="left">↓<a href="https://msdn.microsoft.com/library/windows/hardware/ff551715" data-raw-source="[&lt;strong&gt;IRP_MN_QUERY_RESOURCE_REQUIREMENTS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551715)"><strong>IRP_MN_QUERY_RESOURCE_REQUIREMENTS</strong></a></td>
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff540894" data-raw-source="[&lt;em&gt;EvtDeviceResourceRequirementsQuery (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540894)"><em>EvtDeviceResourceRequirementsQuery (KMDF のみ)</em></a></td>
</tr>
<tr class="even">
<td align="left">↓<a href="https://msdn.microsoft.com/library/windows/hardware/ff551710" data-raw-source="[&lt;strong&gt;IRP_MN_QUERY_RESOURCES&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551710)"><strong>IRP_MN_QUERY_RESOURCES</strong></a></td>
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff540895" data-raw-source="[&lt;em&gt;EvtDeviceResourcesQuery (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540895)"><em>EvtDeviceResourcesQuery (KMDF のみ)</em></a></td>
</tr>
<tr class="odd">
<td align="left">↓<a href="https://msdn.microsoft.com/library/windows/hardware/ff551725" data-raw-source="[&lt;strong&gt;IRP_MN_QUERY_STOP_DEVICE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551725)"><strong>IRP_MN_QUERY_STOP_DEVICE</strong></a></td>
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff540885" data-raw-source="[&lt;em&gt;EvtDeviceQueryStop&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540885)"><em>EvtDeviceQueryStop</em></a></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff551727" data-raw-source="[&lt;strong&gt;IRP_MN_READ_CONFIG&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551727)"><strong>IRP_MN_READ_CONFIG</strong></a></td>
<td align="left">なし。 KMDF ドライバー呼び出し<strong>WdfDeviceInitXxx</strong>フレームワークは、ドライバーを通知することがなく独自のこのクエリに応答できるように、初期化中にデバイスのプロパティを設定する方法。</td>
</tr>
<tr class="odd">
<td align="left">↓<a href="https://msdn.microsoft.com/library/windows/hardware/ff551738" data-raw-source="[&lt;strong&gt;IRP_MN_REMOVE_DEVICE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551738)"><strong>IRP_MN_REMOVE_DEVICE</strong></a></td>
<td align="left"><p>後<a href="https://msdn.microsoft.com/library/windows/hardware/ff551705" data-raw-source="[&lt;strong&gt;IRP_MN_QUERY_REMOVE_DEVICE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551705)"> <strong>IRP_MN_QUERY_REMOVE_DEVICE</strong></a>:</p>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff540907" data-raw-source="[&lt;em&gt;EvtDeviceSelfManagedIoSuspend&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540907)"><em>EvtDeviceSelfManagedIoSuspend</em></a>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff541788" data-raw-source="[&lt;em&gt;EvtIoStop&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541788)"><em>EvtIoStop</em> </a> (<strong>WdfRequestStopActionSuspend</strong>フラグ) <a href="https://msdn.microsoft.com/library/windows/hardware/ff541677" data-raw-source="[&lt;em&gt;EvtDmaEnablerSelfManagedIoStop (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541677)"> <em>EvtDmaEnablerSelfManagedIoStop (KMDF のみ)</em></a>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff540927" data-raw-source="[&lt;em&gt;EvtDmaEnablerDisable (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540927)"><em>EvtDmaEnablerDisable (KMDF のみ)</em> </a> 
<a href="https://msdn.microsoft.com/library/windows/hardware/ff541655" data-raw-source="[&lt;em&gt;EvtDmaEnablerFlush (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541655)"> <em>EvtDmaEnablerFlush (KMDF のみ)</em></a>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff540856" data-raw-source="[&lt;em&gt;EvtDeviceD0ExitPreInterruptsDisabled&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540856)"><em>EvtDeviceD0ExitPreInterruptsDisabled</em></a>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff541714" data-raw-source="[&lt;em&gt;EvtInterruptDisable&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541714)"><em>EvtInterruptDisable</em></a> 
<a href="https://msdn.microsoft.com/library/windows/hardware/ff540855" data-raw-source="[&lt;em&gt;EvtDeviceD0Exit&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540855)"> <em>EvtDeviceD0Exit</em> </a> (<strong>WdfPowerDeviceD3Final</strong>状態) <a href="https://msdn.microsoft.com/library/windows/hardware/ff540890" data-raw-source="[&lt;em&gt;EvtDeviceReleaseHardware&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540890)"> <em>EvtDeviceReleaseHardware</em></a> 
<a href="https://msdn.microsoft.com/library/windows/hardware/ff541788" data-raw-source="[&lt;em&gt;EvtIoStop&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541788)"> <em>EvtIoStop</em> </a> (<strong>WdfRequestStopActionPurge</strong>フラグ) の電源管理対象のキュー <a href="https://msdn.microsoft.com/library/windows/hardware/ff540901" data-raw-source="[&lt;em&gt;EvtDeviceSelfManagedIoFlush&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540901)"> <em>EvtDeviceSelfManagedIoFlush</em></a>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff541788" data-raw-source="[&lt;em&gt;EvtIoStop&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541788)"><em>EvtIoStop</em> </a> (<strong>WdfRequestStopActionPurge</strong>フラグ) の電源管理対象外のキュー <a href="https://msdn.microsoft.com/library/windows/hardware/ff540898" data-raw-source="[&lt;em&gt;EvtDeviceSelfManagedIoCleanup&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540898)"> <em>EvtDeviceSelfManagedIoCleanup</em></a>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff540840" data-raw-source="[&lt;em&gt;EvtCleanupCallback&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540840)"><em>EvtCleanupCallback</em> </a>WDFDEVICE の<a href="https://msdn.microsoft.com/library/windows/hardware/ff540841" data-raw-source="[&lt;em&gt;EvtDestroyCallback&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540841)"> <em>EvtDestroyCallback</em> </a> WDFDEVICE の
<p>After <a href="https://msdn.microsoft.com/library/windows/hardware/ff551760" data-raw-source="[&lt;strong&gt;IRP_MN_SURPRISE_REMOVAL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551760)"><strong>IRP_MN_SURPRISE_REMOVAL</strong></a>:</p>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff541788" data-raw-source="[&lt;em&gt;EvtIoStop&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541788)"><em>EvtIoStop</em> </a> (<strong>WdfRequestStopActionPurge</strong>フラグ) キューの電源管理対象外の<a href="https://msdn.microsoft.com/library/windows/hardware/ff540898" data-raw-source="[&lt;em&gt;EvtDeviceSelfManagedIoCleanup&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540898)"> <em>EvtDeviceSelfManagedIoCleanup</em> </a> 
<a href="https://msdn.microsoft.com/library/windows/hardware/ff540840" data-raw-source="[&lt;em&gt;EvtCleanupCallback&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540840)"><em>EvtCleanupCallback</em> </a> WDFDEVICE の<a href="https://msdn.microsoft.com/library/windows/hardware/ff540841" data-raw-source="[&lt;em&gt;EvtDestroyCallback&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540841)"> <em>EvtDestroyCallback</em> </a> WDFDEVICE の</td>
</tr>
<tr class="even">
<td align="left">↓<a href="https://msdn.microsoft.com/library/windows/hardware/ff551742" data-raw-source="[&lt;strong&gt;IRP_MN_SET_LOCK&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551742)"><strong>IRP_MN_SET_LOCK</strong></a></td>
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff540909" data-raw-source="[&lt;em&gt;EvtDeviceSetLock (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540909)"><em>EvtDeviceSetLock (KMDF のみ)</em></a></td>
</tr>
<tr class="odd">
<td align="left">↑<a href="https://msdn.microsoft.com/library/windows/hardware/ff551749" data-raw-source="[&lt;strong&gt;IRP_MN_START_DEVICE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551749)"><strong>IRP_MN_START_DEVICE</strong></a></td>
<td align="left"><p>列挙: の後</p>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff540892" data-raw-source="[&lt;em&gt;EvtDeviceRemoveAddedResources (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540892)"><em>EvtDeviceRemoveAddedResources (KMDF のみ)</em></a>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff540880" data-raw-source="[&lt;em&gt;EvtDevicePrepareHardware&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540880)"><em>EvtDevicePrepareHardware</em></a>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff540848" data-raw-source="[&lt;em&gt;EvtDeviceD0Entry&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540848)"><em>EvtDeviceD0Entry</em> </a>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff541730" data-raw-source="[&lt;em&gt;EvtInterruptEnable&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541730)"> <em>EvtInterruptEnable</em></a>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff540853" data-raw-source="[&lt;em&gt;EvtDeviceD0EntryPostInterruptsEnabled&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540853)"><em>EvtDeviceD0EntryPostInterruptsEnabled</em> </a> 
<a href="https://msdn.microsoft.com/library/windows/hardware/ff540932" data-raw-source="[&lt;em&gt;EvtDmaEnablerFill (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540932)"> <em>EvtDmaEnablerFill (KMDF のみ)</em></a>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff540929" data-raw-source="[&lt;em&gt;EvtDmaEnablerEnable (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540929)"><em>EvtDmaEnablerEnable (KMDF のみ)</em></a>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff541663" data-raw-source="[&lt;em&gt;EvtDmaEnablerSelfManagedIoStart (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541663)"><em>EvtDmaEnablerSelfManagedIoStart (KMDF のみ)</em></a>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff540902" data-raw-source="[&lt;em&gt;EvtDeviceSelfManagedIoInit&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540902)"><em>EvtDeviceSelfManagedIoInit</em></a>
<p>後<a href="https://msdn.microsoft.com/library/windows/hardware/ff551755" data-raw-source="[&lt;strong&gt;IRP_MN_STOP_DEVICE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551755)"> <strong>IRP_MN_STOP_DEVICE</strong></a>:</p>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff540892" data-raw-source="[&lt;em&gt;EvtDeviceRemoveAddedResources (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540892)"><em>EvtDeviceRemoveAddedResources (KMDF のみ)</em></a>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff540880" data-raw-source="[&lt;em&gt;EvtDevicePrepareHardware&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540880)"><em>EvtDevicePrepareHardware</em></a>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff540848" data-raw-source="[&lt;em&gt;EvtDeviceD0Entry&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540848)"><em>EvtDeviceD0Entry</em> </a>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff541730" data-raw-source="[&lt;em&gt;EvtInterruptEnable&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541730)"> <em>EvtInterruptEnable</em></a>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff540853" data-raw-source="[&lt;em&gt;EvtDeviceD0EntryPostInterruptsEnabled&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540853)"><em>EvtDeviceD0EntryPostInterruptsEnabled</em> </a> 
<a href="https://msdn.microsoft.com/library/windows/hardware/ff540932" data-raw-source="[&lt;em&gt;EvtDmaEnablerFill (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540932)"> <em>EvtDmaEnablerFill (KMDF のみ)</em></a>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff540929" data-raw-source="[&lt;em&gt;EvtDmaEnablerEnable (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540929)"><em>EvtDmaEnablerEnable (KMDF のみ)</em></a>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff541663" data-raw-source="[&lt;em&gt;EvtDmaEnablerSelfManagedIoStart (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541663)"><em>EvtDmaEnablerSelfManagedIoStart (KMDF のみ)</em></a>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff541779" data-raw-source="[&lt;em&gt;EvtIoResume&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541779)"><em>EvtIoResume</em></a>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff540905" data-raw-source="[&lt;em&gt;EvtDeviceSelfManagedIoRestart&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540905)"><em>EvtDeviceSelfManagedIoRestart</em></a></td>
</tr>
<tr class="even">
<td align="left">↓<a href="https://msdn.microsoft.com/library/windows/hardware/ff551755" data-raw-source="[&lt;strong&gt;IRP_MN_STOP_DEVICE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551755)"><strong>IRP_MN_STOP_DEVICE</strong></a></td>
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff540907" data-raw-source="[&lt;em&gt;EvtDeviceSelfManagedIoSuspend&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540907)"><em>EvtDeviceSelfManagedIoSuspend</em></a>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff541788" data-raw-source="[&lt;em&gt;EvtIoStop&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541788)"><em>EvtIoStop</em> </a> (<strong>WdfRequestStopActionSuspend</strong>フラグ) <a href="https://msdn.microsoft.com/library/windows/hardware/ff541677" data-raw-source="[&lt;em&gt;EvtDmaEnablerSelfManagedIoStop (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541677)"> <em>EvtDmaEnablerSelfManagedIoStop (KMDF のみ)</em></a>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff540927" data-raw-source="[&lt;em&gt;EvtDmaEnablerDisable (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540927)"><em>EvtDmaEnablerDisable (KMDF のみ)</em> </a> 
<a href="https://msdn.microsoft.com/library/windows/hardware/ff541655" data-raw-source="[&lt;em&gt;EvtDmaEnablerFlush (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541655)"> <em>EvtDmaEnablerFlush (KMDF のみ)</em></a>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff540856" data-raw-source="[&lt;em&gt;EvtDeviceD0ExitPreInterruptsDisabled&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540856)"><em>EvtDeviceD0ExitPreInterruptsDisabled</em></a>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff541714" data-raw-source="[&lt;em&gt;EvtInterruptDisable&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541714)"><em>EvtInterruptDisable</em></a> 
<a href="https://msdn.microsoft.com/library/windows/hardware/ff540855" data-raw-source="[&lt;em&gt;EvtDeviceD0Exit&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540855)"> <em>EvtDeviceD0Exit</em> </a> (<strong>WdfPowerDeviceD3Final</strong>状態) <a href="https://msdn.microsoft.com/library/windows/hardware/ff540890" data-raw-source="[&lt;em&gt;EvtDeviceReleaseHardware&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540890)"> <em>EvtDeviceReleaseHardware</em></a></td>
</tr>
<tr class="odd">
<td align="left">↓<a href="https://msdn.microsoft.com/library/windows/hardware/ff551760" data-raw-source="[&lt;strong&gt;IRP_MN_SURPRISE_REMOVAL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551760)"><strong>IRP_MN_SURPRISE_REMOVAL</strong></a></td>
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff540913" data-raw-source="[&lt;em&gt;EvtDeviceSurpriseRemoval&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540913)"><em>EvtDeviceSurpriseRemoval</em></a>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff540907" data-raw-source="[&lt;em&gt;EvtDeviceSelfManagedIoSuspend&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540907)"><em>EvtDeviceSelfManagedIoSuspend</em></a>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff541788" data-raw-source="[&lt;em&gt;EvtIoStop&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541788)"><em>EvtIoStop</em> </a> (<strong>WdfRequestStopActionSuspend</strong>フラグ) <a href="https://msdn.microsoft.com/library/windows/hardware/ff541677" data-raw-source="[&lt;em&gt;EvtDmaEnablerSelfManagedIoStop (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541677)"> <em>EvtDmaEnablerSelfManagedIoStop (KMDF のみ)</em></a>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff540927" data-raw-source="[&lt;em&gt;EvtDmaEnablerDisable (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540927)"><em>EvtDmaEnablerDisable (KMDF のみ)</em> </a> 
<a href="https://msdn.microsoft.com/library/windows/hardware/ff541655" data-raw-source="[&lt;em&gt;EvtDmaEnablerFlush (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541655)"> <em>EvtDmaEnablerFlush (KMDF のみ)</em></a>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff540856" data-raw-source="[&lt;em&gt;EvtDeviceD0ExitPreInterruptsDisabled&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540856)"><em>EvtDeviceD0ExitPreInterruptsDisabled</em> </a>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff541714" data-raw-source="[&lt;em&gt;EvtInterruptDisable&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541714)"> <em>EvtInterruptDisable</em></a>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff540855" data-raw-source="[&lt;em&gt;EvtDeviceD0Exit&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540855)"><em>EvtDeviceD0Exit</em> </a> (<strong>WdfPowerDeviceD3Final</strong>状態) <a href="https://msdn.microsoft.com/library/windows/hardware/ff540890" data-raw-source="[&lt;em&gt;EvtDeviceReleaseHardware&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540890)"> <em>EvtDeviceReleaseHardware</em></a>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff541788" data-raw-source="[&lt;em&gt;EvtIoStop&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541788)"><em>EvtIoStop</em> </a> (<strong>WdfRequestStopActionPurge</strong>フラグ) の電源管理対象のキュー <a href="https://msdn.microsoft.com/library/windows/hardware/ff540901" data-raw-source="[&lt;em&gt;EvtDeviceSelfManagedIoFlush&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540901)"> <em>EvtDeviceSelfManagedIoFlush</em></a></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff551769" data-raw-source="[&lt;strong&gt;IRP_MN_WRITE_CONFIG&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551769)"><strong>IRP_MN_WRITE_CONFIG</strong></a></td>
<td align="left">なし。 KMDF ドライバー呼び出し<strong>WdfDeviceInitXxx</strong>フレームワークは、ドライバーを通知することがなく独自のこのクエリに応答できるように、初期化中にデバイスのプロパティを設定する方法。</td>
</tr>
</tbody>
</table>

 

## <a name="kmdf-callbacks-for-irpmjpower"></a>IRP のコールバックを KMDF\_MJ\_電源


次の表に、マイナー IRP のコードに対応する KMDF コールバックの実行の順序でリスト、 [ **IRP\_MJ\_POWER**](https://msdn.microsoft.com/library/windows/hardware/ff550784)します。 矢印は、スタックの上下をたどる際 WDM FDO が IRP を処理するかどうかを示します。

**注**  に注意してください。KMDF ドライバーでは、プラグ アンド プレイおよび電源管理は、統合操作と、ドライバーは、個々 のマイナーを受信しません[ **IRP\_MJ\_PNP** ](https://msdn.microsoft.com/library/windows/hardware/ff550772)または[**IRP\_MJ\_POWER** ](https://msdn.microsoft.com/library/windows/hardware/ff550784)要求。 代わりに、フレームワークは、電源アップ、対応する、電源設定でコールバックのコア セットの呼び出しをこのコアの個別のプラグ アンド プレイ要求ごとに適切な設定の前後に追加のコールバックを呼び出します。 電源投入し、電源ダウン シーケンスを示す包括的な図を参照してください。 [PnP 移植し、電源管理機能](porting-pnp-and-power-management-functionality.md)します。

 

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">コードの軽微なに対し、IRP_MJ_POWER</th>
<th align="left">フレームワークのコールバック</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">↓<a href="https://msdn.microsoft.com/library/windows/hardware/ff551744" data-raw-source="[&lt;strong&gt;IRP_MN_SET_POWER&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551744)"><strong>IRP_MN_SET_POWER</strong> </a> D1、d2 に切り替わり、または D3 (電源ダウン)</td>
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff540907" data-raw-source="[&lt;em&gt;EvtDeviceSelfManagedIoSuspend&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540907)"><em>EvtDeviceSelfManagedIoSuspend</em></a>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff541788" data-raw-source="[&lt;em&gt;EvtIoStop&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541788)"><em>EvtIoStop</em> </a> (<strong>WdfRequestStopActionSuspend</strong>フラグ) <a href="https://msdn.microsoft.com/library/windows/hardware/ff540843" data-raw-source="[&lt;em&gt;EvtDeviceArmWakeFromS0&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540843)"> <em>EvtDeviceArmWakeFromS0</em> </a>または<a href="https://msdn.microsoft.com/library/windows/hardware/ff540844" data-raw-source="[&lt;em&gt;EvtDeviceArmWakeFromSx&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540844)"> <em>EvtDeviceArmWakeFromSx</em></a>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff541677" data-raw-source="[&lt;em&gt;EvtDmaEnablerSelfManagedIoStop (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541677)"><em>EvtDmaEnablerSelfManagedIoStop (KMDFのみ)</em></a>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff540927" data-raw-source="[&lt;em&gt;EvtDmaEnablerDisable (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540927)"><em>EvtDmaEnablerDisable (KMDF のみ)</em></a>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff541655" data-raw-source="[&lt;em&gt;EvtDmaEnablerFlush (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541655)"><em>EvtDmaEnablerFlush (KMDF のみ)</em> </a>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff540856" data-raw-source="[&lt;em&gt;EvtDeviceD0ExitPreInterruptsDisabled&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540856)"> <em>EvtDeviceD0ExitPreInterruptsDisabled</em></a>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff541714" data-raw-source="[&lt;em&gt;EvtInterruptDisable&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541714)"><em>EvtInterruptDisable</em> </a> 
<a href="https://msdn.microsoft.com/library/windows/hardware/ff540855" data-raw-source="[&lt;em&gt;EvtDeviceD0Exit&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540855)"> <em>EvtDeviceD0Exit</em></a></td>
</tr>
<tr class="even">
<td align="left">↑<a href="https://msdn.microsoft.com/library/windows/hardware/ff551744" data-raw-source="[&lt;strong&gt;IRP_MN_SET_POWER&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551744)"><strong>IRP_MN_SET_POWER</strong> </a> D0 の (電源投入)</td>
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff540848" data-raw-source="[&lt;em&gt;EvtDeviceD0Entry&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540848)"><em>EvtDeviceD0Entry</em></a>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff541730" data-raw-source="[&lt;em&gt;EvtInterruptEnable&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541730)"><em>EvtInterruptEnable</em></a>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff540853" data-raw-source="[&lt;em&gt;EvtDeviceD0EntryPostInterruptsEnabled&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540853)"><em>EvtDeviceD0EntryPostInterruptsEnabled</em> </a> 
<a href="https://msdn.microsoft.com/library/windows/hardware/ff540932" data-raw-source="[&lt;em&gt;EvtDmaEnablerFill (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540932)"> <em>EvtDmaEnablerFill (KMDF のみ)</em></a>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff540929" data-raw-source="[&lt;em&gt;EvtDmaEnablerEnable (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540929)"><em>EvtDmaEnablerEnable (KMDF のみ)</em> </a> 
<a href="https://msdn.microsoft.com/library/windows/hardware/ff541663" data-raw-source="[&lt;em&gt;EvtDmaEnablerSelfManagedIoStart (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541663)"> <em>EvtDmaEnablerSelfManagedIoStart (KMDF のみ)</em></a>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff541779" data-raw-source="[&lt;em&gt;EvtIoResume&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541779)"><em>EvtIoResume</em></a>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff540905" data-raw-source="[&lt;em&gt;EvtDeviceSelfManagedIoRestart&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540905)"><em>EvtDeviceSelfManagedIoRestart</em></a></td>
</tr>
<tr class="odd">
<td align="left">↓<a href="https://msdn.microsoft.com/library/windows/hardware/ff551744" data-raw-source="[&lt;strong&gt;IRP_MN_SET_POWER&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551744)"><strong>IRP_MN_SET_POWER</strong> </a> Sx の</td>
<td align="left">なし</td>
</tr>
<tr class="even">
<td align="left">↑<a href="https://msdn.microsoft.com/library/windows/hardware/ff551744" data-raw-source="[&lt;strong&gt;IRP_MN_SET_POWER&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551744)"><strong>IRP_MN_SET_POWER</strong> </a> Sx の</td>
<td align="left">なし</td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff551644" data-raw-source="[&lt;strong&gt;IRP_MN_POWER_SEQUENCE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551644)"><strong>IRP_MN_POWER_SEQUENCE</strong></a></td>
<td align="left">なし</td>
</tr>
<tr class="even">
<td align="left">↓<a href="https://msdn.microsoft.com/library/windows/hardware/ff551766" data-raw-source="[&lt;strong&gt;IRP_MN_WAIT_WAKE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551766)"><strong>IRP_MN_WAIT_WAKE</strong></a></td>
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff540866" data-raw-source="[&lt;em&gt;EvtDeviceEnableWakeAtBus (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540866)"><em>EvtDeviceEnableWakeAtBus (KMDF のみ)</em></a></td>
</tr>
<tr class="odd">
<td align="left">↑<a href="https://msdn.microsoft.com/library/windows/hardware/ff551766" data-raw-source="[&lt;strong&gt;IRP_MN_WAIT_WAKE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551766)"><strong>IRP_MN_WAIT_WAKE</strong></a></td>
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff540858" data-raw-source="[&lt;em&gt;EvtDeviceDisableWakeAtBus (KMDF only)&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540858)"><em>EvtDeviceDisableWakeAtBus (KMDF のみ)</em></a></td>
</tr>
</tbody>
</table>

 

 

 





