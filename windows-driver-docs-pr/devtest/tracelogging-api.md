---
title: TraceLogging API
description: TraceLogging API
ms.assetid: AE93DD45-05D7-4E7A-B086-B40A6FA0904B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9895c52486ed41a48d92da60a0053c3761696db5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539414"
---
# <a name="tracelogging-api"></a>TraceLogging API

新しい Windows 10、TraceLogging はユーザー モード アプリケーションとカーネル モード ドライバーのトレース フレームワークです。 TraceLogging API がに基づいて[Event Tracing for Windows (ETW)](event-tracing-for-windows--etw-.md)とネイティブ C/C++ の ETW プロバイダーを作成するコードをインストルメント化の簡略化された方法を提供します。 TraceLogging インストルメンテーションは、必要なときに、構造化できますが、個別のインストルメンテーション マニフェスト (XML ファイル) のイベントとイベント データを定義するオーバーヘッドは必要ありません。 さらに、インストルメンテーションを追加すると、 [TraceLogging](https://msdn.microsoft.com/library/windows/desktop/dn904636) API は、パフォーマンスの測定と診断のテレメトリ データを提供する簡単に拡張できます。

[TraceLogging](https://msdn.microsoft.com/library/windows/desktop/dn904636) API の利点の[WPP ソフトウェア トレース](wpp-software-tracing.md)またはデバッグであることが簡単で、簡単にコードをマニフェストに基づくの ETW の利点も提供します、ステートメントを印刷分析し、収集されるトレース データからイベントを関連付けます。

TraceLogging は ETW 上に構築し、既存のツールとの互換性がします。 マニフェスト ベースの ETW を使用するプロバイダーでは、引き続きサポートされます。 テレメトリ データのイベントを必要があるような場合を除く TraceLogging プロバイダーが、ベースの ETW プロバイダーをマニフェストに変換する必要はありません。

[WPP ソフトウェア トレース](wpp-software-tracing.md)は引き続きサポートされます。 ただし、TraceLogging はメンテナンスと拡張性の観点から多くの利点し、コードで使用するも簡単です。

## <a name="span-idinthissectionspanin-this-section"></a><span id="in_this_section"></span>このセクションでは

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">トピック</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="tracelogging-for-kernel-mode-drivers-and-components.md" data-raw-source="[TraceLogging for kernel-mode drivers and components](tracelogging-for-kernel-mode-drivers-and-components.md)">カーネル モード ドライバーとコンポーネントの TraceLogging</a></p></td>
<td align="left"><p>このトピックでは、使用する方法を説明します、 <a href="https://msdn.microsoft.com/library/windows/desktop/dn904636" data-raw-source="[TraceLogging](https://msdn.microsoft.com/library/windows/desktop/dn904636)">TraceLogging</a>からカーネル モード ドライバーとコンポーネント内の API。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="tracelogging-examples.md" data-raw-source="[TraceLogging Examples](tracelogging-examples.md)">TraceLogging 例</a></p></td>
<td align="left"><p>このトピックでソース コードでは、TraceLogging を使用する方法を示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="how-to-fix-tracelogging-build-errors.md" data-raw-source="[How to fix TraceLogging build errors](how-to-fix-tracelogging-build-errors.md)">TraceLogging ビルド エラーを修正する方法</a></p></td>
<td align="left"><p>このトピックでは、一般的なビルド エラーとその解決方法について説明します。</p></td>
</tr>
</tbody>
</table>
