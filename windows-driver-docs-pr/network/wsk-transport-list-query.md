---
title: WSK_TRANSPORT_LIST_QUERY
description: WSK_TRANSPORT_LIST_QUERY
ms.assetid: feb6aed2-fac9-4d3f-a36b-f721c737aacf
ms.date: 07/18/2017
keywords:
- WSK_TRANSPORT_LIST_QUERY ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 1d3db89c4885f1dfec1c5b43fdb1e233f229584d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379706"
---
# <a name="wsktransportlistquery"></a>WSK\_トランスポート\_一覧\_クエリ


WSK アプリケーションの使用、WSK\_トランスポート\_一覧\_新しいソケットを作成するときに指定できる利用可能なネットワーク トランスポートの一覧を取得するクエリのクライアント管理操作。

使用可能なネットワーク トランスポートの一覧を取得する WSK アプリケーションが呼び出す、 [ **WskControlClient** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_control_client)関数は次のパラメーター。

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
<td><p><em>ControlCode</em></p></td>
<td><p>WSK_TRANSPORT_LIST_QUERY</p></td>
</tr>
<tr class="even">
<td><p><em>InputSize</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="odd">
<td><p><em>InputBuffer</em></p></td>
<td><p><strong>NULL</strong></p></td>
</tr>
<tr class="even">
<td><p><em>OutputSize</em></p></td>
<td><p>指す構造体の配列のバイト単位で、サイズ、 <em>OutputBuffer</em>パラメーター</p></td>
</tr>
<tr class="odd">
<td><p><em>OutputBuffer</em></p></td>
<td><p>配列へのポインター <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/ns-wsk-_wsk_transport" data-raw-source="[&lt;strong&gt;WSK_TRANSPORT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/ns-wsk-_wsk_transport)"> <strong>WSK_TRANSPORT</strong> </a>構造体を使用可能なネットワーク トランスポートの一覧を受け取る</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p>指す構造体の配列にコピーされたデータのバイト数を受け取る SIZE_T に型指定された変数へのポインター、 <em>OutputBuffer</em>パラメーター</p></td>
</tr>
<tr class="odd">
<td><p><em>Irp</em></p></td>
<td><p><strong>NULL</strong></p></td>
</tr>
</tbody>
</table>

WSK アプリケーションに 0 を指定できます、 *OutputSize*パラメーターと**NULL**で、 *OutputBuffer*パラメーターの配列のサイズを決定する[ **WSK\_トランスポート**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/ns-wsk-_wsk_transport)構造、使用可能なネットワーク トランスポートの完全な一覧を格納するために必要なバイト数。 このような状況への呼び出し、 [ **WskControlClient** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_control_client)ステータスを返します\_バッファー\_オーバーフロー、および変数を指している*OutputSizeReturned*パラメーターに必要なバッファー サイズが含まれています。 アプリケーションは、バッファーが使用可能なネットワーク トランスポートの完全な一覧を格納するのに十分な大きさを呼び出すことができますを割り当てることができますし、 **WskControlClient**関数に示すようなパラメーターを指定する、第 2 回、前の表。

*Irp*パラメーターである必要があります**NULL**このクライアントのコントロールの操作。

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

 

 




