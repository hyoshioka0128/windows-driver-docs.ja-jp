---
title: ドライバーのイベント トレーシングについて
description: ドライバーのイベント トレーシングについて
ms.assetid: 1b5c85b1-5b7a-48bc-bdd4-356316d4467f
keywords:
- Event Tracing for Windows Event Tracing for Windows は、WDK
- ETW の WDK、Event Tracing for Windows について
- Event Tracing for Windows WDK、カーネル モード
- ETW の WDK、カーネル モード
- カーネル モードの ETW WDK ソフトウェア トレース
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 23fee31ba48a8afb8f50a267438e5524e9b70faf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358089"
---
# <a name="about-event-tracing-for-drivers"></a>ドライバーのイベント トレーシングについて


## <a name="what-is-event-tracing"></a>イベントのトレースとは

Event Tracing for Windows (ETW) は、トレースとユーザー モード アプリケーションとカーネル モード ドライバーで発生するイベントをログ記録を効率的かつ効果的なメカニズムです。 ETW は、3 つのコンポーネントで構成されます。

<table>
<thead>
<tr class="header">
<th align="left">用語</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>プロバイダー</p></td>
<td align="left"><p>アプリケーションやトレース インストルメンテーションのイベントを発生させるコンポーネントです。</p></td>
</tr>
<tr class="even">
<td align="left"><p>コント ローラー</p></td>
<td align="left"><p>開始、停止、およびイベント トレース セッションを構成するアプリケーション。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>コンシューマー</p></td>
<td align="left"><p>(リアルタイム) でのイベント トレース セッションを受信するアプリケーションまたはファイル。</p></td>
</tr>
</tbody>
</table>

 

## <a name="the-etw-kernel-mode-api"></a>ETW カーネル モード API

ETW のアプリケーション プログラミング インターフェイス (API) では、カーネル モード コンポーネントとドライバーを使用できる関数のセットを提供します。 [WMI イベントのトレース](https://docs.microsoft.com/windows-hardware/drivers/kernel/wmi-event-tracing)と[WPP ソフトウェア トレース](wpp-software-tracing.md)どちらも ETW を使用します。 ドライバー開発者は、ETW プロバイダーとして、ドライバーを登録するのにこれらの関数を使用できます。 ETW プロバイダーはイベントを発生させることができますを Windows イベント ログを発行したり、トレース ファイルに書き込まれるを取得またはリアルタイムのコンシューマーに配信される ETW セッションにイベントを書き込むことができます。 イベントは、システムで興味深い実行する回数を記述し、ETW プロバイダーによって決定される属性のセットによって定義されているエンティティです。

ETW では、Windows オペレーティング システムでは実装され、開発者がパフォーマンスにほとんど影響の高速で信頼性が高く、かつ汎用的な一連のイベント トレース機能を提供します。 動的に有効または無効にすることができます、コンピューターの再起動や、アプリケーションまたはドライバーを再読み込みせずトレースします。 開発中に、コードを追加するステートメントをデバッグするとは異なり、実稼働コードで ETW を使用できます。

## <a name="when-to-use-event-tracing"></a>イベントのトレースを使用する場合

アプリケーションの開発時に必要な詳細なトレースだけでなく、管理、運用、および分析イベントの目的で使用できるイベントを発行したい場合は、ETW カーネル モードの API を使用します。 主に開発用のトレース データの収集やデバッグのために関心がある場合は、WPP ソフトウェア トレースを使用します。

 

 





