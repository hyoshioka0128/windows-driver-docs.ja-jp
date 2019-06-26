---
title: WSK_CACHE_SD
description: WSK_CACHE_SD
ms.assetid: 60a4c7f9-d7e3-4378-b22b-93c69a9b8a37
ms.date: 07/18/2017
keywords:
- WSK_CACHE_SD ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: d60a21a8e85b32aecd935af1d5c573246acc8d32
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377944"
---
# <a name="wskcachesd"></a>WSK\_キャッシュ\_SD


WSK アプリケーションの使用、WSK\_キャッシュ\_SD のクライアント管理操作に渡すことができるセキュリティ記述子のキャッシュされたコピーを取得する、 [ **WskSocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_socket)、 [ **WskSocketConnect**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_socket_connect)、および[ **WskControlSocket** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_control_socket)関数。

セキュリティ記述子のキャッシュされたコピーを取得する WSK アプリケーションが呼び出す、 [ **WskControlClient** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_control_client)関数は次のパラメーター。

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
<td><p>sizeof(PSECURITY_DESCRIPTOR)</p></td>
</tr>
<tr class="odd">
<td><p><em>InputBuffer</em></p></td>
<td><p>PSECURITY_DESCRIPTOR に型指定された変数へのポインター。 この変数には、キャッシュされているキャッシュされていないセキュリティ記述子を定義する SECURITY_DESCRIPTOR 構造へのポインターが含まれています。</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSize</em></p></td>
<td><p>sizeof(PSECURITY_DESCRIPTOR)</p></td>
</tr>
<tr class="odd">
<td><p><em>OutputBuffer</em></p></td>
<td><p>PSECURITY_DESCRIPTOR に型指定された変数へのポインター。 この変数は、キャッシュされたセキュリティ記述子を表す SECURITY_DESCRIPTOR 構造体へのポインターを受け取ります。</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p><strong>NULL</strong></p></td>
</tr>
<tr class="odd">
<td><p><em>Irp</em></p></td>
<td><p><strong>NULL</strong></p></td>
</tr>
</tbody>
</table>

WSK アプリケーションを使用してセキュリティ記述子のキャッシュされたコピーを解放する必要があります、 [ **WSK\_リリース\_SD** ](wsk-release-sd.md)クライアント管理の操作、セキュリティ記述子がありません不要にします。

セキュリティの詳細については\_記述子構造体をセキュリティのリファレンス ページを参照してください\_Microsoft Windows SDK ドキュメントの記述子。

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

 

 




