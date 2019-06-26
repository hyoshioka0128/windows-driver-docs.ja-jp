---
title: 低速 I/O ルーチン
description: 低速 I/O ルーチン
ms.assetid: 5317917d-9abc-43f9-ab4a-f070e491c816
keywords:
- RDBSS WDK ファイル システム、低の入出力ルーチン
- リダイレクトされたサブシステムの WDK のバッファリングをドライブのファイル システム、低い I/O ルーチン
- 低い I/O ルーチン WDK RDBSS
- I/O WDK RDBSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 59dce6c0cafa233bc71152aba65707dc05b8b097
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375673"
---
# <a name="low-io-routines"></a>低速 I/O ルーチン


## <span id="ddk_low_i_o_functions_if"></span><span id="DDK_LOW_I_O_FUNCTIONS_IF"></span>


最低の I/O ルーチンは、基本的な IRP を表す\_MJ\_ファイル オブジェクトで、XXX 非同期操作 (開く、閉じるには、読み取り、と書き込みなど)。 RDBSS では、ネットワークのミニ リダイレクターによって低い I/O 操作で使用されるいくつかの便利なルーチンを提供します。 RDBSS 低い I/O ルーチンを以下に示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ルーチン</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/lowio/nf-lowio-rxlowiocompletion" data-raw-source="[&lt;strong&gt;RxLowIoCompletion&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/lowio/nf-lowio-rxlowiocompletion)"><strong>RxLowIoCompletion</strong></a></p></td>
<td align="left"><p>このルーチンはルーチンは、保留中として最初に返された場合、処理が完了するととき、ネットワークのミニ リダイレクター ドライバーの低い I/O ルーチンによって呼び出される必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/lowio/nf-lowio-rxlowiogetbufferaddress" data-raw-source="[&lt;strong&gt;RxLowIoGetBufferAddress&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/lowio/nf-lowio-rxlowiogetbufferaddress)"><strong>RxLowIoGetBufferAddress</strong></a></p></td>
<td align="left"><p>このルーチンから MDL に対応するバッファーを返します、 <strong>LowIoContext</strong> RX_CONTEXT 構造体の構造体。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxmapsystembuffer" data-raw-source="[&lt;strong&gt;RxMapSystemBuffer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxmapsystembuffer)"><strong>RxMapSystemBuffer</strong></a></p></td>
<td align="left"><p>このルーチンは、I/O 要求パケット (IRP) からシステムのバッファーのアドレスを返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/rxnewmapuserbuffer" data-raw-source="[&lt;strong&gt;RxNewMapUserBuffer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/rxnewmapuserbuffer)"><strong>RxNewMapUserBuffer</strong></a></p></td>
<td align="left"><p>このルーチンは、低い I/O に使用されるユーザー バッファーのアドレスを返します。 このルーチンは、Windows XP と Windows 2000 で使用可能なだけに注意してください。</p></td>
</tr>
</tbody>
</table>

 

 

 




