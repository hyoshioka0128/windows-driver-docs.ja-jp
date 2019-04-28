---
title: フィルター規則の特別な操作
description: フィルター規則の特別な操作
ms.assetid: f2631f39-02bb-4bbc-b63b-6a0200d47bc8
keywords:
- WDK の特別な操作のトレース メッセージをフィルター処理
- トレース メッセージは、WDK、特別な操作をフィルター処理します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2e8cb1db779fee081e8a4596257c8ebd71999722
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378020"
---
# <a name="special-actions-for-filter-rules"></a>フィルター規則の特別な操作


次の 3 つの特殊な値が、**アクション**フィルター規則の要素。 次に、これらのアクションについて説明します。

<span id="Ignore"></span><span id="ignore"></span><span id="IGNORE"></span>**無視します。**  
ルールを無視します。 このアクションは、代わりに、ルールを削除します。

<span id="Discard"></span><span id="discard"></span><span id="DISCARD"></span>**破棄**  
トレース メッセージを非表示にします。 このアクションは、新しいメッセージに対してのみ有効です。 ログ ファイルにメッセージを保存して、ログを再読み込みします。 手順については、下の「コメント」を参照してください。

<span id="AND"></span><span id="and"></span>**そして**  
AND 演算によって接続されている複数行のルールを作成します。 適用するアクションの複数行のルールのすべての条件を満たす必要があります。 既定では、すべてのルールをフィルターには、OR 演算子によって接続されます。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

ほとんどのフィルター規則は、すぐに有効です。 使用するルールをフィルター処理、**破棄**アクションは、ルールが適用された後に到着したメッセージに対してのみ有効になります。 適用する、**破棄**規則、既存のログ ファイルを[ワークスペースを保存](saving-or-resaving-a-workspace.md)、[トレース セッションを削除](removing-a-trace-session.md)、し[、ワークスペースを開き](opening-a-workspace.md)します。

 

 





