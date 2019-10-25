---
title: テープ デバイス制御要求の処理
description: テープ デバイス制御要求の処理
ms.assetid: de6edfc6-9b4b-4866-8fdb-1047b43163de
keywords:
- テープドライバー WDK storage、マッピング状態値
- 記憶域テープドライバー WDK、マッピング状態値
- TAPE_STATUS_SEND_SRB_AND_CALLBACK
- TAPE_STATUS_CHECK_TEST_UNIT_READY
- TAPE_STATUS_CALLBACK
- TAPE_STATUS_REQUIRES_CLEANING
- TAPE_STATUS
- TAPE_STATUS 値のマッピング
- 状態値 WDK テープ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d03df0ec42bb4bfe408db899b83dbb262d0da5b3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842725"
---
# <a name="processing-tape-device-control-requests"></a>テープ デバイス制御要求の処理


## <span id="ddk_processing_tape_device_control_requests_kg"></span><span id="DDK_PROCESSING_TAPE_DEVICE_CONTROL_REQUESTS_KG"></span>


すべての tape miniclass ドライバーは、 [**tape\_status**](https://docs.microsoft.com/windows-hardware/drivers/ddi/minitape/ne-minitape-_tape_status)列挙子に示されている値を使用して状態を報告する必要があります。 ただし、テープクラスドライバーが i/o 制御要求を完了すると、同等の NT 状態値を使用して状態がレポートされます。 次の表は、テープ\_の状態値と、それに対応する NT 状態値とのマッピングを示しています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">NT 状態の値</th>
<th align="left">テープの状態の値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>STATUS_INSUFFICIENT_RESOURCES</p></td>
<td align="left"><p>TAPE_STATUS_INSUFFICIENT_RESOURCES</p></td>
</tr>
<tr class="even">
<td align="left"><p>STATUS_NOT_IMPLEMENTED</p></td>
<td align="left"><p>TAPE_STATUS_NOT_IMPLEMENTED</p></td>
</tr>
<tr class="odd">
<td align="left"><p>STATUS_INVALID_DEVICE_REQUEST</p></td>
<td align="left"><p>TAPE_STATUS_INVALID_DEVICE_REQUEST</p></td>
</tr>
<tr class="even">
<td align="left"><p>STATUS_INVALID_PARAMETER</p></td>
<td align="left"><p>TAPE_STATUS_INVALID_PARAMETER</p></td>
</tr>
<tr class="odd">
<td align="left"><p>STATUS_VERIFY_REQUIRED</p></td>
<td align="left"><p>TAPE_STATUS_MEDIA_CHANGED</p></td>
</tr>
<tr class="even">
<td align="left"><p>STATUS_BUS_RESET</p></td>
<td align="left"><p>TAPE_STATUS_BUS_RESET</p></td>
</tr>
<tr class="odd">
<td align="left"><p>STATUS_SETMARK_DETECTED</p></td>
<td align="left"><p>TAPE_STATUS_SETMARK_DETECTED</p></td>
</tr>
<tr class="even">
<td align="left"><p>STATUS_FILEMARK_DETECTED</p></td>
<td align="left"><p>TAPE_STATUS_FILEMARK_DETECTED</p></td>
</tr>
<tr class="odd">
<td align="left"><p>STATUS_BEGINNING_OF_MEDIA</p></td>
<td align="left"><p>TAPE_STATUS_BEGINNING_OF_MEDIA</p></td>
</tr>
<tr class="even">
<td align="left"><p>STATUS_END_OF_MEDIA</p></td>
<td align="left"><p>TAPE_STATUS_END_OF_MEDIA</p></td>
</tr>
<tr class="odd">
<td align="left"><p>STATUS_BUFFER_OVERFLOW</p></td>
<td align="left"><p>TAPE_STATUS_BUFFER_OVERFLOW</p></td>
</tr>
<tr class="even">
<td align="left"><p>STATUS_NO_DATA_DETECTED</p></td>
<td align="left"><p>TAPE_STATUS_NO_DATA_DETECTED</p></td>
</tr>
<tr class="odd">
<td align="left"><p>STATUS_EOM_OVERFLOW</p></td>
<td align="left"><p>TAPE_STATUS_EOM_OVERFLOW</p></td>
</tr>
<tr class="even">
<td align="left"><p>STATUS_NO_MEDIA</p></td>
<td align="left"><p>TAPE_STATUS_NO_MEDIA</p></td>
</tr>
<tr class="odd">
<td align="left"><p>STATUS_IO_DEVICE_ERROR</p></td>
<td align="left"><p>TAPE_STATUS_IO_DEVICE_ERROR</p></td>
</tr>
<tr class="even">
<td align="left"><p>STATUS_UNRECOGNIZED_MEDIA</p></td>
<td align="left"><p>TAPE_STATUS_UNRECOGNIZED_MEDIA</p></td>
</tr>
<tr class="odd">
<td align="left"><p>STATUS_DEVICE_NOT_READY</p></td>
<td align="left"><p>TAPE_STATUS_DEVICE_NOT_READY</p></td>
</tr>
<tr class="even">
<td align="left"><p>STATUS_MEDIA_WRITE_PROTECTED</p></td>
<td align="left"><p>TAPE_STATUS_MEDIA_WRITE_PROTECTED</p></td>
</tr>
<tr class="odd">
<td align="left"><p>STATUS_DEVICE_DATA_ERROR</p></td>
<td align="left"><p>TAPE_STATUS_DEVICE_DATA_ERROR</p></td>
</tr>
<tr class="even">
<td align="left"><p>STATUS_NO_SUCH_DEVICE</p></td>
<td align="left"><p>TAPE_STATUS_NO_SUCH_DEVICE</p></td>
</tr>
<tr class="odd">
<td align="left"><p>STATUS_INVALID_BLOCK_LENGTH</p></td>
<td align="left"><p>TAPE_STATUS_INVALID_BLOCK_LENGTH</p></td>
</tr>
<tr class="even">
<td align="left"><p>STATUS_IO_TIMEOUT</p></td>
<td align="left"><p>TAPE_STATUS_IO_TIMEOUT</p></td>
</tr>
<tr class="odd">
<td align="left"><p>STATUS_DEVICE_NOT_CONNECTED</p></td>
<td align="left"><p>TAPE_STATUS_DEVICE_NOT_CONNECTED</p></td>
</tr>
<tr class="even">
<td align="left"><p>STATUS_DATA_OVERRUN</p></td>
<td align="left"><p>TAPE_STATUS_DATA_OVERRUN</p></td>
</tr>
<tr class="odd">
<td align="left"><p>STATUS_DEVICE_BUSY</p></td>
<td align="left"><p>TAPE_STATUS_DEVICE_BUSY</p></td>
</tr>
<tr class="even">
<td align="left"><p>STATUS_DEVICE_REQUIRES_CLEANING</p></td>
<td align="left"><p>TAPE_STATUS_REQUIRES_CLEANING</p></td>
</tr>
<tr class="odd">
<td align="left"><p>STATUS_CLEANER_CARTRIDGE_INSTALLED</p></td>
<td align="left"><p>TAPE_STATUS_CLEANER_CARTRIDGE_INSTALLED</p></td>
</tr>
</tbody>
</table>

 

クラスドライバーが要求を完了するために miniclass ルーチンを2回以上呼び出す必要がある場合、miniclass ドライバーは、要求が完了したかどうか、またはルーチンを再度呼び出す必要があるかどうかを示すために、リターンステータスを使用します。 Tape クラスドライバーは、指定された要求に対して miniclass ルーチンを呼び出した回数の0から始まるカウントを保持し、そのカウントを*Callnumber*パラメーターとしてルーチンに渡します。

Miniclass ルーチンは、次のいずれかの状態値を返して、クラスドライバーがルーチンを再度呼び出す必要があることを示します。

-   テープ\_の状態\_送信\_SRB\_と\_コールバック

    この戻り値は、SRB をデバイスに送信するようにテープクラスドライバーに指示します。 通常、tape miniclass ルーチンは、テープクラスドライバーによって渡された SRB を入力した後に、この状態を返します。 操作が成功した場合、クラスドライバーは*Callnumber*をインクリメントし、miniclass ルーチンを再度呼び出します。 SRB が失敗した場合は、 *Retryflags*の値に応じて、クラスドライバーは miniclass ルーチンを再度呼び出します。

-   テープ\_の状態\_テスト\_ユニット\_準備完了\_を確認する

    この戻り値は、テープクラスドライバーに対して、テスト単位の準備ができたコマンドの SRB を作成し、SRB をデバイスに送信するように指示します。

-   テープ\_の状態\_コールバック

    この戻り値は、SRB をデバイスに送信せずに、テープクラスドライバーに、 *Callnumber*をインクリメントするように指示します。 これにより、複数のデバイスをサポートするケースステートメントが合理化されます。 たとえば、特定の miniclass ドライバーでサポートされているほとんどのテープデバイスで、特定の要求を処理するために3つの SRBs が必要であるとします。 ただし、1つのデバイスには最初と3番目の SRBs のみが必要です。 一意のデバイスの場合、tape miniclass ドライバーは、テープ\_の状態\_コールバックを返して2番目の SRB をスキップします。これにより、ドライバーは同じコードを使用して、サポートされているすべてのデバイスの要求を処理することができます。

-   テープ\_の状態\_には\_クリーニングが必要です

    テープデバイスが、エラーではなく、sense data でのクリーニング通知をサポートしている場合、tape miniclass ドライバーの TapeMiniGetStatus ルーチンは、ドライブのクリーニングが必要であることをテープクラスドライバーに示すためにこの状態を返します。

Miniclass ルーチンが要求の処理を終了したとき (正常に完了した場合、または再試行が終了した後にエラーが発生した場合)、テープクラスドライバーに返されます。この場合、\_テープの状態\_*XXX*に戻り、申請.

 

 




