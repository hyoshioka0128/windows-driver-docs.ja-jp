---
title: テープ デバイス制御要求の処理
description: テープ デバイス制御要求の処理
ms.assetid: de6edfc6-9b4b-4866-8fdb-1047b43163de
keywords:
- テープ ドライバー WDK ストレージは、状態の値のマッピング
- テープ記憶装置ドライバー WDK、状態の値のマッピング
- TAPE_STATUS_SEND_SRB_AND_CALLBACK
- TAPE_STATUS_CHECK_TEST_UNIT_READY
- TAPE_STATUS_CALLBACK
- TAPE_STATUS_REQUIRES_CLEANING
- TAPE_STATUS
- TAPE_STATUS 値のマッピング
- 状態値 WDK テープ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 06195bcdc418417fb497bdbacb6d9313d8af51b2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366274"
---
# <a name="processing-tape-device-control-requests"></a>テープ デバイス制御要求の処理


## <span id="ddk_processing_tape_device_control_requests_kg"></span><span id="DDK_PROCESSING_TAPE_DEVICE_CONTROL_REQUESTS_KG"></span>


すべてのテープ miniclass ドライバーに記載した値を使用して状態を報告する必要があります、 [**テープ\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff567975)列挙子。 ただし、テープのクラス ドライバーには、I/O のコントロール要求が完了するは、対応する NT ステータス値を使用して状態を報告します。 次の表に、テープの間のマッピング\_状態の値とその同等 NT 状態の値。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">NT ステータス値</th>
<th align="left">テープの状態値</th>
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
<td align="left"><p>0XC000000ESTATUS_NO_SUCH_DEVICE</p></td>
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

 

クラス ドライバーは、要求を完了するのに miniclass ルーチンを複数回呼び出す必要があります、たびに、miniclass ドライバーは、要求が完了するかどうか、または、ルーチンが再度呼び出されるかどうかを示す戻り値の状態を使用します。 テープのクラス ドライバーは、特定の要求ととしてルーチンに渡すカウント miniclass ルーチンが呼び出される回数の 0 から始まるカウントを保持、 *CallNumber*パラメーター。

Miniclass ルーチンでは、クラス ドライバーが、ルーチンをもう一度呼び出す必要があることを示す状態値は次のいずれかを返します。

-   テープ\_状態\_送信\_SRB\_AND\_コールバック

    この戻り値では、テープのクラス ドライバー、SRB をデバイスに送信するよう指示します。 通常、テープ miniclass ルーチンでは、テープ クラス ドライバーを渡し、SRB で入力した後にこの状態を返します。 操作が成功した場合のクラス ドライバー単位*CallNumber* miniclass ルーチンをもう一度呼び出すとします。 クラスのドライバーの値に応じてもう一度 miniclass ルーチンを呼び出すと、SRB が失敗した場合、 *RetryFlags*します。

-   テープ\_状態\_確認\_テスト\_単位\_準備完了

    この戻り値では、テープ クラス ドライバーを SRB のテスト単位の準備がコマンドを作成し、SRB をデバイスに送信するよう指示します。

-   テープ\_状態\_コールバック

    これは、値をインクリメントするテープ クラス ドライバーに指示が返される*CallNumber* SRB をデバイスに送信せずにします。 これには、複数のデバイスをサポートするケースのステートメントが効率化します。 たとえば、ほとんどの特定の miniclass ドライバーでサポートされるテープ デバイスが特定の要求を処理する 3 つのされる Srb を必要とします。 1 つのデバイスには、のみ、最初と 3 番目される Srb ただし、必要があります。 一意のデバイスのテープ miniclass ドライバーがテープを返すことができます\_状態\_同じコードを使用して、サポートされるすべてのデバイスの要求を処理するドライバーを許可する、2 つ目の SRB をスキップするコールバック。

-   テープ\_状態\_REQUIRES\_クリーニング

    テープ デバイスは、エラーとしてではなく、センス データのクリーニングの通知をサポートする場合、テープ miniclass ドライバーの TapeMiniGetStatus ルーチンは、ドライブのクリーニングが必要するテープ クラス ドライバーに示すためにこの状態を返します。

Miniclass ルーチンの要求の処理が終了したとき-テープをテープ クラス ドライバーに返すに成功するか、エラーの再試行--後で\_状態\_*XXX*を示す成功した場合または要求の失敗。

 

 




