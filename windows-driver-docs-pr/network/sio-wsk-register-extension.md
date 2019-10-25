---
title: SIO_WSK_REGISTER_EXTENSION
description: SIO_WSK_REGISTER_EXTENSION
ms.assetid: e7fd6d68-85e8-4c5f-b67f-2193d200130d
ms.date: 07/18/2017
keywords:
- SIO_WSK_REGISTER_EXTENSION ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: cbb653845b59fc46d248ef15f73c0ec2543280ed
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841898"
---
# <a name="sio_wsk_register_extension"></a>SIO\_WSK\_レジスタ\_拡張機能


SIO\_WSK\_REGISTER\_EXTENSION socket i/o control 操作を使用すると、wsk サブシステムでサポートされている拡張インターフェイスに WSK アプリケーションを登録できます。 このソケット i/o 制御操作は、すべてのソケットの種類に適用されます。

拡張インターフェイスを登録するために、WSK アプリケーションは次のパラメーターを使用して[**Wskcontrolsocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_socket)関数を呼び出します。

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
<td><p>SIO_WSK_REGISTER_EXTENSION</p></td>
</tr>
<tr class="odd">
<td><p><em>平準</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><em>InputSize</em></p></td>
<td><p>sizeof (WSK_EXTENSION_CONTROL_IN)</p></td>
</tr>
<tr class="odd">
<td><p><em>InputBuffer</em></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_extension_control_in" data-raw-source="[&lt;strong&gt;WSK_EXTENSION_CONTROL_IN&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_extension_control_in)"><strong>WSK_EXTENSION_CONTROL_IN</strong></a>構造体へのポインター。 この構造体には、拡張インターフェイスの<a href="https://docs.microsoft.com/windows-hardware/drivers/network/network-programming-interface" data-raw-source="[Network Programming Interface (NPI)](https://docs.microsoft.com/windows-hardware/drivers/network/network-programming-interface)">ネットワークプログラミングインターフェイス (NPI)</a>識別子へのポインターと、ディスパッチテーブルへのポインター、および wsk アプリケーションの拡張インターフェイスの実装のコンテキストへのポインターが含まれています。</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSize</em></p></td>
<td><p>sizeof (WSK_EXTENSION_CONTROL_OUT)</p></td>
</tr>
<tr class="odd">
<td><p><em>OutputBuffer</em></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_extension_control_out" data-raw-source="[&lt;strong&gt;WSK_EXTENSION_CONTROL_OUT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_extension_control_out)"><strong>WSK_EXTENSION_CONTROL_OUT</strong></a>構造体へのポインター。 この構造体は、ディスパッチテーブルへのポインターと、WSK サブシステムの拡張インターフェイスの実装のコンテキストへのポインターを受け取ります。</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p>NULL</p></td>
</tr>
</tbody>
</table>


WSK アプリケーションは、 **Wskcontrolsocket**関数を呼び出して拡張インターフェイスを登録するときに、IRP へのポインターを指定しません。

ディスパッチテーブル構造の内容は、拡張インターフェイス固有の構造体です。

拡張インターフェイスの登録の詳細については、「[拡張インターフェイスの登録](https://docs.microsoft.com/windows-hardware/drivers/network/registering-an-extension-interface)」を参照してください。

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

 

 




