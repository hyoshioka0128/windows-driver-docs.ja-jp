---
title: SIO_WSK_SET_REMOTE_ADDRESS
description: SIO_WSK_SET_REMOTE_ADDRESS
ms.assetid: 1db11c7a-c9ce-428e-b4da-4a49904a9e4c
ms.date: 07/18/2017
keywords:
- SIO_WSK_SET_REMOTE_ADDRESS ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: 52cffcd9e14f77b709620625e3d52070ec7195a2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841896"
---
# <a name="sio_wsk_set_remote_address"></a>SIO\_WSK\_設定\_リモート\_アドレス


SIO\_WSK\_\_リモート\_アドレスソケット i/o 制御操作を設定すると、WSK アプリケーションでデータグラムソケットの固定リモートトランスポートアドレスを指定できます。 このソケット i/o 制御操作は、データグラムソケットにのみ適用されます。

WSK アプリケーションで、データグラムソケットに対して固定のリモートトランスポートアドレスを設定すると、ソケットを介して送信されるすべてのデータグラムが固定のリモートトランスポートアドレスに送信され、固定のリモートトランスポートアドレスから受信されたデータグラムのみが受け入れられます。

WSK アプリケーションは、 [**Wsksendto**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_send_to)関数を呼び出すときに、 *remoteaddress*パラメーターで別のリモートトランスポートアドレスを指定することによって、ソケットでデータグラムを送信するときに、固定されたリモートトランスポートアドレスをオーバーライドできます。 この場合、データグラムは、固定されたリモートトランスポートアドレスではなく、代替のリモートトランスポートアドレスに送信されます。 ただし、代替のリモートトランスポートアドレスから返信された応答は受け入れられません。

WSK アプリケーションで、このソケット i/o 制御操作を使用して固定のリモートトランスポートアドレスを指定する場合は、データグラムソケットがローカルトランスポートアドレスにバインドされた後で、この処理を行う必要があります。

データグラムソケットの固定リモートトランスポートアドレスを設定するために、WSK アプリケーションは、次のパラメーターを使用して[**Wskcontrolsocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_socket)関数を呼び出します。

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
<td><p>SIO_WSK_SET_REMOTE_ADDRESS</p></td>
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
<td><p>データグラムソケットの固定リモートトランスポートアドレスを指定する構造体へのポインター。 ポインターは、WSK アプリケーションがデータグラムソケットの作成時に指定したアドレスファミリに対応する、特定の SOCKADDR structure 型へのポインターである必要があります。</p></td>
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


データグラムソケットの固定リモートトランスポートアドレスをクリアするために、WSK アプリケーションは次のパラメーターを使用して**Wskcontrolsocket**関数を呼び出します。

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
<td><p>SIO_WSK_SET_REMOTE_ADDRESS</p></td>
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


WSK アプリケーションは、 **Wskcontrolsocket**関数を呼び出して、データグラムソケットの固定リモートトランスポートアドレスを設定またはクリアするときに、IRP へのポインターを指定する必要があります。

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
