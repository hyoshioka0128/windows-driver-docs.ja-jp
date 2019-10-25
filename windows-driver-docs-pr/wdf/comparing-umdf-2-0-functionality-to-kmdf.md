---
title: UMDF 2 機能と KMDF の比較
description: このトピックでは、カーネルモードドライバーフレームワーク (KMDF) ドライバーで使用できる機能と、ユーザーモードドライバーフレームワーク (UMDF) 2 ドライバーで使用可能な機能を比較します。
ms.assetid: 9D4DD1A9-DA49-4132-B98F-AFEC8B427272
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9a1509a96f92e4fabc6bf66176268e54e6ccf464
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843649"
---
# <a name="comparing-umdf-2-functionality-to-kmdf"></a>UMDF 2 機能と KMDF の比較


このトピックでは、カーネルモードドライバーフレームワーク (KMDF) ドライバーで使用できる機能と、ユーザーモードドライバーフレームワーク (UMDF) 2 ドライバーで使用可能な機能を比較します。 これは、UMDF 2 ドライバーまたは KMDF ドライバーを記述する必要があるかどうかを判断するのに役立つように設計されています。

UMDF version 2 では、以前は KMDF ドライバーでしか利用できなかった機能の重要なサブセットが提供されていますが、次の機能は KMDF ドライバーでのみ使用できます。 ドライバーがこれらの機能のいずれかを必要とする場合は、KMDF ドライバーを作成する必要があります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">機能</th>
<th align="left">関連情報</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">ダイレクトメモリアクセス (DMA)</td>
<td align="left"><a href="handling-dma-operations-in-kmdf-drivers.md" data-raw-source="[Handling DMA Operations in KMDF Drivers](handling-dma-operations-in-kmdf-drivers.md)">KMDF ドライバーでの DMA 操作の処理</a></td>
</tr>
<tr class="even">
<td align="left">バス列挙型</td>
<td align="left"><a href="enumerating-the-devices-on-a-bus.md" data-raw-source="[Enumerating the Devices on a Bus](enumerating-the-devices-on-a-bus.md)">バス上のデバイスの列挙</a></td>
</tr>
<tr class="odd">
<td align="left">機能的な電源状態 (一部のサポートは UMDF で利用可能です)</td>
<td align="left"><a href="supporting-functional-power-states.md" data-raw-source="[Supporting Functional Power States](supporting-functional-power-states.md)">機能力状態のサポート</a></td>
</tr>
<tr class="even">
<td align="left">WDM オブジェクトと Irp へのアクセス</td>
<td align="left"><a href="obtaining-wdm-information.md" data-raw-source="[Obtaining WDM Information](obtaining-wdm-information.md)">WDM 情報の取得</a></td>
</tr>
<tr class="odd">
<td align="left">バッファーも直接 i/o でもありません</td>
<td align="left"><p><a href="accessing-data-buffers-in-wdf-drivers.md#neither" data-raw-source="[Accessing Data Buffers in WDF Drivers](accessing-data-buffers-in-wdf-drivers.md#neither)">WDF ドライバーのデータバッファーへのアクセス</a></p>
<p><a href="managing-i-o-queues.md#obtaining-requests-from-an-i-o-queue" data-raw-source="[Intercepting an I/O Request before it is Queued](managing-i-o-queues.md#obtaining-requests-from-an-i-o-queue)">I/o 要求をキューに入れる前にインターセプトする</a></p>
<ul>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_io_in_caller_context" data-raw-source="[&lt;em&gt;EvtIoInCallerContext&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_io_in_caller_context)"><em>EvtIoInCallerContext</em></a></li>
</ul></td>
</tr>
<tr class="even">
<td align="left">内部デバイス制御要求 (Ioctl)</td>
<td align="left"><p><a href="sending-i-o-requests-synchronously.md" data-raw-source="[Sending I/O Requests Synchronously](sending-i-o-requests-synchronously.md)">I/o 要求を同期的に送信する</a></p>
<ul>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetsendinternalioctlsynchronously" data-raw-source="[&lt;strong&gt;WdfIoTargetSendInternalIoctlSynchronously&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetsendinternalioctlsynchronously)"><strong>Wdfiotargetsend、同期的に</strong></a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetsendinternalioctlotherssynchronously" data-raw-source="[&lt;strong&gt;WdfIoTargetSendInternalIoctlOthersSynchronously&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetsendinternalioctlotherssynchronously)"><strong>WdfIoTargetSendInternalIoctlOthersSynchronously</strong></a></li>
</ul>
<p><a href="sending-i-o-requests-asynchronously.md" data-raw-source="[Sending I/O Requests Asynchronously](sending-i-o-requests-asynchronously.md)">I/o 要求を非同期に送信する</a></p>
<ul>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetformatrequestforinternalioctl" data-raw-source="[&lt;strong&gt;WdfIoTargetFormatRequestForInternalIoctl&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetformatrequestforinternalioctl)"><strong>Wdfiotargetformatrequestfor国際化</strong></a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetformatrequestforinternalioctlothers" data-raw-source="[&lt;strong&gt;WdfIoTargetFormatRequestForInternalIoctlOthers&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetformatrequestforinternalioctlothers)"><strong>WdfIoTargetFormatRequestForInternalIoctlOthers</strong></a></li>
</ul></td>
</tr>
<tr class="odd">
<td align="left">I/o 要求に対するロックオプトインの解除</td>
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetremovelockoptions" data-raw-source="[&lt;strong&gt;WdfDeviceInitSetRemoveLockOptions&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetremovelockoptions)"><strong>WdfDeviceInitSetRemoveLockOptions</strong></a></td>
</tr>
<tr class="even">
<td align="left">WMI に関するページ</td>
<td align="left"><a href="introduction-to-wmi-for-kmdf-drivers.md" data-raw-source="[Introduction to WMI for KMDF Drivers](introduction-to-wmi-for-kmdf-drivers.md)">KMDF ドライバーの WMI の概要</a></td>
</tr>
</tbody>
</table>

 

ドライバーが上記のいずれかを必要としない場合は、KMDF を使用する代わりに、UMDF 2 ドライバーを記述できます。 2つのフレームワークは多くのインターフェイスを共有するため、必要な場合は後でドライバーを KMDF に変換できます。 UMDF を選択する理由については、「 [Umdf ドライバーを作成する利点](advantages-of-writing-umdf-drivers.md)」を参照してください。

KMDF および UMDF でサポートされているフレームワークオブジェクトとの詳細については、「 [Framework オブジェクトの概要](summary-of-framework-objects.md)」を参照してください。

すべての Windows Driver Framework (WDF) のコールバックとメソッド、およびそれらのフレームワークの適用性を示す表については、「 [WDF のコールバックとメソッドの概要](https://docs.microsoft.com/windows-hardware/drivers/ddi/_wdf/)」を参照してください。

 

 





