---
title: 各トレース メッセージの前にあるテキストします。
description: 各トレース メッセージの前にあるテキストします。
ms.assetid: bff8eb0b-f571-405f-b930-3003e2c50621
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4aeffbafc960ad92289d51f5ae7738d4582851d4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536834"
---
# <a name="what-is-the-text-that-precedes-each-trace-message"></a>各トレース メッセージの前にあるテキストとは何ですか。


[Tracefmt](tracefmt.md)と[traceview で](traceview.md)追加、[トレース メッセージのプレフィックス](trace-message-prefix.md)を書式を設定する各トレース メッセージ。 プレフィックスは、トレース メッセージに関するデータから成る文字列です。 Tracefmt と traceview で出力では、プレフィックスを表示できます。

次の行は、トレース メッセージのプレフィックスの既定の構文を示しています。

```
[CPUNumber]ProcessID.ThreadID :: SystemTime [MessageGUIDFriendlyName]
```

場所の既定値、 *MessageGUIDFriendlyName*はディレクトリを[トレース プロバイダー](trace-provider.md)がビルドされました。

そのプレフィックス、変数の置換値を持つが表示されます、次の行でトレース ログのサンプルから。

```
[0]0C40.0C3C::09/20/2004-14:41:31.625 [tracedrv]Hello, 1 Hi
```

追加し、プレフィックスから作成または編集 % トレース データ要素を削除する\_形式\_%path% 環境変数のプレフィックス。

手順と % トレースの値に含めることができるデータ要素のリスト\_形式\_% のプレフィックスを参照してください[トレース メッセージのプレフィックス](trace-message-prefix.md)します。
