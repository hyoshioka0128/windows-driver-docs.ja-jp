---
title: ソフトウェア トレースのパフォーマンス コストとは
description: ソフトウェア トレースのパフォーマンス コストとは
ms.assetid: 4337a619-58aa-4ad2-8873-6cbf5d84d074
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5b4ead4614d0640f0ecd41a0b11d4884ecc4ec3b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63386363"
---
# <a name="what-is-the-performance-cost-of-software-tracing"></a>ソフトウェア トレースのパフォーマンス コスト


一般に、ソフトウェア トレースのパフォーマンス コストは、非常に小さいです。 コードを最小限に抑える、バッファーは、効率的に管理およびバイナリ形式で、メッセージが書き込まれます。 また、あるパフォーマンスの大規模なドレイン、トレース メッセージを書式設定がされるまで遅延ユーザーが書式設定し、トレース メッセージを表示します。

使用すると[WPP ソフトウェア トレース](wpp-software-tracing.md)マクロ software を追加するドライバーにトレースがほとんど行われないパフォーマンス コスト、トレース セッションのプロバイダーが有効になっている場合を除き、します。

If 内の 3 つの条件付きチェックを WPP マクロ金額ソフトウェア トレース コード ステートメント。 これらのチェックは、すべてのトレース メッセージが、プロバイダーが有効にしない限り生成されないようにします。 WPP マクロでは、次の形式でコードを生成します。

```
If (WPP_CHECK_INIT && WPP_LEVEL_FLAGS_ENABLED) {
    Call trace_message_routine
}
```

こので生成されたコード、WPP\_確認\_INIT は、1 つの条件付きチェックで構成されています。 WPP\_レベル\_フラグ\_レベルまたはフラグの 1 つだけのフィルターがある場合、1 つの条件付きチェックの有効で構成されます。 それ以外の場合、WPP\_レベル\_フラグ\_有効 には、2 つの条件付きチェックで構成されています。

詳細については、WPP を除外する方法の詳細について\_確認\_INIT は、パフォーマンスの向上のため確認を参照してください[WPP マクロをトレースする前に生成する条件付きチェックを最適化できますか?](can-i-optimize-the-conditional-checks-that-the-wpp-macros-produce-befo.md)。

> [!NOTE]
> WPP ソフトウェア トレース以外のメソッドを使用するには、ドライバー ソフトウェア トレースを実装する場合は、いくつかのパフォーマンス コストがかかることがあります。 効果は、実装方法によって異なります。
