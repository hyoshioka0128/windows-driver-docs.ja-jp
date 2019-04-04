---
title: I/O 要求を発行するコードを修正します。
description: I/O 要求を発行するコードを修正します。
ms.assetid: 39E4B6B2-45C8-42B7-811A-EEDCCCB056EF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8bcfaa8cc3ecf1303223c3f80df81fd2d94f7e0d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552811"
---
# <a name="revise-code-that-issues-io-requests"></a>I/O 要求を発行するコードを修正します。


WDF では、ドライバーは、I/O 要求の書式設定を作成して使用できるいくつかのメソッドを定義します。 次の表は、これらのメソッドをまとめたものです。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">KMDF メソッド</th>
<th align="left">アクション</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548604" data-raw-source="[&lt;strong&gt;WdfIoTargetFormatRequestForIoctl&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548604)"><strong>WdfIoTargetFormatRequestForIoctl</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548595" data-raw-source="[&lt;strong&gt;WdfIoTargetFormatRequestForInternalIoctl&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548595)"><strong>WdfIoTargetFormatRequestForInternalIoctl</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548599" data-raw-source="[&lt;strong&gt;WdfIoTargetFormatRequestForInternalIoctlOthers&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548599)"><strong>WdfIoTargetFormatRequestForInternalIoctlOthers</strong></a></p></td>
<td align="left">[次へ] の I/O スタックの場所を手動で書式設定に似ています。</td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548612" data-raw-source="[&lt;strong&gt;WdfIoTargetFormatRequestForRead&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548612)"><strong>WdfIoTargetFormatRequestForRead</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548620" data-raw-source="[&lt;strong&gt;WdfIoTargetFormatRequestForWrite&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548620)"><strong>WdfIoTargetFormatRequestForWrite</strong></a></p></td>
<td align="left">ような<a href="https://msdn.microsoft.com/library/windows/hardware/ff548310" data-raw-source="[&lt;strong&gt;IoBuildAsynchronousFsdRequest&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548310)"> <strong>IoBuildAsynchronousFsdRequest</strong></a>します。</td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548660" data-raw-source="[&lt;strong&gt;WdfIoTargetSendIoctlSynchronously&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548660)"><strong>WdfIoTargetSendIoctlSynchronously</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548656" data-raw-source="[&lt;strong&gt;WdfIoTargetSendInternalIoctlSynchronously&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548656)"><strong>WdfIoTargetSendInternalIoctlSynchronously</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548651" data-raw-source="[&lt;strong&gt;WdfIoTargetSendInternalIoctlOthersSynchronously&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548651)"><strong>WdfIoTargetSendInternalIoctlOthersSynchronously</strong></a></p></td>
<td align="left">ような<a href="https://msdn.microsoft.com/library/windows/hardware/ff548318" data-raw-source="[&lt;strong&gt;IoBuildDeviceIoControlRequest&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548318)"> <strong>IoBuildDeviceIoControlRequest</strong></a>、その後に<a href="https://msdn.microsoft.com/library/windows/hardware/ff548336" data-raw-source="[&lt;strong&gt;IoCallDriver&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548336)"><strong>保留</strong></a>します。</td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548669" data-raw-source="[&lt;strong&gt;WdfIoTargetSendReadSynchronously&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548669)"><strong>WdfIoTargetSendReadSynchronously</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548672" data-raw-source="[&lt;strong&gt;WdfIoTargetSendWriteSynchronously&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548672)"><strong>WdfIoTargetSendWriteSynchronously</strong></a></p></td>
<td align="left">ような<a href="https://msdn.microsoft.com/library/windows/hardware/ff548330" data-raw-source="[&lt;strong&gt;IoBuildSynchronousFsdRequest&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548330)"> <strong>IoBuildSynchronousFsdRequest</strong></a>、その後に<a href="https://msdn.microsoft.com/library/windows/hardware/ff548336" data-raw-source="[&lt;strong&gt;IoCallDriver&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548336)"><strong>保留</strong></a>します。</td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549941" data-raw-source="[&lt;strong&gt;WdfRequestCancelSentRequest&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549941)"><strong>WdfRequestCancelSentRequest</strong></a></p></td>
<td align="left">ような<a href="https://msdn.microsoft.com/library/windows/hardware/ff548338" data-raw-source="[&lt;strong&gt;IoCancelIrp&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548338)"> <strong>IoCancelIrp</strong> </a>で送信された PIRP の<a href="https://msdn.microsoft.com/library/windows/hardware/ff548336" data-raw-source="[&lt;strong&gt;IoCallDriver&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548336)"><strong>保留</strong></a>します。 フレームワークの提供、PIRP の完了または呼び出しの間の解放されていないことに、ロック<strong>保留</strong>と<strong>IoCancelIrp</strong>します。</td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff549951" data-raw-source="[&lt;strong&gt;WdfRequestCreate&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549951)"><strong>WdfRequestCreate</strong></a></td>
<td align="left">ような<a href="https://msdn.microsoft.com/library/windows/hardware/ff548257" data-raw-source="[&lt;strong&gt;IoAllocateIrp&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548257)"> <strong>IoAllocateIrp</strong></a>します。 新しい WDFREQUEST オブジェクトを作成、属性を設定し、呼び出し元のハンドルを返します。</td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff549955" data-raw-source="[&lt;strong&gt;WdfRequestFormatRequestUsingCurrentType&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549955)"><strong>WdfRequestFormatRequestUsingCurrentType</strong></a></td>
<td align="left">ような<a href="https://msdn.microsoft.com/library/windows/hardware/ff549100" data-raw-source="[&lt;strong&gt;IoForwardIrpSynchronously&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549100)"> <strong>IoForwardIrpSynchronously</strong> </a>呼び出されませんが、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff548336" data-raw-source="[&lt;strong&gt;IoCallDriver&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548336)"><strong>保留</strong></a>; ドライバーを呼び出す必要があります<a href="https://msdn.microsoft.com/library/windows/hardware/ff550027" data-raw-source="[&lt;strong&gt;WdfRequestSend&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550027)"> <strong>WdfRequestSend</strong></a>します。</td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550027" data-raw-source="[&lt;strong&gt;WdfRequestSend&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550027)"><strong>WdfRequestSend</strong></a></td>
<td align="left">ような<a href="https://msdn.microsoft.com/library/windows/hardware/ff549100" data-raw-source="[&lt;strong&gt;IoForwardIrpSynchronously&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549100)"> <strong>IoForwardIrpSynchronously</strong> </a>呼び出されませんが、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff548336" data-raw-source="[&lt;strong&gt;IoCallDriver&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548336)"><strong>保留</strong></a>; ドライバーを呼び出す必要があります<a href="https://msdn.microsoft.com/library/windows/hardware/ff550027" data-raw-source="[&lt;strong&gt;WdfRequestSend&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550027)"> <strong>WdfRequestSend</strong></a>します。</td>
</tr>
</tbody>
</table>

 

を別のデバイス スタックを、要求を送信するには、は、WDF ドライバーは、リモートの I/O ターゲットを使用します。 リモートの I/O ターゲットを初期化する方法については、[一般的な I/O のターゲットの初期化](initializing-a-general-i-o-target.md)を参照してください。

非同期要求のまたは呼び出すことによって送信されるすべての要求の完了ステータスを取得する[ **WdfRequestSend**](https://msdn.microsoft.com/library/windows/hardware/ff550027)、ドライバー呼び出し[ **WdfRequestGetStatus**](https://msdn.microsoft.com/library/windows/hardware/ff549974). 同期の要求の状態をすぐに取得できます。 非同期の要求、ドライバーの I/O 完了コールバックは通常の状態を取得します。 同期または非同期要求を送信する方法の詳細については、[一般的な I/O ターゲットへの I/O 要求の送信](sending-i-o-requests-to-general-i-o-targets.md)を参照してください。

 

 





