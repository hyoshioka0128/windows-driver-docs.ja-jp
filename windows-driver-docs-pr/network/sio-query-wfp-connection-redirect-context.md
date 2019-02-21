---
title: SIO_QUERY_WFP_CONNECTION_REDIRECT_CONTEXT 制御コード
description: SIO_QUERY_WFP_CONNECTION_REDIRECT_CONTEXT ソケット I/O 制御操作には、Winsock クライアントはリダイレクトされた接続のリダイレクト レコードのリダイレクトのコンテキストを取得するができます。
ms.assetid: D23971FC-D75F-4C39-BE6A-F0E17F7C1804
ms.date: 08/08/2017
keywords: -Windows Vista 以降のドライバーをネットワーク SIO_QUERY_WFP_CONNECTION_REDIRECT_CONTEXT 制御コード
ms.localizationpriority: medium
ms.openlocfilehash: a8bfb1206a1e16d26f55487b8db5e94ea82f65bb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549240"
---
# <a name="sioquerywfpconnectionredirectcontext-control-code"></a>SIO\_クエリ\_WFP\_接続\_リダイレクト\_コンテキスト コントロールのコード


**SIO\_クエリ\_WFP\_接続\_リダイレクト\_コンテキスト**ソケット I/O 制御操作により、Winsock クライアントは、リダイレクトのコンテキストを取得します。リダイレクトされた接続のレコードをリダイレクトします。

WFP リダイレクト レコードは、WFP が送信プロキシ接続を設定する必要があり、リダイレクトされた接続と、元の接続が論理的に関連する非透過データのバッファーです。

**注**  、 [ **SIO\_クエリ\_WFP\_接続\_リダイレクト\_レコード**](sio-query-wfp-connection-redirect-records.md)クエリできます接続がリダイレクトされる場合にのみ使用、 **FWPS\_レイヤー\_ALE\_CONNECT\_リダイレクト\_V4**または**FWPS\_レイヤー\_ALE\_CONNECT\_リダイレクト\_V6** WFP クライアント レイヤー。

 

リダイレクトの詳細については、次を参照してください。 [Bind を使用して、または接続のリダイレクト](https://msdn.microsoft.com/library/windows/hardware/ff571005)します。

Winsock クライアントが呼び出すリダイレクト レコードのリダイレクトのコンテキストを照会、 [ **WskControlSocket** ](https://msdn.microsoft.com/library/windows/hardware/ff571127)関数は次のパラメーター。

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
<td><p><em>レベル</em></p></td>
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
<td><p>指すバッファーのバイト単位で、サイズ、 <em>OutputBuffer</em>パラメーター。</p></td>
</tr>
<tr class="odd">
<td><p><em>OutputBuffer</em></p></td>
<td><p>受け入れられた TCP 接続のリダイレクトのレコードのリダイレクトのコンテキストを受け取るバッファーへのポインター。 バッファーのサイズがで指定された、 <em>OutputSize</em>パラメーター。</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p>ポインターを<strong>ULONG</strong>-型指定された変数が指すバッファーにコピーされたデータのバイト数を受け取る、 <em>OutputBuffer</em>パラメーター。</p></td>
</tr>
<tr class="odd">
<td><p>Irp</p></td>
<td><p>IRP へのポインター。</p></td>
</tr>
</tbody>
</table>

 

呼び出し元は、次の方法のいずれかでこのクエリを実行できます。

-   設定できる、 *OutputBuffer*に大きなサイズで約 1 KB のバッファーします。 出力バッファー サイズが十分でない場合[ **WskControlSocket** ](https://msdn.microsoft.com/library/windows/hardware/ff571127)戻ります**状態\_バッファー\_すぎます\_小さな**と*OutputSizeReturned*必要なバッファーのサイズが含まれます。 大きなバッファーを割り当てられ、 **WskControlSocket**でもう一度呼び出すと、 **SIO\_クエリ\_WFP\_接続\_リダイレクト\_コンテキスト**要求と*OutputBuffer*より大きなバッファーを設定します。
-   設定できますか、 *OutputSize*パラメーターを 0 にし、 *OutputBuffer*に NULL を呼び出して[ **WskControlSocket**](https://msdn.microsoft.com/library/windows/hardware/ff571127)します。 完了すると、 **WskControlSocket**関数での出力バッファーのサイズ (バイト単位) 単位の取得、 *OutputSizeReturned*パラメーター。 適切なサイズのバッファーを割り当てられ、 **WskControlSocket**でもう一度呼び出すと、 **SIO\_クエリ\_WFP\_接続\_リダイレクト\_コンテキスト**要求と*OutputBuffer*バッファーに設定します。

**注**  を使用して、ユーザー モード アプリケーションでこのクエリを実行することも[ **SIO\_クエリ\_WFP\_接続\_リダイレクト\_コンテキスト (SDK)**](https://msdn.microsoft.com/library/windows/desktop/hh859712)します。

 

この種の要求では、Winsock クライアントは IRP へのポインターとその完了ルーチンへのポインターを指定する必要があります。 以上のドライバーをクライアントに IRP を渡せるまたは IRP を割り当て、クライアントを選択できます。 完了ルーチンを指定する、クライアントが呼び出す必要があります[ **IoSetCompletionRoutine**](https://msdn.microsoft.com/library/windows/hardware/ff549679)します。 詳細については、次を参照してください。 [Winsock カーネル関数を使用して Irp](https://msdn.microsoft.com/library/windows/hardware/ff571006)します。

Winsock クライアント WSK サブシステムによって IRP が完了するまで、割り当てられたバッファーを解放する必要があります。 WSK サブシステムには、IRP が完了すると、完了ルーチンを呼び出すことによって、クライアントを通知します。 WSK サブシステムによってそのバッファーへの参照がクライアントに渡される、*コンテキスト*完了ルーチンのパラメーター。 バッファーのサイズが格納されている*Irp -&gt;IoStatus.Information*します。

チェックして、クライアントが IRP の状態を取得できます*Irp -&gt;IoStatus.Status*します。 *Irp -&gt;IoStatus.Status*に設定されます**状態\_成功**要求が成功した場合。 それが含まれます**状態\_整数\_OVERFLOW**、**状態\_いない\_が見つかりました**、**状態\_バッファー\_すぎます\_小さな**、または**状態\_アクセス\_DENIED**呼び出しが成功しなかった場合。

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


[Bind を使用して、またはリダイレクトの接続](https://msdn.microsoft.com/library/windows/hardware/ff571005)

[Winsock カーネル関数での Irp の使用](https://msdn.microsoft.com/library/windows/hardware/ff571006)

[**SIO\_クエリ\_WFP\_接続\_リダイレクト\_レコード**](sio-query-wfp-connection-redirect-records.md)

[**SIO\_クエリ\_WFP\_接続\_リダイレクト\_コンテキスト (SDK)**](https://msdn.microsoft.com/library/windows/desktop/hh859712)

 

 




