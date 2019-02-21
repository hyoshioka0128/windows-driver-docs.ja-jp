---
title: TCPMON Xcv インターフェイス
description: TCPMON Xcv インターフェイス
ms.assetid: 7b2b1cff-ab8f-44e0-9327-dc60a0072bf5
keywords:
- 印刷モニター WDK、TCPMON Xcv
- WDK の印刷の利用 (Xcv) インターフェイス
- Xcv インターフェイス WDK の印刷
- TCPMON Xcv インターフェイス WDK の印刷
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d0e957fcc8682b79bc708cc6a932f6405fd5669b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551746"
---
# <a name="tcpmon-xcv-interface"></a>TCPMON Xcv インターフェイス





このセクションでは、標準の TCP/IP ポート モニタ (TCPMON) の利用 (Xcv) インターフェイスについて説明します。 このインターフェイスを使用して実装されている[ **XcvData** ](https://msdn.microsoft.com/library/windows/hardware/ff564255)と[ **XcvDataPort** ](https://msdn.microsoft.com/library/windows/hardware/ff564258)関数呼び出し、によりを使用して構成するもの、TCP/IP プリンター ポート、または TCP/IP プリンター ポートの構成に関する情報を取得します。 このセクションで説明されている Xcv インターフェイスは、TCP/IP ポートに固有です。 その他のポートの種類の使用可能な Xcv の他のインターフェイスがあります。

ローカル コンピューターまたはリモート コンピューターのいずれかの Xcv インターフェイスを識別するハンドルを取得する呼び出し、**ようになりました**関数 (Microsoft Windows SDK のドキュメントで説明)。 次のコード例では、ポートへの Xcv ハンドルを取得する方法を示します。

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

コードの例で*ServerName*と*PortName*サーバーとポート名の文字列を表します。 ハンドルを取得すると、TCPMON ポート モニターに固有の情報を照会できるまたはポートの構成を変更することができます。 ポート モニターに必要なアクセスを指定する必要がありますに注意してください、 **DesiredAccess**プリンターのメンバー\_の既定値の構造体 (または渡す**NULL**特別なセキュリティが必要ない場合)。 特定の呼び出し、 [ **XcvData** ](https://msdn.microsoft.com/library/windows/hardware/ff564255)関数 (AddPort と DeletePort コマンドが指定されている場合 - などを参照してください[TCPMON Xcv コマンド](tcpmon-xcv-commands.md))、SERVER\_ 。アクセス\_管理特権が必要です。 詳細については、**ようになりました**関数とアクセス権をプリンターに要求することが\_既定値は構造体を Windows SDK のマニュアルを参照してください。

ポートがまだ存在しない場合、モニター名を指定することによって、Xcv ハンドルをサーバーから取得できます。 (標準の TCP/IP ポート モニター ポート場合これは「標準 TCP/IP ポート」) です。次のコード例では、ポート モニターの Xcv データ ハンドルを取得する方法を示します。

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

コードの例で*ServerName*と*PortName*サーバーとポート名の文字列を表します。 Xcv データのハンドルを入手した場合を実行できる手順と要求モニターに呼び出すことによって、 [ **XcvData** ](https://msdn.microsoft.com/library/windows/hardware/ff564255)関数。

戻り値に注意してください、 **XcvData**ポート モニターにデータが正しく送信されるかどうか関数がのみを示します。 戻り値**TRUE**操作が成功したことを示しません。 操作が成功したかどうかを判断する値を検査\* *pdwStatus*します。 これらの状態値は、次の表にまとめます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>状態値</th>
<th>意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>NO_ERROR</p></td>
<td><p>操作が正常に完了しました。</p></td>
</tr>
<tr class="even">
<td><p>ERROR_ACCESS_DENIED</p></td>
<td><p>ユーザーは、十分な特権を持ちます。 コマンドには、SERVER_ACCESS_ADMINISTER 特権が必要です。</p></td>
</tr>
<tr class="odd">
<td><p>ERROR_INSUFFICIENT_BUFFER</p></td>
<td><p>出力バッファーが必要ですが、必要なより小さい。</p></td>
</tr>
<tr class="even">
<td><p>ERROR_INVALID_DATA</p></td>
<td><p>入力バッファーですが必要ですが、それへのポインターが<strong>NULL</strong>、または</p>
<p>入力バッファーのサイズは、必要な未満です。</p></td>
</tr>
<tr class="odd">
<td><p>ERROR_INVALID_HANDLE</p></td>
<td><p>Xcv データ ハンドルが無効です。</p></td>
</tr>
<tr class="even">
<td><p>ERROR_INVALID_LEVEL</p></td>
<td><p>入力または出力のデータ構造は、適切なバージョンではありません。</p></td>
</tr>
<tr class="odd">
<td><p>ERROR_INVALID_PARAMETER</p></td>
<td><p>出力バッファーが必要ですが、 <strong>NULL</strong>、または</p>
<p>出力は、パラメーターが必要な<strong>NULL</strong>出力バッファーが小さすぎる、または</p>
<p>標準の TCP/IP ポート モニタは、発行中のコマンドを認識できません。</p></td>
</tr>
</tbody>
</table>

 

 

 




