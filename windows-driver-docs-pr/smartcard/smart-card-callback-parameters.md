---
title: スマート カードのコールバック パラメーター
description: スマート カードのコールバック パラメーター
ms.assetid: 6fd1590b-0600-4065-b1cc-71d8aed3f98a
keywords:
- Ioctl WDK スマートカード
- コールバックパラメーター WDK スマートカード
- ベンダー提供のドライバー WDK スマートカード、IOCTL 要求の管理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 102a2bb5f963451bacd44312af7c38cb0dddcb17
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842614"
---
# <a name="smart-card-callback-parameters"></a>スマート カードのコールバック パラメーター


## <span id="_ntovr_smart_card_callback_parameters"></span><span id="_NTOVR_SMART_CARD_CALLBACK_PARAMETERS"></span>


Ioctl を除くすべての IOCTL 要求について[ **\_は\_スマートカード\_が**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548905(v=vs.85))存在しません。また、 [**IOCTL\_スマートカード\_が存在\_** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548906(v=vs.85))場合は、 [**SMARTCARDDEVICECONTROL (WDM)** ](https://docs.microsoft.com/previous-versions/ff548939(v=vs.85))によって**IoRequest**メンバーが初期化されます。コールバックルーチンを呼び出す前の[**スマートカード\_拡張機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/smclib/ns-smclib-_smartcard_extension)の構造体。 次の表は、 **Smartcarddevicecontrol**によって実行される初期化の種類を示しています。

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
<td align="left"><p><strong>IoRequest</strong></p></td>
<td align="left"><p>このメンバーが指すバッファー内のカードに送信されるユーザーデータを格納します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>IoRequest の長さ</strong></p></td>
<td align="left"><p>このメンバーのユーザーバッファーの長さを格納します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>IoRequest.ReplyBuffer</strong></p></td>
<td align="left"><p>スマートカードによって返されるデータを、このメンバーが指すバッファーに格納します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>IoRequest.ReplyBufferLength</strong></p></td>
<td align="left"><p>このメンバーの応答バッファーのサイズを格納します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>IoRequest</strong></p></td>
<td align="left"><p>このメンバーが指す変数のカードから実際に受信したバイト数を格納します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>MajorIoControlCode</strong></p></td>
<td align="left"><p>このメンバーに、IOCTL 要求の主要な i/o 制御コードを格納します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>MinorIoControlCode</strong></p></td>
<td align="left"><p>このメンバーに IOCTL 要求のマイナー i/o 制御コード (存在する場合) を格納します。</p></td>
</tr>
</tbody>
</table>

 

**Smartcardextension-&gt;OsData**によって示される構造は、次の表に示すように設定されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">メンバー</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>% Entirp</strong></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548905(v=vs.85)" data-raw-source="[&lt;strong&gt;IOCTL_SMARTCARD_IS_ABSENT&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548905(v=vs.85))"><strong>IOCTL_SMARTCARD_IS_ABSENT</strong></a>と<a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548906(v=vs.85)" data-raw-source="[&lt;strong&gt;IOCTL_SMARTCARD_IS_PRESENT&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548906(v=vs.85))"><strong>IOCTL_SMARTCARD_IS_PRESENT</strong></a>を除くすべてのコントロール要求に対して、要求元の IRP へのポインターを受け取ります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>NotificationIrp</strong></p></td>
<td align="left"><p>IOCTL_SMARTCARD_IS_ABSENT または IOCTL_SMARTCARD_IS_PRESENT control 要求に対して、要求元の IRP へのポインターを受け取ります。</p></td>
</tr>
</tbody>
</table>

 

 

 





