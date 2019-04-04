---
title: ソフトウェア トレースするためのツール
description: WDK には、Event Tracing for Windows (ETW) をサポートし、Windows に含まれているトレース ツールを補完するように設計されたツールが含まれています。
ms.assetid: 31056b02-378f-4756-b5a0-3d4cbbc6d3da
keywords:
- ツールを WDK、ソフトウェア トレース
- ドライバーの開発ツールを WDK、ソフトウェア トレース
- ソフトウェアの WDK のトレース
- WDK のトレース
- WDK のソフトウェア トレースのトレース
- WDK のトレース イベント
- トレース ツールを WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8ea87821206a6aba081bd95a836042b86c515328
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528894"
---
# <a name="tools-for-software-tracing"></a>ソフトウェア トレースするためのツール


Microsoft Windows Driver Kit (WDK) には、アプリケーションとソフトウェア トレース用コマンド ライン ツールのセットが含まれています。 これらのツールは、Event Tracing for Windows (ETW) をサポートし、Windows に含まれているトレース ツールを補完するものです。

- [トレース ツールとは](#what-are-the-tracing-tools)
- [WPP ソフトウェア トレースまたは、Event Tracing for Windows (ETW) API を使用する必要がありますはいつでしょうか。](#when-should-i-use-wpp-software-tracing-or-the-event-tracing-for-windows-etw-api)
- [このセクションでは新機能](#whats-in-this-section)

## <a name="what-are-the-tracing-tools"></a>トレース ツールとは

ツールが含まれて[コント ローラーをトレース](trace-controller.md)構成、開始、更新、およびトレースのセッションを停止して[トレース コンシューマー](trace-consumer.md)セッション中に生成されたトレース メッセージを受信し、バイナリ データを変換します。ファイルまたは表示するための人間が判読できる形式です。

ツールは、サポート、さまざまな[トレース プロバイダー](trace-provider.md)ユーザー モード アプリケーションとカーネル モード ドライバーを使用して、ソフトウェア トレースのインストルメント化を含めて、 [WPP ソフトウェア トレース](wpp-software-tracing.md)または ([Event Tracing for Windows (ETW)](event-tracing-for-windows--etw-.md)します。 2 つの比較は、コードをインストルメント化するアプローチ、参照してください[使用 WPP ソフトウェア トレースおよび Event Tracing for Windows (ETW) する](#when-should-i-use-wpp-software-tracing-or-the-event-tracing-for-windows-etw-api)します。

また、ツールにアクセスできます予約[トレース セッション](trace-session.md)など、Windows に組み込まれている、[グローバル ロガー トレース セッション](global-logger-trace-session.md) / [トレース セッションの NT Kernel Logger](nt-kernel-logger-trace-session.md).

これらのツールのいくつかのツールにある\\&lt;*プラットフォーム*&gt;サブディレクトリ Windows Driver Kit (WDK) の場所&lt;*プラットフォーム*&gt;は x86 または x64 のいずれか。 その他のツールは Windows に付属するか、箱にあるまたは\\&lt;*プラットフォーム*&gt; WDK のサブディレクトリ。

## <a name="when-should-i-use-wpp-software-tracing-or-the-event-tracing-for-windows-etw-api"></a>WPP ソフトウェア トレースまたは、Event Tracing for Windows (ETW) API を使用する必要がありますはいつでしょうか。

使用[WPP ソフトウェア トレース](wpp-software-tracing.md)開発のためのトレース データを収集すると、デバッグ目的で主に関心がある場合。 使用[Event Tracing for Windows (ETW)](event-tracing-for-windows--etw-.md)他の種類のトレース。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">WPP ソフトウェア トレース</th>
<th align="left">Manifested/TraceLogging ETW</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">Windows 2000 以降でサポートされています。</td>
<td align="left">Windows Vista 以降でサポートされています。</td>
</tr>
<tr class="even">
<td align="left">開発およびデバッグ用のイベントをトレースします。 ほとんどの内部開発者重点を置いています。</td>
<td align="left">管理、運用、分析およびデバッグのためのイベントをトレースします。</td>
</tr>
<tr class="even">
<td align="left">TMF ファイルがログ記録のバイナリの PDB から抽出すると、イベントをデコードする必要があります。</td>
<td align="left">イベントをデコードするメタデータは、ローカルのバイナリまたはイベントのペイロードに含まれています。</td>
</tr>
<tr class="odd">
<td align="left">トレース プロバイダーごとの 1 つだけのアクティブなセッションを指定できます。</td>
<td align="left">イベントを複数のコンシューマーに多重化することができます。</td>
</tr>
<tr class="even">
<td align="left">メッセージ文字列をローカライズすることはできません。</td>
<td align="left">文字列をローカライズすることができます。</td>
</tr>
<tr class="odd">
<td align="left">プロバイダーのセキュリティは、有効にして、それぞれのイベントをデコードするために必要なコントロールの GUID または TMF ファイルを共有しないことに制限されています。</td>
<td align="left">プロバイダーは、ユーザーはそこからイベントを収集することができますの制限に適用される Acl を持つことができます。</td>
</tr>
</tbody>
</table> 

Windows ソフトウェア トレース プリプロセッサ (WPP) マクロを使用して、ソフトウェア トレース ドライバーまたはアプリケーションを追加する方法については、[WPP ソフトウェア トレース](wpp-software-tracing.md)を参照してください。

ドライバーの使用、カーネル モードの ETW API については、[Event Tracing for Windows (ETW)](event-tracing-for-windows--etw-.md)を参照してください。

Windows Driver Model (WDM) に Windows Management Instrumentation (WMI) の拡張機能を使用して、ソフトウェア トレースのドライバーを追加する方法については、[WMI Event Tracing](https://msdn.microsoft.com/library/windows/hardware/ff566350)を参照してください。

**注**   ETW と WPP カーネル モード ドライバーとユーザー モード アプリケーションのほとんどの種類をサポートします。 ただし、ETW と WPP は、ドライバー、ミニポート ドライバーなどの特定の種類では使用する型を使用します。 特定のドライバーの種類がサポートされているかどうかを判断する基本的な WPP にマクロを追加、ドライバーなど[WPP\_INIT\_トレース](https://msdn.microsoft.com/library/windows/hardware/ff556191)と[WPP\_クリーンアップ](https://msdn.microsoft.com/library/windows/hardware/ff556179)します。 使用される型が定義されていないため、コードがコンパイルできない場合は、ETW と WPP がドライバーの種類をサポートできません。 

## <a name="whats-in-this-section"></a>このセクションでは新機能

ここでは、ソフトウェア トレース ツールのアンケートを開始し、ツールを基になる概念を説明します、WDK に含まれてし、ソフトウェア トレース ツールのドキュメントが含まれています。

このセクションの内容:

[ソフトウェア トレース ツールのアンケート](survey-of-software-tracing-tools.md)

[トレース ツールの概念](tracing-tool-concepts.md)

[Traceview で](traceview.md)

[トレース ログ](tracelog.md)

[Tracepdb](tracepdb.md)

[Tracefmt](tracefmt.md)

[起動中にトレース](tracing-during-boot.md)

[WPP ソフトウェア トレース](wpp-software-tracing.md)

[ソフトウェアのトレースに関する FAQ](software-tracing-faq.md)

[Event Tracing for Windows (ETW)](event-tracing-for-windows--etw-.md)

[カーネル モードのパフォーマンスの監視](kernel-mode-performance-monitoring.md)

概念的な情報は[イベントのトレースに関する](https://msdn.microsoft.com/library/windows/desktop/aa363668)、Microsoft Windows SDK のドキュメントを参照してください。 
