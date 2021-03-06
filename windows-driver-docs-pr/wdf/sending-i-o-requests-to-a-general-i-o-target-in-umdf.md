---
title: UMDF での一般 I/O ターゲットへの I/O 要求の送信
description: UMDF での一般 I/O ターゲットへの I/O 要求の送信
ms.assetid: f373afa8-292a-47bb-af6f-5035287d1e8c
keywords:
- 一般的な I/O ターゲット WDK UMDF への I/O 要求を送信します。
- WDK UMDF を要求する I/O を送信します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 217e10ce4b5a2ff3e15f19a8069bf24ddb511a9b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376215"
---
# <a name="sending-io-requests-to-a-general-io-target-in-umdf"></a>UMDF での一般 I/O ターゲットへの I/O 要求の送信


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

UMDF ドライバーは、同期または非同期 I/O の一般的なターゲットに I/O 要求を送信できます。

ドライバーは、同期的に I/O 要求を送信する場合、ドライバーのスレッドは、一度に 1 つの要求を送信します。 スレッドは、次の 1 つを送信する前に完了するには、各要求を待機します。 このプロセスは、I/O 要求を非同期的に送信するよりも簡単です。 ドライバーは、多くの要求を送信しない場合、および I/O 要求ごとに、ドライバーが待機中に、システムまたはデバイスのパフォーマンスが低下しない場合、I/O 要求を同期的に送信できます。

ドライバーでは、I/O 要求を非同期的に送信する場合、ドライバーのスレッドは、要求が先に送信された要求を完了を待つことがなく、送信できる状態にするとすぐに各要求を送信します。 処理する場合、ドライバーする必要があります多くの I/O 要求短い時間の期間、ドライバーおそらくを待機できません次の要求を送信する前に完了するには、各要求。 それ以外の場合、ドライバーは、データを失う可能性があります。 またはそのデバイスのおよびシステム全体のパフォーマンスが低下する可能性があります。

UMDF ドライバーは、I/O のターゲットに、I/O 要求を送信することができます、前に、ドライバーは、要求を書式設定する必要があります。 次の表では、ドライバーは、I/O 要求の形式を呼び出すことができるメソッドを示します。 ドライバーは、ドライバーの受信の I/O キューのいずれかで、またはドライバーを作成する要求を書式設定をこれらのメソッドを使用できます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">メソッド</th>
<th align="left">目的</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-formatusingcurrenttype" data-raw-source="[&lt;strong&gt;IWDFIoRequest::FormatUsingCurrentType&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-formatusingcurrenttype)"><strong>IWDFIoRequest::FormatUsingCurrentType</strong></a></p></td>
<td align="left"><p>ドライバーは、ドライバーは、未変更の状態で、ターゲットに、要求を送信できるように、フレームワークから受信要求を書式設定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiotarget-formatrequestforioctl" data-raw-source="[&lt;strong&gt;IWDFIoTarget::FormatRequestForIoctl&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiotarget-formatrequestforioctl)"><strong>IWDFIoTarget::FormatRequestForIoctl</strong></a></p></td>
<td align="left"><p>デバイスの制御要求を形式します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiotarget-formatrequestforread" data-raw-source="[&lt;strong&gt;IWDFIoTarget::FormatRequestForRead&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiotarget-formatrequestforread)"><strong>IWDFIoTarget::FormatRequestForRead</strong></a></p></td>
<td align="left"><p>読み取り要求を書式設定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiotarget-formatrequestforwrite" data-raw-source="[&lt;strong&gt;IWDFIoTarget::FormatRequestForWrite&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiotarget-formatrequestforwrite)"><strong>IWDFIoTarget::FormatRequestForWrite</strong></a></p></td>
<td align="left"><p>書き込み要求を形式します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiotarget2-formatrequestforflush" data-raw-source="[&lt;strong&gt;IWDFIoTarget2::FormatRequestForFlush&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiotarget2-formatrequestforflush)"><strong>IWDFIoTarget2::FormatRequestForFlush</strong></a></p></td>
<td align="left"><p>バッファーをフラッシュする要求を書式設定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiotarget2-formatrequestforqueryinformation" data-raw-source="[&lt;strong&gt;IWDFIoTarget2::FormatRequestForQueryInformation&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiotarget2-formatrequestforqueryinformation)"><strong>IWDFIoTarget2::FormatRequestForQueryInformation</strong></a></p></td>
<td align="left"><p>ファイル情報を取得する要求を書式設定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiotarget2-formatrequestforsetinformation" data-raw-source="[&lt;strong&gt;IWDFIoTarget2::FormatRequestForSetInformation&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiotarget2-formatrequestforsetinformation)"><strong>IWDFIoTarget2::FormatRequestForSetInformation</strong></a></p></td>
<td align="left"><p>ファイル情報を設定する要求を書式設定します。</p></td>
</tr>
</tbody>
</table>

 

ドライバーの呼び出しに I/O ターゲットを I/O 要求を送信する、 [ **IWDFIoRequest::Send** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-send)メソッド。 I/O 要求を同期的に送信する、ドライバーは、WDF を渡します\_要求\_送信\_オプション\_同期フラグを*フラグ*パラメーター。 それ以外の場合、ドライバーは、I/O 要求を非同期的に送信します。 ドライバーは、非同期 I/O 要求を送信する場合、ドライバーで別のドライバーが要求を完了すると、通知が通常必要です。 ドライバーを定義する必要があります、 [ **IRequestCallbackRequestCompletion::OnCompletion** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-irequestcallbackrequestcompletion-oncompletion)コールバック関数を呼び出すことによって、登録、 [ **IWDFIoRequest:。SetCompletionCallback** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-setcompletioncallback)メソッド。 詳細については、次を参照してください。 [I/O 要求の完了](completing-i-o-requests.md)します。

呼び出すドライバー **IWDFIoRequest::Send** 、I/O を送信する要求が呼び出すことによって、要求の後で取り消しを試みることができます、 [ **IWDFIoRequest::CancelSentRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-cancelsentrequest)メソッド。 ドライバー、フレームワークから受信したドライバーをドライバー必要のある常に、I/O 要求をキャンセルした場合は、呼び出すことによって、要求を完了、 [ **IWDFIoRequest::Complete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-complete)または[ **IWDFIoRequest::CompleteWithInformation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-completewithinformation)メソッドを*CompletionStatus*パラメーターの状態に設定\_キャンセルします。 ドライバーを呼び出す場合は、ドライバーは、要求オブジェクトを作成、 [ **IWDFObject::DeleteWdfObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfobject-deletewdfobject)要求を完了するのではなく。

 

 





