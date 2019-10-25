---
title: SIO_ADDRESS_LIST_CHANGE
description: SIO_ADDRESS_LIST_CHANGE
ms.assetid: d451208d-c850-4f2f-9ee0-d34139454ed4
ms.date: 08/08/2017
keywords: -Windows Vista 以降の SIO_ADDRESS_LIST_CHANGE ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 92425311277c269c3e14008fc3a28adc7cca202d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841916"
---
# <a name="sio_address_list_change"></a>SIO\_アドレス\_リスト\_変更


ソケットのアドレスファミリのローカルトランスポートアドレスの一覧が変更された場合、SIO\_ADDRESS\_LIST\_CHANGE socket i/o control 操作は WSK アプリケーションに通知します。 このソケット i/o 制御操作は、すべてのソケットの種類に適用されます。

ソケットのアドレスファミリのローカルトランスポートアドレスの一覧が変更されたときに通知を受けるには、WSK アプリケーションは次のパラメーターを使用して[**Wskcontrolsocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_socket)関数を呼び出します。

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
<td><p>SIO_ADDRESS_LIST_CHANGE</p></td>
</tr>
<tr class="odd">
<td><p><em>平準</em></p></td>
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
<td><p>0</p></td>
</tr>
<tr class="odd">
<td><p><em>OutputBuffer</em></p></td>
<td><p>NULL</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p>NULL</p></td>
</tr>
</tbody>
</table>

WSK アプリケーションは、 **Wskcontrolsocket**関数を呼び出して、ソケットのアドレスファミリのローカルトランスポートアドレスの一覧が変更されたことを通知するときに、IRP へのポインターを指定する必要があります。 WSK サブシステムは、IRP をキューに置いて、STATUS\_PENDING を返します。 ソケットのアドレスファミリのローカルトランスポートアドレスの一覧に変更が加えられると、WSK サブシステムが IRP を完了します。 IRP の完了ルーチンが呼び出されると、WSK アプリケーションは、 [**SIO\_ADDRESS\_LIST\_query**](sio-address-list-query.md) socket i/o control 操作を使用して、ソケットのアドレスファミリのローカルトランスポートアドレスの新しいリストを照会できます。

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
<td>Ws2def (Wsk .h を含む)</td>
</tr>
</tbody>
</table>

 

 




