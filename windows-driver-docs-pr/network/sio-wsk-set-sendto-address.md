---
title: SIO_WSK_SET_SENDTO_ADDRESS
description: SIO_WSK_SET_SENDTO_ADDRESS
ms.assetid: 2dd149d2-adc6-4e03-92de-ed76aa048886
ms.date: 07/18/2017
keywords:
- SIO_WSK_SET_SENDTO_ADDRESS ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: 58bda46c3aab4a43ba2c58ac6329119a0055414f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841894"
---
# <a name="sio_wsk_set_sendto_address"></a>SIO\_WSK\_設定\_SENDTO\_アドレス


SIO\_WSK\_\_SENDTO\_アドレスソケット i/o 制御操作を設定すると、WSK アプリケーションでデータグラムソケットの固定送信先トランスポートアドレスを指定できます。 このソケット i/o 制御操作は、データグラムソケットにのみ適用されます。

WSK アプリケーションで、データグラムソケットに固定の送信先トランスポートアドレスを設定すると、ソケットを介して送信されるすべてのデータグラムが固定送信先トランスポートアドレスに送信されます。 ただし、ソケットで受信したデータグラムは、任意のトランスポートアドレスから受け入れられます。

WSK アプリケーションは、 [**Wsksendto**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_send_to)関数を呼び出すときに、 *remoteaddress*パラメーターで別のリモートトランスポートアドレスを指定することによって、ソケットでデータグラムを送信するときに、固定された宛先トランスポートアドレスをオーバーライドできます。 この場合、データグラムは、固定された送信先トランスポートアドレスではなく、代替のリモートトランスポートアドレスに送信されます。

WSK アプリケーションで、このソケット i/o 制御操作を使用して固定の宛先トランスポートアドレスを指定する場合は、データグラムソケットがローカルトランスポートアドレスにバインドされた後で、この処理を行う必要があります。

データグラムソケットの固定送信先トランスポートアドレスを設定するために、WSK アプリケーションは次のパラメーターを使用して[**Wskcontrolsocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_socket)関数を呼び出します。

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
<td><p>SIO_WSK_SET_SENDTO_ADDRESS</p></td>
</tr>
<tr class="odd">
<td><p><em>平準</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><em>InputSize</em></p></td>
<td><p><em>InputBuffer</em>パラメーターによって示される SOCKADDR 構造体のサイズ。</p></td>
</tr>
<tr class="odd">
<td><p><em>InputBuffer</em></p></td>
<td><p>データグラムソケットの固定送信先トランスポートアドレスを指定する構造体へのポインター。 ポインターは、WSK アプリケーションがデータグラムソケットの作成時に指定したアドレスファミリに対応する、特定の SOCKADDR structure 型へのポインターである必要があります。</p></td>
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


データグラムソケットの固定送信先トランスポートアドレスをクリアするために、WSK アプリケーションは次のパラメーターを使用して**Wskcontrolsocket**関数を呼び出します。

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
<td><p>SIO_WSK_SET_SENDTO_ADDRESS</p></td>
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



WSK アプリケーションは、 **Wskcontrolsocket**関数を呼び出してデータグラムソケットの固定送信先トランスポートアドレスを設定またはクリアするときに、IRP へのポインターを指定する必要があります。

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

 

 




