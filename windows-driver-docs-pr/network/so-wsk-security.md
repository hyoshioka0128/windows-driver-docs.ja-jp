---
title: SO_WSK_SECURITY
description: SO_WSK_SECURITY
ms.assetid: 169680ba-6486-48fe-89d7-dcd4e5930605
ms.date: 07/18/2017
keywords:
- SO_WSK_SECURITY ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: ff1f423294f6c296c6b984b203640c860fdcb889
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841876"
---
# <a name="so_wsk_security"></a>\_WSK\_セキュリティ


\_WSK\_セキュリティソケットオプションを使用すると、WSK アプリケーションでソケットにセキュリティ記述子を適用したり、ソケットからソケットのセキュリティ記述子のキャッシュされたコピーを取得したりできます。 セキュリティ記述子は、ソケットがバインドされるローカルトランスポートアドレスの共有を制御します。

このソケットオプションは、リッスンしているソケット、データグラムソケット、および接続指向のソケットにのみ適用されます。

WSK アプリケーションがこのソケットオプションを使用してソケットにセキュリティ記述子を適用する場合は、ソケットがローカルトランスポートアドレスにバインドされる前に、この操作を行う必要があります。

セキュリティ記述子をソケットに適用するために、WSK アプリケーションは次のパラメーターを使用して[**Wskcontrolsocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_socket)関数を呼び出します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>パラメーター</th>
<th>値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>RequestType</em></p></td>
<td><p><strong>WskSetOption</strong></p></td>
</tr>
<tr class="even">
<td><p><em>ControlCode</em></p></td>
<td><p>SO_WSK_SECURITY</p></td>
</tr>
<tr class="odd">
<td><p><em>Level</em></p></td>
<td><p>SOL_SOCKET</p></td>
</tr>
<tr class="even">
<td><p><em>InputSize</em></p></td>
<td><p>sizeof (PSECURITY_DESCRIPTOR)</p></td>
</tr>
<tr class="odd">
<td><p><em>InputBuffer</em></p></td>
<td><p>PSECURITY_DESCRIPTOR で型指定された変数へのポインター。 この変数には、 <a href="wsk-cache-sd.md" data-raw-source="[&lt;strong&gt;WSK_CACHE_SD&lt;/strong&gt;](wsk-cache-sd.md)"><strong>WSK_CACHE_SD</strong></a>制御コードで<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_client" data-raw-source="[&lt;strong&gt;WskControlClient&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_client)"><strong>Wskcontrolclient</strong></a>関数を呼び出すことによって取得されたセキュリティ記述子のキャッシュされたコピーへのポインターが含まれている必要があります。</p></td>
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

WSK アプリケーションは、 **Wskcontrolsocket**関数を呼び出してソケットにセキュリティ記述子を適用するときに、IRP へのポインターを指定する必要があります。

WSK アプリケーションがこのソケットオプションを使用してセキュリティ記述子をソケットに適用する場合、新しいセキュリティ記述子は、以前にソケットに適用されていたセキュリティ記述子を置き換えます。

WSK アプリケーションは、IRP が完了するまで、セキュリティ記述子のキャッシュされたコピーを解放しないでください。

WSK アプリケーションは、最初に作成されたときに、セキュリティ記述子をソケットに適用することもできます。これを行うには、セキュリティ記述子が[**wsksocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_socket) [**を呼び出すときに、SecurityDescriptor パラメーターにキャッシュされたコピーへのポインターを指定します。WskSocketConnect**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_socket_connect)関数。

WSK アプリケーションがセキュリティ記述子をソケットに適用しない場合、WSK サブシステムでは、ローカルトランスポートアドレスの共有を許可しない既定のセキュリティ記述子が使用されます。

ソケットからソケットのセキュリティ記述子のキャッシュされたコピーを取得するために、WSK アプリケーションは次のパラメーターを使用して[**Wskcontrolsocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_socket)関数を呼び出します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>パラメーター</th>
<th>値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>RequestType</em></p></td>
<td><p><strong>WskGetOption</strong></p></td>
</tr>
<tr class="even">
<td><p><em>ControlCode</em></p></td>
<td><p>SO_WSK_SECURITY</p></td>
</tr>
<tr class="odd">
<td><p><em>Level</em></p></td>
<td><p>SOL_SOCKET</p></td>
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
<td><p>sizeof (PSECURITY_DESCRIPTOR)</p></td>
</tr>
<tr class="odd">
<td><p><em>OutputBuffer</em></p></td>
<td><p>PSECURITY_DESCRIPTOR で型指定された変数へのポインター。 この変数は、ソケットのセキュリティ記述子のキャッシュされたコピーへのポインターを受け取ります。</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p>NULL</p></td>
</tr>
</tbody>
</table>

WSK アプリケーションは、 **Wskcontrolsocket**関数を呼び出してソケットからソケットのセキュリティ記述子のキャッシュされたコピーを取得するときに、IRP へのポインターを指定する必要があります。

WSK アプリケーションは、 [**wsk\_RELEASE\_SD**](wsk-release-sd.md)制御コードを使用して[**Wskcontrolclient**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_client)関数を呼び出して、不要になったセキュリティ記述子のキャッシュされたコピーを解放する必要があります。

セキュリティ\_記述子の構造の詳細については、Microsoft Windows SDK のドキュメントのセキュリティ\_記述子のリファレンスページを参照してください。

<a name="requirements"></a>前提条件
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
<td><p>ヘッダー</p></td>
<td>Wsk .h (Wsk .h を含む)</td>
</tr>
</tbody>
</table>

 

 




