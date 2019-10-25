---
title: SIO_QUERY_WFP_CONNECTION_REDIRECT_CONTEXT 制御コード
description: SIO_QUERY_WFP_CONNECTION_REDIRECT_CONTEXT socket i/o control 操作を使用すると、Winsock クライアントは、リダイレクトされた接続のリダイレクトレコードのリダイレクトコンテキストを取得できます。
ms.assetid: D23971FC-D75F-4C39-BE6A-F0E17F7C1804
ms.date: 08/08/2017
keywords: -SIO_QUERY_WFP_CONNECTION_REDIRECT_CONTEXT Windows Vista 以降のコードネットワークドライバーの制御
ms.localizationpriority: medium
ms.openlocfilehash: 838630273811f8130d00702af44e153e00acde69
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841908"
---
# <a name="sio_query_wfp_connection_redirect_context-control-code"></a>SIO\_クエリ\_WFP\_接続\_リダイレクト\_コンテキスト制御コード


**SIO\_クエリ\_WFP\_接続\_リダイレクト\_コンテキスト**ソケット i/o 制御操作により、Winsock クライアントは、リダイレクトされた接続のリダイレクトレコードのリダイレクトコンテキストを取得できます。

WFP リダイレクトレコードは、リダイレクトされた接続と元の接続が論理的に関連するように、WFP が送信プロキシ接続に対して設定する必要がある不透明なデータのバッファーです。

**注**  [**SIO\_クエリ\_WFP\_接続\_リダイレクト\_レコード**](sio-query-wfp-connection-redirect-records.md)クエリは、接続が fwps\_レイヤーでリダイレクトされた場合にのみ使用でき\_**ALE\_接続 @no__t13_ リダイレクト\_V4**または**fwps\_レイヤー\_ALE\_接続\_V6**レイヤーを WFP クライアントにリダイレクトします。

 

リダイレクトの詳細については、「 [Using Bind Or Connect リダイレクション](https://docs.microsoft.com/windows-hardware/drivers/network/using-bind-or-connect-redirection)」を参照してください。

リダイレクトレコードのリダイレクトコンテキストに対してクエリを実行するために、Winsock クライアントは、次のパラメーターを使用して[**Wskcontrolsocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_socket)関数を呼び出します。

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
<td><p><strong>SIO_QUERY_WFP_CONNECTION_REDIRECT_CONTEXT</strong></p></td>
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
<td><p><em>Outputbuffer</em>パラメーターによって示されるバッファーのサイズ (バイト単位)。</p></td>
</tr>
<tr class="odd">
<td><p><em>OutputBuffer</em></p></td>
<td><p>受け入れられた TCP 接続のリダイレクトレコードのリダイレクトコンテキストを受け取るバッファーへのポインター。 バッファーのサイズは、 <em>Outputsize</em>パラメーターで指定します。</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p><em>Outputbuffer</em>パラメーターによって示されるバッファーにコピーされるデータのバイト数を受け取る、 <strong>ULONG</strong>型の変数へのポインター。</p></td>
</tr>
<tr class="odd">
<td><p>Irp</p></td>
<td><p>IRP へのポインター。</p></td>
</tr>
</tbody>
</table>

 

呼び出し元は、次のいずれかの方法でこのクエリを実行できます。

-   出力*バッファー*は、サイズが約 1 KB の大きなバッファーに設定できます。 出力バッファーのサイズが十分でない場合は、 [**Wskcontrolsocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_socket)は**状態\_バッファー\_** を返します。\_小さ、 *outputsizereturned*にはバッファーに必要なサイズが含まれます。 その後、より大きなバッファーを割り当てることができます。また、 **SIO\_クエリ\_WFP\_\_接続** **を使用し**てもう一度呼び出されます。これにより、\_コンテキスト要求と*outputbuffer*が大きなバッファーに設定されます。
-   または、 *Outputsize*パラメーターを0に設定し、 *OUTPUTSIZE*を NULL に設定して、 [**wskcontrolsocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_socket)を呼び出すこともできます。 完了時に、 **Wskcontrolsocket**関数は*Outputsizereturned*パラメーターの出力バッファーサイズ (バイト単位) を取得します。 適切にサイズ設定されたバッファーを割り当てることができます。また、 **SIO\_クエリ\_WFP\_\_接続** **を使用し**て再び呼び出される場合は、\_コンテキスト要求と*outputbuffer*がバッファーに設定されます.

**注**  [ **\_クエリ\_WFP\_接続\_リダイレクト\_コンテキスト (SDK)** ](https://docs.microsoft.com/previous-versions/windows/desktop/legacy/hh859712(v=vs.85))を使用して、ユーザーモードアプリケーションでこのクエリを実行することもできます。

 

この種類の要求の場合、Winsock クライアントは、IRP へのポインターとその完了ルーチンへのポインターを指定する必要があります。 IRP は、上位のドライバーによってクライアントに渡すことができます。または、クライアントが IRP の割り当てを選択できます。 完了ルーチンを指定するには、クライアントは[**Iosetcompletion ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine)を呼び出す必要があります。 詳細については、「 [Winsock カーネル関数での irp の使用](https://docs.microsoft.com/windows-hardware/drivers/network/using-irps-with-winsock-kernel-functions)」を参照してください。

WSK サブシステムが IRP を完了するまで、Winsock クライアントは割り当てられたバッファーを解放しないようにする必要があります。 WSK サブシステムが IRP を完了すると、完了ルーチンを呼び出すことによってクライアントに通知します。 そのバッファーへの参照は、完了ルーチンの*コンテキスト*パラメーターで wsk サブシステムによってクライアントに渡されます。 バッファーのサイズは、 *Irp&gt;IoStatus. 情報*に格納されます。

クライアントは、 *irp&gt;IoStatus. status*をチェックすることによって、irp の状態を取得できます。 *Irp&gt;iostatus。* 要求が成功した場合、状態は **成功\_正常**に設定されます。 それ以外の場合は、**状態\_整数\_オーバーフロー**、**状態\_\_見つかりません**、**ステータス\_バッファー\_小さすぎる**、または**状態**\_バッファー\_\_小さ、呼び出しは成功しません。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>サポートされている最小のクライアント</p></td>
<td><p>Windows 8</p></td>
</tr>
<tr class="even">
<td><p>サポートされている最小のサーバー</p></td>
<td><p>Windows Server 2012</p></td>
</tr>
<tr class="odd">
<td><p>Header</p></td>
<td>Mstcpip.h</td>
</tr>
<tr class="even">
<td><p>IRQL</p></td>
<td><p>PASSIVE_LEVEL</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[バインドまたは接続リダイレクトの使用](https://docs.microsoft.com/windows-hardware/drivers/network/using-bind-or-connect-redirection)

[Winsock カーネル関数での Irp の使用](https://docs.microsoft.com/windows-hardware/drivers/network/using-irps-with-winsock-kernel-functions)

[**SIO\_クエリ\_WFP\_接続\_リダイレクト\_レコード**](sio-query-wfp-connection-redirect-records.md)

[**SIO\_クエリ\_WFP\_接続\_リダイレクト\_コンテキスト (SDK)** ](https://docs.microsoft.com/previous-versions/windows/desktop/legacy/hh859712(v=vs.85))

 

 




