---
title: パケット処理ドライバーおよびアプリの WFP への移植
description: Windows フィルタ リング プラットフォーム (WFP) は、TCP/IP パケットのフィルター処理、検査、変更、接続の監視または承認、IPsec の規則と処理、および RPC フィルタを使用できます。
ms.assetid: 9BB77BB8-1382-4F65-A4E8-80E229F43425
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 457f1a5bfbfb09344ff7996d10f3b68c43402b41
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581870"
---
# <a name="porting-packet-processing-drivers-and-apps-to-wfp"></a>パケット処理ドライバーおよびアプリの WFP への移植


Windows フィルタ リング プラットフォーム (WFP) は、TCP/IP パケットのフィルター処理、検査、変更、接続の監視または承認、IPsec の規則と処理、および RPC フィルタを使用できます。 一般に、TCP/IP フィルタ リングまたは接続監視 WFP ユーザー モード アプリケーションまたはサービス、WFP カーネル モードのコールアウト ドライバーでは、または Windows Vista および Windows Server 2008 の両方を使用するには、Windows XP および Windows Server 2003 コンポーネントおよびそれ以降を変換する必要があります。 次の表では、既存のパケットでは、Windows XP と Windows Server 2003 とする必要がありますを変更する操作では、Windows Vista および Windows Server 2008 および WFP を使用するには、後で処理の方法を示します。

