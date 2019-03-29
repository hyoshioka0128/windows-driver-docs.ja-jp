---
title: I/O 要求の非同期送信
description: I/O 要求の非同期送信
ms.assetid: 9f6fb85e-96aa-4945-8c8a-13277beff140
keywords:
- 一般的な I/O ターゲット WDK KMDF への I/O 要求を送信します。
- WDK KMDF を要求する I/O を送信します。
- 送信 I/O WDK KMDF、非同期の要求します。
- WDK KMDF の I/O 要求を非同期的に送信します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 510680f227b141bfe941823b1c17de09629fd443
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571314"
---
# <a name="sending-io-requests-asynchronously"></a>I/O 要求の非同期送信





I/O 要求を非同期的に送信するには I/O のターゲットに、前に、要求の書式を設定する必要があります。 次の表では、I/O 要求の書式設定するには、ドライバーを呼び出すことができる I/O ターゲット オブジェクトのメソッドを示します。

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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548612" data-raw-source="[&lt;strong&gt;WdfIoTargetFormatRequestForRead&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548612)"><strong>WdfIoTargetFormatRequestForRead</strong></a></p></td>
<td align="left"><p>読み取り要求を書式設定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548620" data-raw-source="[&lt;strong&gt;WdfIoTargetFormatRequestForWrite&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548620)"><strong>WdfIoTargetFormatRequestForWrite</strong></a></p></td>
<td align="left"><p>書き込み要求を形式します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548604" data-raw-source="[&lt;strong&gt;WdfIoTargetFormatRequestForIoctl&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548604)"><strong>WdfIoTargetFormatRequestForIoctl</strong></a></p></td>
<td align="left"><p>デバイスの制御要求を形式します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548595" data-raw-source="[&lt;strong&gt;WdfIoTargetFormatRequestForInternalIoctl&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548595)"><strong>WdfIoTargetFormatRequestForInternalIoctl</strong></a></p></td>
<td align="left"><p>内部デバイスの制御要求を形式します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548599" data-raw-source="[&lt;strong&gt;WdfIoTargetFormatRequestForInternalIoctlOthers&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548599)"><strong>WdfIoTargetFormatRequestForInternalIoctlOthers</strong></a></p></td>
<td align="left"><p>非標準の内部デバイス制御の要求を書式設定します。</p></td>
</tr>
</tbody>
</table>

 

I/O 要求を非同期的に送信するには、ドライバーが必要です。

1.  要求の書式を設定します。

    要求を書式設定する前の表に記載されているメソッドのいずれかを使用します。 これらのメソッドを使用する方法の詳細については、メソッドのリファレンス ページを参照してください。

2.  登録、 [ *CompletionRoutine* ](https://msdn.microsoft.com/library/windows/hardware/ff540745)コールバック関数。

    要求を非同期的に送信する場合は、別のドライバーが各要求を完了すると、ドライバーに通知するためにフレームワーク通常します。 ドライバーを定義する必要があります、 [ *CompletionRoutine* ](https://msdn.microsoft.com/library/windows/hardware/ff540745)コールバック関数を呼び出すことによって登録[ **WdfRequestSetCompletionRoutine** ](https://msdn.microsoft.com/library/windows/hardware/ff550030). 詳細については、次を参照してください。 [I/O 要求の完了](completing-i-o-requests.md)します。

3.  要求を送信します。

    ドライバーの後に要求をフォーマットし、登録、 [ *CompletionRoutine* ](https://msdn.microsoft.com/library/windows/hardware/ff540745)コールバック関数には、ドライバーが呼び出す必要があります[ **WdfRequestSend** ](https://msdn.microsoft.com/library/windows/hardware/ff550027). このメソッド設定されているフラグによって同期的または非同期的に要求を送信することができます、 *RequestOptions*パラメーター。 I/O 要求を同期的に送信する簡単な方法は、次を参照してください。[同期に I/O 要求を送信する](sending-i-o-requests-synchronously.md)します。 非同期要求のまたは呼び出すことによって送信されるすべての要求の完了ステータスを取得する方法については**WdfRequestSend**を参照してください[I/O 要求の完了](completing-i-o-requests.md)します。

呼び出すドライバー [ **WdfRequestSend** ](https://msdn.microsoft.com/library/windows/hardware/ff550027) I/O を送信する要求は後で要求の取り消しを試行できます。 詳細については、次を参照してください。 [I/O 要求のキャンセル](canceling-i-o-requests.md)します。

一部のドライバーは、複数のデバイスを 1 つの I/O 要求を送信する可能性があり、複数の I/O が対象とそのため、呼び出すことによって[ **WdfRequestSend** ](https://msdn.microsoft.com/library/windows/hardware/ff550027)要求ごとに 2 回以上。 これらのドライバーを呼び出す必要があります[ **WdfRequestChangeTarget** ](https://msdn.microsoft.com/library/windows/hardware/ff549943)への各呼び出しの前に**WdfRequestSend** I/O ターゲットを次に、要求を送信できることを確認する 1 つ目の後にします。

 

 





