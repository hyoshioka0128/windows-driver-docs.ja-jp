---
title: WIA 診断ログのマクロ
description: WIA 診断ログのマクロ
ms.assetid: 8b544045-e9d7-422b-825c-f1a5531e0e11
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0d6abf2ddb043b2890ad42cb98f2c74f93009dfc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548592"
---
# <a name="wia-diagnostic-log-macros"></a>WIA 診断ログのマクロ





Windows Vista 以降のオペレーティング システムで処理エラーでは、次を参照してください。 [WIA ドライバー エラー Recovery for Windows Vista](wia-driver-error-recovery-for-windows-vista.md)します。

[診断ログ マクロ](https://msdn.microsoft.com/library/windows/hardware/ff540599)ミニドライバー ログ トレース、エラー、警告メッセージを有効にする、 *Wiaservc.log*診断のログ ファイル。

Windows Vista 以降のオペレーティング システムでエラー処理の詳細については、次を参照してください。 [WIA ドライバー エラー Recovery for Windows Vista](wia-driver-error-recovery-for-windows-vista.md)します。

それぞれのエラー、トレース、または警告の種類を指定してログ記録ステートメントを記述する最初の 3 つのマクロを使用できます。 4 番目のマクロを使用して、HRESULT を説明する文字列に変換することができます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>マクロ</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549580" data-raw-source="[&lt;strong&gt;WIAS_LERROR&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549580)"><strong>WIAS_LERROR</strong></a></p></td>
<td><p>ログ ステートメントを入力するとエラーに書き込み、 <em>Wiaservc.log</em>診断のログ ファイル.</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549589" data-raw-source="[&lt;strong&gt;WIAS_LHRESULT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549589)"><strong>WIAS_LHRESULT</strong></a></p></td>
<td><p>HRESULT 値を文字列に変換する文字列を読み書き、 <em>Wiaservc.log</em>診断のログ ファイル。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549600" data-raw-source="[&lt;strong&gt;WIAS_LTRACE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549600)"><strong>WIAS_LTRACE</strong></a></p></td>
<td><p>型のログ ステートメントのトレースを書き込み、 <em>Wiaservc.log</em>診断のログ ファイル.</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549610" data-raw-source="[&lt;strong&gt;WIAS_LWARNING&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549610)"><strong>WIAS_LWARNING</strong></a></p></td>
<td><p>型に対する警告のログ ステートメントを書き込みます、 <em>Wiaservc.log</em>診断のログ ファイル.</p></td>
</tr>
<tr class="odd">
<td><p><strong>WIAS_ERROR</strong></p></td>
<td><p>このマクロは、Windows Vista 以降のオペレーティング システムで使用できます。</p>
<p>ログ ステートメントを入力するとエラーに書き込み、 <em>Wiatrace.log</em>診断のログ ファイル。</p></td>
</tr>
<tr class="even">
<td><p><strong>WIAS_TRACE</strong></p></td>
<td><p>このマクロは、Windows Vista 以降のオペレーティング システムで使用できます。</p>
<p>型のログ ステートメントのトレースを書き込み、 <em>Wiatrace.log</em>診断のログ ファイル。</p></td>
</tr>
</tbody>
</table>

 

これらのマクロの詳細については、次を参照してください。 [IWiaLog インターフェイスおよび診断ログ マクロ](https://msdn.microsoft.com/library/windows/hardware/ff543937)します。

 

 




