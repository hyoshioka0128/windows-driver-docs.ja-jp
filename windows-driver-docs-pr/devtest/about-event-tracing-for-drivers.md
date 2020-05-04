---
title: ドライバーのイベント トレーシングについて
description: ドライバーのイベント トレーシングについて
ms.assetid: 1b5c85b1-5b7a-48bc-bdd4-356316d4467f
keywords:
- WDK Windows イベントトレーシング、Windows イベントトレーシングについて
- ETW WDK、Windows イベントトレーシングについて
- Windows イベントトレーシング WDK、カーネルモード
- ETW WDK、カーネルモード
- カーネルモード ETW WDK ソフトウェアトレース
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 959a78cf068691a2bba679e3063b1f1ee906f374
ms.sourcegitcommit: 9b791a85c471f0d7707a4a28a2ca273713b7993e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/29/2020
ms.locfileid: "82558847"
---
# <a name="about-event-tracing-for-drivers"></a>ドライバーのイベント トレーシングについて

## <a name="event-tracing-defined"></a>定義されたイベントトレース

Windows イベントトレーシング (ETW) は、ユーザーモードアプリケーションやカーネルモードドライバーによって発生するイベントをトレースおよびログ記録するための効率的で効果的なメカニズムです。 ETW は、次の3つのコンポーネントで構成されます。

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
<td align="left"><p>イベントトレースのインストルメンテーションを発生させるアプリケーションまたはコンポーネント。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Controllers</p></td>
<td align="left"><p>イベントトレースセッションを開始、停止、および構成するアプリケーション。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>コンシューマー</p></td>
<td align="left"><p>イベントトレースセッションを (リアルタイムで) またはファイルから受け取るアプリケーション。</p></td>
</tr>
</tbody>
</table>

## <a name="the-etw-kernel-mode-api"></a>ETW カーネルモード API

ETW アプリケーションプログラミングインターフェイス (API) には、カーネルモードのコンポーネントとドライバーで使用できる一連の関数が用意されています。 [WMI イベントトレーシング](https://docs.microsoft.com/windows-hardware/drivers/kernel/wmi-event-tracing)と[WPP ソフトウェアトレース](wpp-software-tracing.md)はどちらも ETW を使用します。 ドライバー開発者は、これらの関数を使用して、ドライバーを ETW プロバイダーとして登録できます。 ETW プロバイダーはイベントを発生させることができ、イベントを Windows イベントログに発行したり、イベントを ETW セッションに書き込んだりできます。 ETW セッションは、トレースファイルに書き込まれるか、リアルタイムコンシューマーに配信されます。 イベントは、システム内での興味深い出現を記述するエンティティであり、ETW プロバイダーによって決定される一連の属性によって定義されます。

ETW は Windows オペレーティングシステムに実装されており、開発者は、パフォーマンスにほとんど影響を与えることなく、高速で信頼性の高い、汎用性のある一連のイベントトレース機能を提供します。 コンピューターを再起動したり、アプリケーションやドライバーを再読み込みしたりせずに、トレースを動的に有効または無効にすることができます。 開発時にコードに追加するデバッグステートメントとは異なり、ETW を実稼働コードで使用できます。

## <a name="when-to-use-event-tracing"></a>イベントトレースを使用する場合

開発時に必要となる可能性のある詳細なトレースに加えて、管理、操作、および分析イベントに関連するアプリケーションで使用できるイベントを公開する場合は、ETW カーネルモード API を使用します。 主に開発およびデバッグのためにトレースデータを収集する場合は、WPP ソフトウェアトレースを使用します。