**注**  時点で、Windows 8 では、トランスポート Driver Interface (TDI) 機能と複数層サービス プロバイダー (Lsp) 機能が非推奨です。

 

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Windows XPand Windows Server 2003 の既存のメソッド</th>
<th align="left">Windows Vista および Windows Server 2008 以降の新しいメソッド</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">ファイアウォール用のフックやフィルターは、単純なパケット フィルター処理するためのドライバーをフックします。</td>
<td align="left">ユーザー モード アプリケーションまたはサービスを使用する、 <a href="https://msdn.microsoft.com/library/windows/desktop/aa366510" data-raw-source="[WFP Win32 API](https://msdn.microsoft.com/library/windows/desktop/aa366510)">WFP Win32 API</a>します。</td>
</tr>
<tr class="even">
<td align="left">ファイアウォールのフックやフィルターは、詳細なパケット検査や変更用のドライバーをフックします。</td>
<td align="left">IP 層、トランスポート層またはアプリケーション レイヤーの強制 (ALE) レイヤーのコールアウト ドライバーと省略可能なユーザー モード アプリケーションまたはサービスを使用する、 <a href="https://msdn.microsoft.com/library/windows/desktop/aa366510" data-raw-source="[WFP Win32 API](https://msdn.microsoft.com/library/windows/desktop/aa366510)">WFP Win32 API</a>します。</td>
</tr>
<tr class="odd">
<td align="left">単純なパケット フィルター処理するためには、Driver Interface (TDI) フィルター ドライバーをトランスポートします。</td>
<td align="left">ユーザー モード アプリケーションまたはサービスを使用する、 <a href="https://msdn.microsoft.com/library/windows/desktop/aa366510" data-raw-source="[WFP Win32 API](https://msdn.microsoft.com/library/windows/desktop/aa366510)">WFP Win32 API</a>します。</td>
</tr>
<tr class="even">
<td align="left">詳細なパケットまたはストリームの検査または変更の TDI フィルター ドライバー。</td>
<td align="left"><p>レイヤー、Stream のレイヤーや ALE コールアウト ドライバーと省略可能なユーザー モード アプリケーションまたはサービスを使用するトランスポート、 <a href="https://msdn.microsoft.com/library/windows/desktop/aa366510" data-raw-source="[WFP Win32 API](https://msdn.microsoft.com/library/windows/desktop/aa366510)">WFP Win32 API</a></p></td>
</tr>
<tr class="odd">
<td align="left">TCP 接続またはユーザー データグラム プロトコル (UDP) トラフィック管理用 TDI フィルター ドライバーです。</td>
<td align="left"><p>TCP 接続管理。ALE コールアウト ドライバーと省略可能なユーザー モード アプリケーションまたはサービスを使用する、 <a href="https://msdn.microsoft.com/library/windows/desktop/aa366510" data-raw-source="[WFP Win32 API](https://msdn.microsoft.com/library/windows/desktop/aa366510)">WFP Win32 API</a>します。</p>
<p>TCP プロキシ処理を行います。</p>
<ul>
<li>Windows vista:パケットの変更のコールアウト ドライバー。</li>
<li>Windows 7 以降で。ALE_REDIRECT レイヤー コールアウト ドライバー。</li>
</ul>
<p>MAC レベルのフィルター処理します。</p>
<ul>
<li>Windows 8 およびそれ以降。MAC_FRAME レイヤー コールアウト ドライバー。</li>
<li>Windows Vista および Windows 7。NDIS ライトウェイト フィルター ドライバー。</li>
</ul>
<p>UDP トラフィックの管理。Stream またはデータグラム データ層のコールアウト ドライバーと省略可能なユーザー モード アプリケーションまたはサービスを使用する、 <a href="https://msdn.microsoft.com/library/windows/desktop/aa366510" data-raw-source="[WFP Win32 API](https://msdn.microsoft.com/library/windows/desktop/aa366510)">WFP Win32 API</a>します。</p></td>
</tr>
<tr class="even">
<td align="left">単純なパケット フィルター処理するための Windows Sockets LSP です。</td>
<td align="left">ユーザー モード アプリケーションまたはサービスを使用する、 <a href="https://msdn.microsoft.com/library/windows/desktop/aa366510" data-raw-source="[WFP Win32 API](https://msdn.microsoft.com/library/windows/desktop/aa366510)">WFP Win32 API</a>します。</td>
</tr>
<tr class="odd">
<td align="left">詳細なパケット検査または変更の Windows Sockets LSP です。</td>
<td align="left"><p>IP レイヤー、ALE、トランスポート (データグラム データなど)、または Stream レイヤー コールアウト ドライバーと省略可能なユーザー モード アプリケーションまたはサービスを使用する、 <a href="https://msdn.microsoft.com/library/windows/desktop/aa366510" data-raw-source="[WFP Win32 API](https://msdn.microsoft.com/library/windows/desktop/aa366510)">WFP Win32 API</a>します。</p></td>
</tr>
<tr class="even">
<td align="left">Network Device Interface Specification (NDIS) 単純なパケット フィルターの中間ドライバー。</td>
<td align="left"><p>IP ベースのフィルター処理します。ユーザー モード アプリケーションまたはサービスを使用する、 <a href="https://msdn.microsoft.com/library/windows/desktop/aa366510" data-raw-source="[WFP Win32 API](https://msdn.microsoft.com/library/windows/desktop/aa366510)">WFP Win32 API</a>します。</p>
<p>MAC に基づくフィルター処理。</p>
<ul>
<li>Windows 8 およびそれ以降。MAC_FRAME レイヤー コールアウト ドライバー。</li>
<li>Windows Vista および Windows 7。NDIS ライトウェイト フィルター ドライバー。</li>
</ul></td>
</tr>
<tr class="odd">
<td align="left">TCP 接続または UDP トラフィック管理用の NDIS 中間のドライバーです。</td>
<td align="left"><p>TCP 接続管理:ALE コールアウト ドライバーと省略可能なユーザー モード アプリケーションまたはサービスを使用する、 <a href="https://msdn.microsoft.com/library/windows/desktop/aa366510" data-raw-source="[WFP Win32 API](https://msdn.microsoft.com/library/windows/desktop/aa366510)">WFP Win32 API</a>します。</p>
<p>UDP トラフィックの管理:ALE またはトランスポート層のコールアウト ドライバーと省略可能なユーザー モード アプリケーションまたはサービスを使用する、 <a href="https://msdn.microsoft.com/library/windows/desktop/aa366510" data-raw-source="[WFP Win32 API](https://msdn.microsoft.com/library/windows/desktop/aa366510)">WFP Win32 API</a>します。</p></td>
</tr>
<tr class="even">
<td align="left">メディア アクセス制御 (MAC) を実行する NDIS ライトウェイト フィルター ドライバーのレベルのフィルター処理します。</td>
<td align="left"><p>Windows 8 およびそれ以降。MAC_FRAME レイヤー コールアウト ドライバー。</p>
<p>Windows Vista および Windows 7。NDIS ライトウェイト フィルター ドライバー。</p></td>
</tr>
</tbody>
</table>

 

 

 





