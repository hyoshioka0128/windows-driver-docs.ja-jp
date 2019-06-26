---
title: スマート カードのコールバック パラメーター
description: スマート カードのコールバック パラメーター
ms.assetid: 6fd1590b-0600-4065-b1cc-71d8aed3f98a
keywords:
- Ioctl WDK のスマート カード
- コールバック パラメーター WDK のスマート カード
- ベンダーから提供されたドライバー WDK スマート カード、IOCTL 要求の管理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d68ee5becb45e0362b10f619c36b208e47c51811
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356667"
---
# <a name="smart-card-callback-parameters"></a>スマート カードのコールバック パラメーター


## <span id="_ntovr_smart_card_callback_parameters"></span><span id="_NTOVR_SMART_CARD_CALLBACK_PARAMETERS"></span>


除くすべての IOCTL 要求[ **IOCTL\_スマート カード\_IS\_ABSENT** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548905(v=vs.85))と[ **IOCTL\_スマートカード\_\_存在**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548906(v=vs.85))、 [ **SmartcardDeviceControl (WDM)** ](https://docs.microsoft.com/previous-versions/ff548939(v=vs.85))を初期化します、 **IoRequest**のメンバー、[**スマート カード\_拡張子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/smclib/ns-smclib-_smartcard_extension)コールバック ルーチンを呼び出す前に構造体します。 次の表は、初期化の種類を示している**SmartcardDeviceControl**を実行します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">IoRequest のメンバー</th>
<th align="left">SmartcardDeviceControl によって実行される初期化</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>IoRequest.RequestBuffer</strong></p></td>
<td align="left"><p>このメンバーが指すバッファーには、カードに送信されるユーザー データを格納します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>IoRequest.RequestBufferLength</strong></p></td>
<td align="left"><p>このメンバーには、ユーザーのバッファーの長さを格納します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>IoRequest.ReplyBuffer</strong></p></td>
<td align="left"><p>このメンバーが指すバッファーにスマート カードによって返されるデータを格納します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>IoRequest.ReplyBufferLength</strong></p></td>
<td align="left"><p>このメンバーには、応答のバッファーのサイズを格納します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>IoRequest.Information</strong></p></td>
<td align="left"><p>このメンバーが指す変数には、カードから実際に受信したバイト数を格納します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>MajorIoControlCode</strong></p></td>
<td align="left"><p>このメンバーには、IOCTL 要求の主要な I/O 制御コードを格納します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>MinorIoControlCode</strong></p></td>
<td align="left"><p>このメンバーには、IOCTL 要求のマイナーの I/O 制御コード (ある場合) を格納します。</p></td>
</tr>
</tbody>
</table>

 

によって示される構造**SmartcardExtension -&gt;OsData**次の表に示すように設定されています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Member</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>CurrentIrp</strong></p></td>
<td align="left"><p>除くすべてのコントロール要求の要求元の IRP へのポインターを受け取る<a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548905(v=vs.85)" data-raw-source="[&lt;strong&gt;IOCTL_SMARTCARD_IS_ABSENT&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548905(v=vs.85))"> <strong>IOCTL_SMARTCARD_IS_ABSENT</strong> </a>と<a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548906(v=vs.85)" data-raw-source="[&lt;strong&gt;IOCTL_SMARTCARD_IS_PRESENT&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548906(v=vs.85))"> <strong>IOCTL_SMARTCARD_IS_PRESENT</strong> </a>.</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>NotificationIrp</strong></p></td>
<td align="left"><p>IOCTL_SMARTCARD_IS_ABSENT または IOCTL_SMARTCARD_IS_PRESENT 制御要求の要求元の IRP へのポインターを受け取ります。</p></td>
</tr>
</tbody>
</table>

 

 

 





