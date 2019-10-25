---
title: I/o ルーチンが不足しています
description: I/o ルーチンが不足しています
ms.assetid: 5317917d-9abc-43f9-ab4a-f070e491c816
keywords:
- RDBSS WDK ファイルシステム、低 i/o ルーチン
- リダイレクトされたドライブバッファリングサブシステム WDK ファイルシステム、低 i/o ルーチン
- 低 i/o ルーチン WDK RDBSS
- I/O WDK RDBSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b4e06309993b35de48aa4cbf807af79193e2543c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841134"
---
# <a name="low-io-routines"></a>I/o ルーチンが不足しています


## <span id="ddk_low_i_o_functions_if"></span><span id="DDK_LOW_I_O_FUNCTIONS_IF"></span>


低 i/o ルーチンは、ファイルオブジェクトに対する基本的な IRP\_MJ\_XXX 非同期操作 (オープン、閉じる、読み取り、書き込みなど) を表します。 RDBSS には、ネットワークミニリダイレクターによる低 i/o 操作で使用される便利なルーチンがいくつか用意されています。 RDBSS 低 i/o ルーチンには、次のものが含まれます。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/lowio/nf-lowio-rxlowiocompletion" data-raw-source="[&lt;strong&gt;RxLowIoCompletion&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/lowio/nf-lowio-rxlowiocompletion)"><strong>RxLowIoCompletion</strong></a></p></td>
<td align="left"><p>このルーチンは、ルーチンが最初に pending として返された場合に、処理が完了すると、ネットワークミニリダイレクタードライバーの低 i/o ルーチンによって呼び出される必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/lowio/nf-lowio-rxlowiogetbufferaddress" data-raw-source="[&lt;strong&gt;RxLowIoGetBufferAddress&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/lowio/nf-lowio-rxlowiogetbufferaddress)"><strong>RxLowIoGetBufferAddress</strong></a></p></td>
<td align="left"><p>このルーチンは、RX_CONTEXT 構造体の<strong>Lowiocontext</strong>構造から、MDL に対応するバッファーを返します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxmapsystembuffer" data-raw-source="[&lt;strong&gt;RxMapSystemBuffer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxmapsystembuffer)"><strong>RxMapSystemBuffer</strong></a></p></td>
<td align="left"><p>このルーチンは、i/o 要求パケット (IRP) からのシステムバッファーアドレスを返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/rxnewmapuserbuffer" data-raw-source="[&lt;strong&gt;RxNewMapUserBuffer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/rxnewmapuserbuffer)"><strong>RxNewMapUserBuffer</strong></a></p></td>
<td align="left"><p>このルーチンは、低 i/o に使用されたユーザーバッファーのアドレスを返します。 このルーチンは、Windows XP と Windows 2000 でのみ使用できます。</p></td>
</tr>
</tbody>
</table>

 

 

 




