---
title: SIO_SET_WFP_CONNECTION_REDIRECT_RECORDS 制御コード
description: SIO_SET_WFP_CONNECTION_REDIRECT_RECORDS ソケット I/O 制御操作には、Winsock クライアントは最終的な宛先に接続するために使用される新しい TCP ソケットにリダイレクト レコードを指定するができます。
ms.assetid: 51FC55BB-FD7A-4FDE-B1FC-02745AC03E33
ms.date: 08/08/2017
keywords: -SIO_SET_WFP_CONNECTION_REDIRECT_RECORDS ネットワーク ドライバーが Windows Vista で始まるコードを制御します。
ms.localizationpriority: medium
ms.openlocfilehash: 051a437a5f5ea91928524334abad5bcf9ad9b81d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377238"
---
# <a name="siosetwfpconnectionredirectrecords-control-code"></a>SIO\_設定\_WFP\_接続\_リダイレクト\_レコード制御コード


**SIO\_設定\_WFP\_接続\_リダイレクト\_レコード**ソケット I/O 制御操作により、新しい TCP にリダイレクト レコードを指定するクライアントは Winsock最終的な宛先に接続するために使用されるソケット。

WFP リダイレクト レコードは、WFP が送信プロキシ接続を設定する必要があり、リダイレクトされた接続と、元の接続が論理的に関連する非透過データのバッファーです。

リダイレクトの詳細については、次を参照してください。 [Bind を使用して、または接続のリダイレクト](https://msdn.microsoft.com/library/windows/hardware/ff571005)します。

Winsock クライアントの呼び出しを最終的な宛先に接続するために使用される新しい TCP ソケットにリダイレクト レコードを設定する、 [ **WskControlSocket** ](https://msdn.microsoft.com/library/windows/hardware/ff571127)関数は次のパラメーター。

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
<td><p>InputBuffer パラメーターが指すリダイレクト レコードのサイズ。</p></td>
</tr>
<tr class="odd">
<td><p><em>InputBuffer</em></p></td>
<td><p>ソケットに関連付けられているリダイレクト レコードへのポインター。</p></td>
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

 

Winsock クライアントのバッファーを割り当てるし、バッファーのサイズへのポインターを指定する必要があります*InputBuffer*と*InputSize します。*

Winsock クライアントが呼び出すときに IRP の完了のルーチンへのポインターを指定する必要があります、 [ **WskControlSocket** ](https://msdn.microsoft.com/library/windows/hardware/ff571127)の要求のこの型の関数。 WSK サブシステムが IRP を完了するまで、クライアントはバッファーを解放する必要があります。 IRP が完了すると、サブシステムは、完了ルーチンを呼び出します。 完了ルーチンで、クライアントが IRP の状態を確認し、いた以前の要求の割り当てられているすべてのリソースを解放する必要があります。

**注**  を使用して、ユーザー モード アプリケーションでこのクエリを実行することも[ **SIO\_設定\_WFP\_接続\_リダイレクト\_レコード (SDK)**](https://msdn.microsoft.com/library/windows/desktop/hh859714)します。

 

WSK IRP の処理の詳細については、次を参照してください。 [Winsock カーネル関数を使用して Irp](https://msdn.microsoft.com/library/windows/hardware/ff571006)します。

チェックして、クライアントが IRP の状態を取得できます*Irp -&gt;IoStatus.Status*します。 *Irp -&gt;IoStatus.Status*に設定されます**状態\_成功**要求が成功した場合。 それが含まれます**状態\_整数\_OVERFLOW**、または**状態\_アクセス\_DENIED**呼び出しが成功しなかった場合。

<a name="requirements"></a>必要条件
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

[**SIO\_設定\_WFP\_接続\_リダイレクト\_レコード (SDK)**](https://msdn.microsoft.com/library/windows/desktop/hh859714)

 

 




