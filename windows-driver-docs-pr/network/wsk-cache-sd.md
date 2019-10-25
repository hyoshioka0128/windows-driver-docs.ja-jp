---
title: WSK_CACHE_SD
description: WSK_CACHE_SD
ms.assetid: 60a4c7f9-d7e3-4378-b22b-93c69a9b8a37
ms.date: 07/18/2017
keywords:
- WSK_CACHE_SD ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: 123e78289023c81b962d188c385237d68f736aee
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842326"
---
# <a name="wsk_cache_sd"></a>WSK\_キャッシュ\_SD


WSK アプリケーションは WSK\_CACHE\_SD クライアントコントロール操作を使用して、 [**Wsksocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_socket)、 [**wsksocketconnect**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_socket_connect)、および[**wskcontrolsocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_socket)関数に渡すことができるセキュリティ記述子のキャッシュされたコピーを取得します。

セキュリティ記述子のキャッシュされたコピーを取得するために、WSK アプリケーションは、次のパラメーターを使用して[**Wskcontrolclient**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_client)関数を呼び出します。

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
<td><p>WSK_CACHE_SD</p></td>
</tr>
<tr class="even">
<td><p><em>InputSize</em></p></td>
<td><p>sizeof (PSECURITY_DESCRIPTOR)</p></td>
</tr>
<tr class="odd">
<td><p><em>InputBuffer</em></p></td>
<td><p>PSECURITY_DESCRIPTOR で型指定された変数へのポインター。 この変数には、キャッシュされるキャッシュされていないセキュリティ記述子を定義する SECURITY_DESCRIPTOR 構造体へのポインターが含まれています。</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSize</em></p></td>
<td><p>sizeof (PSECURITY_DESCRIPTOR)</p></td>
</tr>
<tr class="odd">
<td><p><em>OutputBuffer</em></p></td>
<td><p>PSECURITY_DESCRIPTOR で型指定された変数へのポインター。 この変数は、キャッシュされたセキュリティ記述子を記述する SECURITY_DESCRIPTOR 構造体へのポインターを受け取ります。</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p><strong>空白</strong></p></td>
</tr>
<tr class="odd">
<td><p><em>Irp</em></p></td>
<td><p><strong>空白</strong></p></td>
</tr>
</tbody>
</table>

WSK アプリケーションは、セキュリティ記述子が不要になったときに[**wsk\_release\_SD**](wsk-release-sd.md)クライアントコントロール操作を使用して、セキュリティ記述子のキャッシュされたコピーを解放する必要があります。

セキュリティ\_記述子の構造の詳細については、Microsoft Windows SDK のドキュメントのセキュリティ\_記述子のリファレンスページを参照してください。

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

 

 




