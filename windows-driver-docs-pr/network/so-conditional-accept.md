---
title: SO_CONDITIONAL_ACCEPT
description: SO_CONDITIONAL_ACCEPT
ms.assetid: 8aaaa08b-b239-4648-8c4f-8db2efbda551
ms.date: 08/08/2017
keywords: -Windows Vista 以降の SO_CONDITIONAL_ACCEPT ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: e25f085704b9d48e99beed0c62a6bc3934a437ac
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841888"
---
# <a name="so_conditional_accept"></a>\_条件付き\_受け入れ


SO\_条件付き\_ACCEPT socket オプションの状態によって、リスニングソケットで条件付き受け入れモードが有効かどうかが決まります。 このソケットオプションは、リッスンしているソケットにのみ適用されます。

WSK アプリケーションがこのソケットオプションを設定する場合は、リッスンしているソケットがローカルトランスポートアドレスにバインドされる前に実行する必要があります。

このソケットオプションの状態を設定するために、WSK アプリケーションは次のパラメーターを使用して[**Wskcontrolsocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_socket)関数を呼び出します。

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
<td><p><strong>WskSetOption</strong></p></td>
</tr>
<tr class="even">
<td><p><em>ControlCode</em></p></td>
<td><p>SO_CONDITIONAL_ACCEPT</p></td>
</tr>
<tr class="odd">
<td><p><em>平準</em></p></td>
<td><p>SOL_SOCKET</p></td>
</tr>
<tr class="even">
<td><p><em>InputSize</em></p></td>
<td><p>sizeof (ULONG)</p></td>
</tr>
<tr class="odd">
<td><p><em>InputBuffer</em></p></td>
<td><p>Socket オプションの新しい状態の値を格納する、ULONG 型の変数へのポインター。</p>
<p>0: 条件付き受け入れモードを無効にします。</p>
<p>1: 条件付き受け入れモードを有効にします。</p></td>
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


WSK アプリケーションは、このソケットオプションの状態を取得するために、次のパラメーターを使用して**Wskcontrolsocket**関数を呼び出します。

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
<td><p><strong>WskGetOption</strong></p></td>
</tr>
<tr class="even">
<td><p><em>ControlCode</em></p></td>
<td><p>SO_CONDITIONAL_ACCEPT</p></td>
</tr>
<tr class="odd">
<td><p><em>平準</em></p></td>
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
<td><p>sizeof (ULONG)</p></td>
</tr>
<tr class="odd">
<td><p><em>OutputBuffer</em></p></td>
<td><p>ソケットオプションの状態の値を受け取る、ULONG 型の変数へのポインター。</p>
<p>0: 条件付き受け入れモードは無効です。</p>
<p>1: 条件付き受け入れモードが有効になっています</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p>NULL</p></td>
</tr>
</tbody>
</table>



WSK アプリケーションは、 **Wskcontrolsocket**関数を呼び出してその状態を設定または取得するときに、IRP へのポインターを指定する必要があります。これにより、\_の条件付き\_ACCEPT socket オプションを設定または取得します。

このソケットオプションの既定の状態は、条件付き受け入れモードが無効になっていることを示します。

一部のトランスポートプロトコルでは、リスニングソケットで条件付き受け入れモードがサポートされていない場合があります。

着信接続を条件付きで受け入れる方法の詳細については、「[受信接続のリッスンと受け入れ](https://docs.microsoft.com/windows-hardware/drivers/network/listening-for-and-accepting-incoming-connections)」を参照してください。

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

 

 




