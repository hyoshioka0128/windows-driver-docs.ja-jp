---
title: トレース メッセージのフィルター処理
description: トレース メッセージのフィルター処理
ms.assetid: 6e4be7ea-1a3f-4fb2-900d-b857cd635fde
keywords:
- Traceview で WDK、メッセージをフィルター処理
- フィルター処理のトレース メッセージ WDK
- トレース メッセージをフィルター処理について、トレース メッセージをフィルター処理
- トレース メッセージ フィルター WDK
- WDK、トレース メッセージ フィルターは、トレース メッセージのフィルターについて
- WDK ソフトウェア トレースの規則
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c83cb393620ecfd91e7cb2f9ee1541ea5439b8e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580771"
---
# <a name="filtering-trace-messages"></a>トレース メッセージのフィルター処理

でも、簡単で使い慣れたプロバイダーによって生成されるメッセージの量は、ソフトウェア トレースの操作の課題の 1 つ。 Traceview でのトレース メッセージ フィルターは、検索して重大なメッセージを強調表示し、他のユーザーを非表示にする際に役立ちます。

A*トレース メッセージ フィルター*一連のルールでのトレース メッセージの外観を変更するには、[トレース メッセージ一覧](trace-message-lists.md)します。 すべてのトレース、トレース セッション、ログの表示、またはトレース セッション (またはメッセージ ログ) グループに適用されます。 フィルターは、基になるトレース プロバイダーまたはトレース ログは変更されません。

作成し、完了した後、トレース セッションの実行中に、またはトレース ログの表示中にトレース メッセージのフィルターを変更できます。

このセクションが含まれています

[ルールを追加します。](adding-a-rule.md)

[ルールを削除します。](deleting-a-rule.md)

[条件を変更します。](changing-a-rule.md)

[フィルターを保存しています](saving-a-filter.md)

[ルール要素をフィルター処理します。](filter-rule-elements.md)

[フィルター規則の特別な操作](special-actions-for-filter-rules.md)

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

ほとんどのフィルター規則は、すぐに有効です。 使用するルールをフィルター処理、**破棄**アクションは、ルールが適用された後に到着したメッセージに対してのみ有効になります。 適用する、**破棄**規則、既存のログ ファイルを[ワークスペースを保存](saving-or-resaving-a-workspace.md)、[トレース セッションを削除](removing-a-trace-session.md)、し[、ワークスペースを開き](opening-a-workspace.md)します。

フィルタの規則は、フィルターに出現する順序で適用されます。 トレース メッセージを 1 つ以上のルールに影響する場合は、最初のメッセージに影響するルールのみが適用されます。

ルールをフィルターには、OR 操作によって暗黙的に接続しています。つまり、すべて適用されます。 AND 操作では、ルールを接続するには、選択、 **AND**アクション。
