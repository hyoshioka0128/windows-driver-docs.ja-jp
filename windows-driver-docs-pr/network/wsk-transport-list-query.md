---
title: WSK_TRANSPORT_LIST_QUERY
description: WSK_TRANSPORT_LIST_QUERY
ms.assetid: feb6aed2-fac9-4d3f-a36b-f721c737aacf
ms.date: 07/18/2017
keywords:
- WSK_TRANSPORT_LIST_QUERY ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: 29817f14f61ee142e1f8a7ae249436a1d81e5f6e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844415"
---
# <a name="wsk_transport_list_query"></a>WSK\_TRANSPORT\_LIST\_クエリ


WSK アプリケーションは、WSK\_TRANSPORT\_LIST を使用してクライアント制御操作を照会\_、新しいソケットの作成時に指定できる使用可能なネットワークトランスポートの一覧を取得します。

使用可能なネットワークトランスポートの一覧を取得するために、WSK アプリケーションは、次のパラメーターを使用して[**Wskcontrolclient**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_client)関数を呼び出します。

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
<td><p><strong>空白</strong></p></td>
</tr>
<tr class="even">
<td><p><em>OutputSize</em></p></td>
<td><p><em>Outputbuffer</em>パラメーターによって示される構造体の配列のサイズ (バイト単位)。</p></td>
</tr>
<tr class="odd">
<td><p><em>OutputBuffer</em></p></td>
<td><p>使用可能なネットワークトランスポートの一覧を受け取る<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_transport" data-raw-source="[&lt;strong&gt;WSK_TRANSPORT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_transport)"><strong>WSK_TRANSPORT</strong></a>構造体の配列へのポインター</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p><em>Outputbuffer</em>パラメーターによって示される構造体の配列にコピーされるデータのバイト数を受け取る SIZE_T 型の変数へのポインター。</p></td>
</tr>
<tr class="odd">
<td><p><em>Irp</em></p></td>
<td><p><strong>空白</strong></p></td>
</tr>
</tbody>
</table>

WSK アプリケーションでは、 *Outputsize*パラメーターに0を指定し、 *Outputsize*パラメーターに**NULL**を指定することができます。これにより、 [**wsk\_トランスポート**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_transport)構造体の配列のサイズ (バイト単位) を指定できます。利用可能なネットワークトランスポートの完全な一覧。 このような状況では、 [**Wskcontrolclient**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_client)関数の呼び出しによって STATUS\_BUFFER\_OVERFLOW が返され、 *Outputsizereturned*パラメーターによって示される変数に必要なバッファーサイズが含まれています。 アプリケーションは、使用可能なネットワークトランスポートの完全な一覧を格納するのに十分な大きさのバッファーを割り当てることができます。また、前の表に示したパラメーターを指定して、 **Wskcontrolclient**関数を2回目に呼び出すことができます。

このクライアントコントロール操作では、 *Irp*パラメーターは**NULL**である必要があります。

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
<td><p>Windows Vista 以降のバージョンの Windows オペレーティングシステムで使用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wsk .h (Wsk .h を含む)</td>
</tr>
</tbody>
</table>

 

 




