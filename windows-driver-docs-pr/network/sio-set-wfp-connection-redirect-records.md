---
title: SIO_SET_WFP_CONNECTION_REDIRECT_RECORDS 制御コード
description: SIO_SET_WFP_CONNECTION_REDIRECT_RECORDS socket i/o control 操作を使用すると、Winsock クライアントは、最終的な宛先に接続するために使用する新しい TCP ソケットにリダイレクトレコードを指定できます。
ms.assetid: 51FC55BB-FD7A-4FDE-B1FC-02745AC03E33
ms.date: 08/08/2017
keywords: -Windows Vista 以降でコードネットワークドライバーを SIO_SET_WFP_CONNECTION_REDIRECT_RECORDS 制御する
ms.localizationpriority: medium
ms.openlocfilehash: b3617d012cff3a28638a0c8991ba039b5c3f7a14
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841906"
---
# <a name="sio_set_wfp_connection_redirect_records-control-code"></a>SIO\_\_WFP\_接続の設定\_リダイレクト\_レコードの制御コード


**SIO\_SET\_WFP\_接続\_リダイレクト\_レコード**ソケット i/o 制御操作により、Winsock クライアントは、最終的な宛先に接続するために使用する新しい TCP ソケットにリダイレクトレコードを指定できます。

WFP リダイレクトレコードは、リダイレクトされた接続と元の接続が論理的に関連するように、WFP が送信プロキシ接続に対して設定する必要がある不透明なデータのバッファーです。

リダイレクトの詳細については、「 [Using Bind Or Connect リダイレクション](https://docs.microsoft.com/windows-hardware/drivers/network/using-bind-or-connect-redirection)」を参照してください。

最終的な宛先への接続に使用する新しい TCP ソケットにリダイレクトレコードを設定するために、Winsock クライアントは、次のパラメーターを使用して[**Wskcontrolsocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_socket)関数を呼び出します。

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
<td><p><strong>SIO_SET_WFP_CONNECTION_REDIRECT_RECORDS</strong></p></td>
</tr>
<tr class="odd">
<td><p><em>Level</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><em>InputSize</em></p></td>
<td><p>InputBuffer パラメーターが指すリダイレクトレコードのサイズ。</p></td>
</tr>
<tr class="odd">
<td><p><em>InputBuffer</em></p></td>
<td><p>ソケットに関連付けられているリダイレクトレコードへのポインター。</p></td>
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
<tr class="odd">
<td><p>Irp</p></td>
<td><p>IRP へのポインター。</p></td>
</tr>
</tbody>
</table>

 

Winsock クライアントは、バッファーを割り当て、バッファーへのポインターとそのサイズを*InputBuffer*と inputsize で指定する必要があり*ます。*

この種類の要求に対して[**Wskcontrolsocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_socket)関数を呼び出すときに、Winsock クライアントでは、IRP と完了ルーチンへのポインターを指定する必要があります。 クライアントは、WSK サブシステムが IRP を完了するまでバッファーを解放しないようにする必要があります。 IRP が完了すると、サブシステムは完了ルーチンを呼び出します。 完了ルーチンでは、クライアントは IRP の状態を確認し、要求に対して以前に割り当てられたすべてのリソースを解放する必要があります。

また、SIO を使用してユーザーモードアプリケーションでこのクエリを実行することも**でき  ** [ **\_設定\_WFP\_接続\_リダイレクト\_レコード (SDK)** ](https://docs.microsoft.com/previous-versions/windows/desktop/legacy/hh859714(v=vs.85))です。

 

WSK の IRP 処理の詳細については、「 [Winsock カーネル関数での irp の使用](https://docs.microsoft.com/windows-hardware/drivers/network/using-irps-with-winsock-kernel-functions)」を参照してください。

クライアントは、 *irp&gt;IoStatus. status*をチェックすることによって、irp の状態を取得できます。 *Irp&gt;iostatus。* 要求が成功した場合、状態は **成功\_正常**に設定されます。 それ以外の場合は、**状態\_整数\_オーバーフロー**、または呼び出しが成功しなかった場合 **\_アクセス\_拒否**されます。

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

[**SIO\_設定\_WFP\_接続\_リダイレクト\_レコード (SDK)** ](https://docs.microsoft.com/previous-versions/windows/desktop/legacy/hh859714(v=vs.85))

 

 




