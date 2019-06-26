---
title: SIO_WSK_QUERY_INSPECT_ID
description: SIO_WSK_QUERY_INSPECT_ID
ms.assetid: 6fc3e5ea-61df-47fc-8f79-f9ae272b3544
ms.date: 07/18/2017
keywords:
- SIO_WSK_QUERY_INSPECT_ID ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 599590cf92c090f9b83945977a71ccb4c96dc3fb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379139"
---
# <a name="siowskqueryinspectid"></a>SIO\_WSK\_クエリ\_検査\_ID


SIO\_WSK\_クエリ\_検査\_ID ソケット I/O 制御操作が正常に受け入れられた接続指向のソケットの検査識別データを照会する WSK アプリケーションは、条件付きのあるリッスン ソケットの受け入れモードを有効にします。 このソケット I/O 制御操作を有効になっているモードをそのまま使用条件を持つリッスン ソケットの受け入れられた接続指向のソケットだけに適用されます。

WSK アプリケーションを呼び出す接続指向のソケットの検査の id データを照会、 [ **WskControlSocket** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_control_socket)関数は次のパラメーター。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>パラメーター</th>
<th>Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>RequestType</em></p></td>
<td><p><strong>WskIoctl</strong></p></td>
</tr>
<tr class="even">
<td><p><em>ControlCode</em></p></td>
<td><p>SIO_WSK_QUERY_INSPECT_ID</p></td>
</tr>
<tr class="odd">
<td><p><em>Level</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><em>InputSize</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="odd">
<td><p><em>InputBuffer</em></p></td>
<td><p>NULL</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSize</em></p></td>
<td><p>sizeof(WSK_INSPECT_ID)</p></td>
</tr>
<tr class="odd">
<td><p><em>OutputBuffer</em></p></td>
<td><p>検査の識別データを受信する WSK_INSPECT_ID 構造体へのポインター</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p>指すバッファーにコピーされたデータのバイト数を受け取る ULONG に型指定された変数へのポインター、 <em>OutputBuffer</em>パラメーター。</p></td>
</tr>
<tr class="odd">
<td><p><em>Irp</em></p></td>
<td><p>NULL</p></td>
</tr>
</tbody>
</table>

WSK アプリケーションから呼び出す場合、 **WskControlSocket**関数を持つ条件付きリッスン ソケットの受け入れられた接続指向のソケット以外の任意のソケットの検査識別データを照会するには、モードがそのまま使用有効になって、 **WskControlSocket**ステータスを返します\_無効な\_デバイス\_要求。

条件付きで接続の受け入れの詳細については、次を参照してください。[リッスン中の接続と着信接続を受け入れる](https://docs.microsoft.com/windows-hardware/drivers/network/listening-for-and-accepting-incoming-connections)します。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>Windows Vista および Windows オペレーティング システムの以降のバージョンで使用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wsk.h (Wsk.h を含む)</td>
</tr>
</tbody>
</table>

 

 




