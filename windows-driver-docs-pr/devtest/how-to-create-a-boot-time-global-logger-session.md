---
title: 起動時のグローバル ロガー セッションを作成する方法
description: 起動時のグローバル ロガー セッションを作成する方法
ms.assetid: ddd9e1b1-d732-4ef1-a0e0-4d8e95660d7c
keywords:
- グローバルの WDK、ロガー トレース セッションを作成します。
- 起動時のグローバル ロガー トレース セッション、WDK を作成します。
- EnableKernelFlags WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e3c4923f32b7f38f04c30f28ec8375168f42cbce
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63329746"
---
# <a name="how-to-create-a-boot-time-global-logger-session"></a>起動時のグローバル ロガー セッションを作成する方法


カーネル イベント ログに記録するグローバル ロガー トレース セッションを作成する最も簡単な方法は、使用することです[Tracelog](tracelog.md)標準グローバル ロガー トレース セッションを作成し、追加、 **EnableKernelFlags**エントリとその。値。 このトピックでは、手順について説明します。

1.  グローバル ロガー トレース セッションを作成するのにには、トレース ログを使用します。 最も簡単なコマンドは次のとおりです。

    ```
    tracelog -start GlobalLogger
    ```

    手順と詳細については、次を参照してください。 [ **Tracelog コマンド構文**](tracelog-command-syntax.md)と[ロガー トレース セッションのグローバル](global-logger-trace-session.md)します。 例については、次を参照してください。[例 13。ロガーがグローバル セッションを作成する](example-13--creating-a-global-logger-session.md)します。

2.  追加、REG\_という名前のバイナリ エントリ**EnableKernelFlags**を**HKLM\\システム\\CurrentControlSet\\コントロール\\WMI\\GlobalLogger**サブキー。 トレース ログを作成、 **GlobalLogger**レジストリ サブキーを使用する場合、 **tracelog-開始**コマンド。 使用できる値**EnableKernelFlags**の値から取得されますが、 **EnableFlags**のメンバー、**イベント\_トレース\_プロパティ**構造体。 説明については、 **EnableFlags**値を参照してください[**イベント\_トレース\_プロパティ**](https://msdn.microsoft.com/library/windows/desktop/aa363784)します。

3.  システムを再起動します。

4.  テストが完了したらを使用して、 **tracelog-削除**GlobalLogger コマンド内のエントリを再初期化する、 **GlobalLogger**サブキー。 それ以外の場合、グローバルのロガーのトレース セッションは、システムを起動するたびを起動します。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

有無、 **EnableKernelFlags**エントリは、有効な値では、グローバルのロガーのトレース セッションを NT Kernel Logger のトレース セッションに変換します。 値**EnableKernelFlags**、他のグローバル ロガー レジストリ エントリと共に、セッションを構成に使用されます。 トレース セッションは、システムを再起動するときに起動します。

システムが完全に動作する前に、構成値が使用可能な必要があるので、グローバル ロガー トレース セッションを構成するレジストリ エントリを使用します。

グローバルのロガーのトレース セッションを構成するには、レジストリを編集するかを使用して[Tracelog](tracelog.md)、Windows Driver Kit (WDK) で含まれているツールです。 グローバル ロガーのトレース セッションを構成するレジストリ エントリの詳細については、次を参照してください。[グローバル ロガー トレース セッション](global-logger-trace-session.md)します。

このトレース セッションを実行すると、使用、 **tracelog-削除**の値を設定するコマンド、**開始**エントリを追加したレジストリ サブキーを削除するには 0。 そうでない場合は、セッションは、システムを起動するたびに実行され、ログは非常に大きくなる可能性があります。

詳細 Tracelog コマンドについては、次を参照してください[ **Tracelog コマンドの構文。**](tracelog-command-syntax.md)

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[**イベント\_トレース\_プロパティ**](https://msdn.microsoft.com/library/windows/desktop/aa363784)

[13 の使用例:ロガーがグローバル セッションを作成します。](example-13--creating-a-global-logger-session.md)

[グローバルなロガー トレース セッション](global-logger-trace-session.md)

[トレース ログ](tracelog.md)

[**Tracelog コマンドの構文**](tracelog-command-syntax.md)

 

 






