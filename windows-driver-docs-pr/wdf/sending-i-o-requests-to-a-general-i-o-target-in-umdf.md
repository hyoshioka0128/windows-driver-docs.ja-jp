---
title: UMDF での一般 I/O ターゲットへの I/O 要求の送信
description: UMDF での一般 I/O ターゲットへの I/O 要求の送信
ms.assetid: f373afa8-292a-47bb-af6f-5035287d1e8c
keywords:
- 一般的な i/o ターゲット WDK UMDF、i/o 要求を送信する
- i/o 要求の送信 (WDK UMDF)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1923744538f2dbbb40a266b07d68b95fb0889543
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75209948"
---
# <a name="sending-io-requests-to-a-general-io-target-in-umdf"></a>UMDF での一般 I/O ターゲットへの I/O 要求の送信


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

UMDF ドライバーは、i/o 要求を一般 i/o ターゲットに同期または非同期で送信できます。

ドライバーが i/o 要求を同期的に送信する場合、ドライバースレッドは一度に1つずつ要求を送信します。 スレッドは、要求が完了するまで待機してから、次の要求を送信します。 このプロセスは、i/o 要求を非同期的に送信するよりも簡単です。 ドライバーは、多数の要求を送信しない場合や、ドライバーが各 i/o 要求を待機している間にシステムまたはデバイスのパフォーマンスが低下しない場合に、i/o 要求を同期的に送信できます。

ドライバーが i/o 要求を非同期で送信する場合、ドライバースレッドは、要求が送信される準備が整うとすぐに各要求を送信します。これは、以前に送信された要求が終了するまで待機する必要がありません。 ドライバーが多数の i/o 要求を短時間処理する必要がある場合、ドライバーは、要求が完了するまで待機してから次の要求を送信することはできません。 そうしないと、ドライバーによってデータが失われたり、デバイスのパフォーマンスが低下したり、場合によってはシステム全体が縮小される可能性があります。

UMDF ドライバーが i/o 要求を i/o ターゲットに送信する前に、ドライバーが要求をフォーマットする必要があります。 次の表は、ドライバーが i/o 要求をフォーマットするために呼び出すことができるメソッドを示しています。 ドライバーは、これらのメソッドを使用して、ドライバーが i/o キューまたは作成したドライバーのいずれかで受信した要求をフォーマットできます。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-formatusingcurrenttype" data-raw-source="[&lt;strong&gt;IWDFIoRequest::FormatUsingCurrentType&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-formatusingcurrenttype)"><strong>IWDFIoRequest:: Format使い方 Currenttype</strong></a></p></td>
<td align="left"><p>ドライバーが要求を変更されていない要求をターゲットに送信できるように、ドライバーがフレームワークから受信した要求を書式設定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotarget-formatrequestforioctl" data-raw-source="[&lt;strong&gt;IWDFIoTarget::FormatRequestForIoctl&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotarget-formatrequestforioctl)"><strong>IWDFIoTarget:: FormatRequestForIoctl</strong></a></p></td>
<td align="left"><p>デバイスコントロール要求をフォーマットします</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotarget-formatrequestforread" data-raw-source="[&lt;strong&gt;IWDFIoTarget::FormatRequestForRead&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotarget-formatrequestforread)"><strong>IWDFIoTarget:: FormatRequestForRead</strong></a></p></td>
<td align="left"><p>読み取り要求の書式を設定します</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotarget-formatrequestforwrite" data-raw-source="[&lt;strong&gt;IWDFIoTarget::FormatRequestForWrite&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotarget-formatrequestforwrite)"><strong>IWDFIoTarget:: FormatRequestForWrite</strong></a></p></td>
<td align="left"><p>書き込み要求をフォーマットします</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotarget2-formatrequestforflush" data-raw-source="[&lt;strong&gt;IWDFIoTarget2::FormatRequestForFlush&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotarget2-formatrequestforflush)"><strong>IWDFIoTarget2:: FormatRequestForFlush</strong></a></p></td>
<td align="left"><p>バッファーをフラッシュする要求をフォーマットします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotarget2-formatrequestforqueryinformation" data-raw-source="[&lt;strong&gt;IWDFIoTarget2::FormatRequestForQueryInformation&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotarget2-formatrequestforqueryinformation)"><strong>IWDFIoTarget2:: FormatRequestForQueryInformation</strong></a></p></td>
<td align="left"><p>ファイル情報を取得する要求を書式設定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotarget2-formatrequestforsetinformation" data-raw-source="[&lt;strong&gt;IWDFIoTarget2::FormatRequestForSetInformation&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotarget2-formatrequestforsetinformation)"><strong>IWDFIoTarget2:: FormatRequestForSetInformation</strong></a></p></td>
<td align="left"><p>ファイル情報を設定する要求をフォーマットします。</p></td>
</tr>
</tbody>
</table>

 

I/o 要求を i/o ターゲットに送信するために、ドライバーは[**IWDFIoRequest:: send**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-send)メソッドを呼び出します。 I/o 要求を同期的に送信するために、ドライバーは WDF\_要求を渡し、\_オプション\_同期フラグを*Flags*パラメーターに送信\_ます。 それ以外の場合、ドライバーは i/o 要求を非同期的に送信します。 ドライバーが i/o 要求を非同期に送信する場合、ドライバーは通常、別のドライバーが要求を完了するときに通知を必要とします。 ドライバーは、 [**Irequestcallback Requestcompletion:: OnCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-irequestcallbackrequestcompletion-oncompletion)コールバック関数を定義し、 [**IWDFIoRequest:: setcompletion callback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-setcompletioncallback)メソッドを呼び出すことによって登録する必要があります。 詳細については、「 [I/o 要求の完了](completing-i-o-requests.md)」を参照してください。

I/o 要求を送信するために**IWDFIoRequest:: send**を呼び出すドライバーは、後で[**IWDFIoRequest:: 中断 request**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-cancelsentrequest)メソッドを呼び出すことによって要求をキャンセルしようとします。 ドライバーがフレームワークから受け取った i/o 要求をキャンセルした場合、ドライバーは、 [**IWDFIoRequest:: complete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-complete)または[**IWDFIoRequest:: completewithinformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-completewithinformation)メソッドを呼び出すことによって、常に要求を完了する必要があります。これには、COMPLETED*ステータス*パラメーターを status\_キャンセルに設定します。 ドライバーが要求オブジェクトを作成した場合、ドライバーは要求を完了するのではなく、 [**Iwdfobject::D eletewdfobject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfobject-deletewdfobject)を呼び出します。

 

 





