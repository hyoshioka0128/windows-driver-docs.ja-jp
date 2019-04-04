---
title: UMDF 2 を比較する KMDF の機能
description: このトピックでは、カーネル モード ドライバー フレームワーク (KMDF) ドライバーを利用できる機能を比較します。 ユーザー モード ドライバー フレームワーク (UMDF) 2 ドライバーを利用できます。
ms.assetid: 9D4DD1A9-DA49-4132-B98F-AFEC8B427272
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 354219205dd2d52df290fe01d1d5fe7e2143cb34
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557672"
---
# <a name="comparing-umdf-2-functionality-to-kmdf"></a>UMDF 2 を比較する KMDF の機能


このトピックでは、カーネル モード ドライバー フレームワーク (KMDF) ドライバーを利用できる機能を比較します。 ユーザー モード ドライバー フレームワーク (UMDF) 2 ドライバーを利用できます。 2 の UMDF ドライバーまたは KMDF ドライバーを記述する必要があるかどうかを判断できるように設計されています。

UMDF バージョン 2 では、KMDF ドライバーにのみ使用可能だった機能の重要なサブセットを提供する、次の機能は KMDF ドライバーでのみ使用できます。 ドライバーでは、これらの機能の 1 つ必要とする場合は、KMDF ドライバーを記述する必要があります。

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
<td align="left">ダイレクト メモリ アクセス (DMA)</td>
<td align="left"><a href="handling-dma-operations-in-kmdf-drivers.md" data-raw-source="[Handling DMA Operations in KMDF Drivers](handling-dma-operations-in-kmdf-drivers.md)">KMDF ドライバーで DMA 操作の処理</a></td>
</tr>
<tr class="even">
<td align="left">バスの列挙型</td>
<td align="left"><a href="enumerating-the-devices-on-a-bus.md" data-raw-source="[Enumerating the Devices on a Bus](enumerating-the-devices-on-a-bus.md)">バス上のデバイスを列挙します。</a></td>
</tr>
<tr class="odd">
<td align="left">機能の電源の状態 (UMDF で使用できるは、制限付きサポートです)</td>
<td align="left"><a href="supporting-functional-power-states.md" data-raw-source="[Supporting Functional Power States](supporting-functional-power-states.md)">電源状態の機能をサポートしています。</a></td>
</tr>
<tr class="even">
<td align="left">WDM オブジェクトと Irp へのアクセス</td>
<td align="left"><a href="obtaining-wdm-information.md" data-raw-source="[Obtaining WDM Information](obtaining-wdm-information.md)">WDM 情報を取得します。</a></td>
</tr>
<tr class="odd">
<td align="left">バッファーもダイレクト I/O</td>
<td align="left"><p><a href="accessing-data-buffers-in-wdf-drivers.md#neither" data-raw-source="[Accessing Data Buffers in WDF Drivers](accessing-data-buffers-in-wdf-drivers.md#neither)">WDF のドライバーでのデータ バッファーへのアクセス</a></p>
<p><a href="managing-i-o-queues.md#obtaining-requests-from-an-i-o-queue" data-raw-source="[Intercepting an I/O Request before it is Queued](managing-i-o-queues.md#obtaining-requests-from-an-i-o-queue)">キューに配置する前に、I/O 要求をインターセプト</a></p>
<ul>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/ff541764" data-raw-source="[&lt;em&gt;EvtIoInCallerContext&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541764)"><em>EvtIoInCallerContext</em></a></li>
</ul></td>
</tr>
<tr class="even">
<td align="left">内部デバイスの制御 (Ioctl) を要求します。</td>
<td align="left"><p><a href="sending-i-o-requests-synchronously.md" data-raw-source="[Sending I/O Requests Synchronously](sending-i-o-requests-synchronously.md)">I/O 要求を同期的に送信します。</a></p>
<ul>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/ff548656" data-raw-source="[&lt;strong&gt;WdfIoTargetSendInternalIoctlSynchronously&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548656)"><strong>WdfIoTargetSendInternalIoctlSynchronously</strong></a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/ff548651" data-raw-source="[&lt;strong&gt;WdfIoTargetSendInternalIoctlOthersSynchronously&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548651)"><strong>WdfIoTargetSendInternalIoctlOthersSynchronously</strong></a></li>
</ul>
<p><a href="sending-i-o-requests-asynchronously.md" data-raw-source="[Sending I/O Requests Asynchronously](sending-i-o-requests-asynchronously.md)">非同期 I/O 要求を送信</a></p>
<ul>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/ff548595" data-raw-source="[&lt;strong&gt;WdfIoTargetFormatRequestForInternalIoctl&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548595)"><strong>WdfIoTargetFormatRequestForInternalIoctl</strong></a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/ff548599" data-raw-source="[&lt;strong&gt;WdfIoTargetFormatRequestForInternalIoctlOthers&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548599)"><strong>WdfIoTargetFormatRequestForInternalIoctlOthers</strong></a></li>
</ul></td>
</tr>
<tr class="odd">
<td align="left">ロックのオプトインの I/O 要求を削除します。</td>
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/hh451095" data-raw-source="[&lt;strong&gt;WdfDeviceInitSetRemoveLockOptions&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh451095)"><strong>WdfDeviceInitSetRemoveLockOptions</strong></a></td>
</tr>
<tr class="even">
<td align="left">WMI に関するページ</td>
<td align="left"><a href="introduction-to-wmi-for-kmdf-drivers.md" data-raw-source="[Introduction to WMI for KMDF Drivers](introduction-to-wmi-for-kmdf-drivers.md)">KMDF ドライバーの WMI の概要</a></td>
</tr>
</tbody>
</table>

 

ドライバーが、上記のいずれにも不要な場合は、KMDF を使用する代わりに 2 の UMDF ドライバーを記述できます。 2 つのフレームワークでは、多くのインターフェイスを共有するために変換できます、ドライバー KMDF 後で必要になった場合。 UMDF を選択する理由については、[書き込み UMDF ドライバーの利点](advantages-of-writing-umdf-drivers.md)を参照してください。

Framework のオブジェクトおよび KMDF して UMDF サポートの詳細については、[Framework オブジェクトの概要](summary-of-framework-objects.md)を参照してください。

Windows Driver Frameworks (WDF) のすべてのコールバック メソッドと、フレームワークの適用性を示す表を参照してください[WDF のコールバックの概要とメソッド](https://msdn.microsoft.com/library/windows/hardware/dn265591)します。

 

 





