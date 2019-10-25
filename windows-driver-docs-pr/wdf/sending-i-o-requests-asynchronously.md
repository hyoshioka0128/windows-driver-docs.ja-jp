---
title: I/O 要求の非同期送信
description: I/O 要求の非同期送信
ms.assetid: 9f6fb85e-96aa-4945-8c8a-13277beff140
keywords:
- 一般的な i/o は、WDK KMDF をターゲットにし、i/o 要求をに送信します。
- i/o 要求の送信 (WDK KMDF)
- 送信 i/o 要求 (WDK KMDF)、非同期
- i/o 要求の非同期送信 (WDK KMDF)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2b0cd40fe08ebc56a2b13739b9de5fe464de390b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845206"
---
# <a name="sending-io-requests-asynchronously"></a>I/O 要求の非同期送信





I/o 要求を i/o ターゲットに非同期で送信する前に、要求をフォーマットする必要があります。 次の表に、ドライバーが i/o 要求をフォーマットするために呼び出すことができる i/o ターゲットオブジェクトのメソッドを示します。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetformatrequestforread" data-raw-source="[&lt;strong&gt;WdfIoTargetFormatRequestForRead&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetformatrequestforread)"><strong>WdfIoTargetFormatRequestForRead</strong></a></p></td>
<td align="left"><p>読み取り要求の書式を設定します</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetformatrequestforwrite" data-raw-source="[&lt;strong&gt;WdfIoTargetFormatRequestForWrite&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetformatrequestforwrite)"><strong>WdfIoTargetFormatRequestForWrite</strong></a></p></td>
<td align="left"><p>書き込み要求をフォーマットします</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetformatrequestforioctl" data-raw-source="[&lt;strong&gt;WdfIoTargetFormatRequestForIoctl&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetformatrequestforioctl)"><strong>WdfIoTargetFormatRequestForIoctl</strong></a></p></td>
<td align="left"><p>デバイスコントロール要求をフォーマットします</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetformatrequestforinternalioctl" data-raw-source="[&lt;strong&gt;WdfIoTargetFormatRequestForInternalIoctl&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetformatrequestforinternalioctl)"><strong>Wdfiotargetformatrequestfor国際化</strong></a></p></td>
<td align="left"><p>内部デバイスコントロール要求の書式を設定します</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetformatrequestforinternalioctlothers" data-raw-source="[&lt;strong&gt;WdfIoTargetFormatRequestForInternalIoctlOthers&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetformatrequestforinternalioctlothers)"><strong>WdfIoTargetFormatRequestForInternalIoctlOthers</strong></a></p></td>
<td align="left"><p>非標準の内部デバイスコントロール要求を書式設定します</p></td>
</tr>
</tbody>
</table>

 

I/o 要求を非同期に送信するには、ドライバーが次のことを行う必要があります。

1.  要求の書式を設定します。

    前の表に記載されているいずれかの方法を使用して、要求の書式を設定します。 これらのメソッドの使用方法の詳細については、メソッドのリファレンスページを参照してください。

2.  [*補完ルーチン*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nc-wdfrequest-evt_wdf_request_completion_routine)のコールバック関数を登録します。

    要求を非同期で送信する場合は、通常、別のドライバーが各要求を完了したときに、フレームワークによってドライバーに通知する必要があります。 ドライバーは、設定[*ルーチン*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nc-wdfrequest-evt_wdf_request_completion_routine)のコールバック関数を定義し、 [**Wdfrequestset補完ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsetcompletionroutine)を呼び出すことによって登録する必要があります。 詳細については、「 [I/o 要求の完了](completing-i-o-requests.md)」を参照してください。

3.  要求を送信します。

    ドライバーが要求をフォーマットし、完了[*ルーチン*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nc-wdfrequest-evt_wdf_request_completion_routine)のコールバック関数を登録した後、ドライバーは[**Wdfrequestsend**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend)を呼び出す必要があります。 このメソッドを使用すると、 *Requestoptions*パラメーターに設定されているフラグに応じて、同期または非同期のいずれかの方法で要求を送信できます。 I/o 要求を同期的に送信するための簡単な方法については、「[同期的](sending-i-o-requests-synchronously.md)に i/o 要求を送信する」を参照してください。 非同期要求の完了状態を取得する方法、または**Wdfrequestsend**を呼び出して送信される要求については、「 [I/o 要求の完了](completing-i-o-requests.md)」を参照してください。

[**Wdfrequestsend**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend)を呼び出して i/o 要求を送信するドライバーは、後で要求をキャンセルしようとします。 詳細については、「 [I/o 要求のキャンセル](canceling-i-o-requests.md)」を参照してください。

一部のドライバーでは、各要求に対して[**Wdfrequestsend**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend)を複数回呼び出すことによって、複数のデバイスに単一の i/o 要求を送信し、複数の i/o ターゲットに送信する場合があります。 これらのドライバーは、最初の**Wdfrequestsend**の呼び出しの前に、 [**Wdfrequestchangetarget**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestchangetarget)を呼び出して、要求を次の i/o ターゲットに送信できることを確認する必要があります。

 

 





