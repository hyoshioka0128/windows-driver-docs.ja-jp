---
title: TCPMON Xcv インターフェイス
description: TCPMON Xcv インターフェイス
ms.assetid: 7b2b1cff-ab8f-44e0-9327-dc60a0072bf5
keywords:
- 印刷モニター WDK、TCPMON Xcv
- transceive (Xcv) インターフェイス WDK 印刷
- Xcv インターフェイス WDK 印刷
- TCPMON Xcv インターフェイス WDK print
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 18800207a56cbc58a1f044f21585b25e19c38a2a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838783"
---
# <a name="tcpmon-xcv-interface"></a>TCPMON Xcv インターフェイス





このセクションでは、標準 TCP/IP ポートモニター (TCPMON) の transceive (Xcv) インターフェイスについて説明します。 このインターフェイスは、 [**XcvData**](https://docs.microsoft.com/previous-versions/ff564255(v=vs.85))および[**XcvDataPort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-xcvdataport)関数呼び出しを使用して実装され、このインターフェイスを使用して tcp/ip プリンターポートを構成したり、tcp/ip プリンターポートの構成に関する情報を取得したりできます。 このセクションで説明する Xcv インターフェイスは、TCP/IP ポートに固有です。 他のポートの種類では、他の Xcv インターフェイスが使用できる場合があります。

ローカルコンピューターまたはリモートコンピューターの Xcv インターフェイスへのハンドルを取得するには、(Microsoft Windows SDK のドキュメントで説明されている) **OpenPrinter**関数を呼び出します。 次のコード例は、ポートへの Xcv ハンドルを取得する方法を示しています。

```cpp
HANDLE hXcv = INVALID_HANDLE_VALUE;
PRINTER_DEFAULTS Defaults = { NULL, NULL, <Required Access> };

// Handle to a local machine
if (OpenPrinter(",XcvPort <PortName>", &hXcv, &Defaults )
{
 // hXvc contains an Xcv data handle to a local TCPMON port
}

// Handle to a remote machine
if (OpenPrinter("<ServerName>\\,XcvPort <PortName>", &hXcv, &Defaults )
{
 // hXvc contains an Xcv data handle to a TCPMON port on <ServerName>
}
```

このコード例では、 *ServerName*と*PortName*はサーバーとポート名の文字列を表します。 ハンドルを取得したら、TCPMON ポートモニターに固有の情報を照会したり、ポートの構成を変更したりできます。 ポートモニターに必要なアクセス権は、プリンター\_の既定の構造体の**DesiredAccess**メンバーに指定する必要があります (特別なセキュリティが必要ない場合は**NULL**が渡されます)。 [**XcvData**](https://docs.microsoft.com/previous-versions/ff564255(v=vs.85))関数の特定の呼び出し (addport コマンドと deleteport コマンドが指定されている場合など) については、「 [Tcpmon xcv コマンド](tcpmon-xcv-commands.md)」を参照してください。サーバー\_ACCESS\_管理特権が必要です。 **OpenPrinter**関数とプリンター\_の既定の構造で要求される可能性のあるアクセス権の詳細については、Windows SDK のドキュメントを参照してください。

ポートがまだ存在しない場合は、モニター名を指定することによって、Xcv ハンドルをサーバーから取得できます。 (標準の TCP/IP ポートモニタポートの場合、これは "標準 TCP/IP ポート" です)。次のコード例は、ポートモニターに対して Xcv データハンドルを取得する方法を示しています。

```cpp
HANDLE hXcv = INVALID_HANDLE_VALUE;
PRINTER_DEFAULTS Defaults = { NULL, NULL, <Required Access> };

// Handle to a local machine
if (OpenPrinter(",XcvMonitor <MonitorName>", &hXcv, &Defaults )
{
 // hXcv contains an Xcv data handle to the monitor <MonitorName>
}

// Handle to a remote machine
if (OpenPrinter("<ServerName>\\,XcvMonitor <MonitorName>", &hXcv, &Defaults )
{
 // hXcv contains an Xcv data handle to the monitor 
 // <MonitorName> on the server <ServerName>
}
```

このコード例では、 *ServerName*と*PortName*はサーバーとポート名の文字列を表します。 Xcv データハンドルを取得したら、 [**XcvData**](https://docs.microsoft.com/previous-versions/ff564255(v=vs.85))関数を呼び出して、モニターに命令と要求を発行できます。

**XcvData**関数の戻り値は、データがポートモニターに正しく送信されたかどうかのみを示します。 戻り値が**TRUE**の場合、操作が成功したことは示されません。 操作が成功したかどうかを確認するには、\**pdwStatus*の値を調べます。 これらの状態値は、次の表にまとめられています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>状態の値</th>
<th>意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>NO_ERROR</p></td>
<td><p>操作は成功しました。</p></td>
</tr>
<tr class="even">
<td><p>ERROR_ACCESS_DENIED</p></td>
<td><p>ユーザーに十分な特権がありません。 コマンドには SERVER_ACCESS_ADMINISTER 特権が必要です。</p></td>
</tr>
<tr class="odd">
<td><p>ERROR_INSUFFICIENT_BUFFER</p></td>
<td><p>出力バッファーが必要ですが、必要なサイズよりも小さくなっています。</p></td>
</tr>
<tr class="even">
<td><p>ERROR_INVALID_DATA</p></td>
<td><p>入力バッファーが必要ですが、それを指すポインターが<strong>NULL</strong>です。</p>
<p>入力バッファーのサイズが必要なサイズを下回っています。</p></td>
</tr>
<tr class="odd">
<td><p>ERROR_INVALID_HANDLE</p></td>
<td><p>Xcv データハンドルが無効です。</p></td>
</tr>
<tr class="even">
<td><p>ERROR_INVALID_LEVEL</p></td>
<td><p>入力または出力のデータ構造が正しいバージョンではありません。</p></td>
</tr>
<tr class="odd">
<td><p>ERROR_INVALID_PARAMETER</p></td>
<td><p>出力バッファーが必要ですが、 <strong>NULL</strong>であるか、または</p>
<p>出力の必須パラメーターが<strong>NULL</strong>で、出力バッファーが小さすぎます。</p>
<p>標準 TCP/IP ポートモニタは、発行されているコマンドを認識しません。</p></td>
</tr>
</tbody>
</table>

 

 

 




