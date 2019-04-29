---
title: トレース メッセージのプレフィックスでソース行番号を含める方法
description: トレース メッセージのプレフィックスでソース行番号を含める方法
ms.assetid: 07fbdd27-59a9-4fe1-8662-6c2489efdb7f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9bf5bde84c25e0936ad7ccdd4a47eb8a2d564f65
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63329880"
---
# <a name="how-to-include-the-source-line-number-in-the-trace-message-prefix"></a>トレース メッセージのプレフィックスにソースの行番号を含める方法

WPP はされるは、既定では表示されません、各トレース メッセージに関するデータを自動的に記録します。 このデータには、関数名、ファイル名、ソース行番号、コンポーネント名、サブコンポーネント名、およびトレース メッセージのトレース レベルが含まれます。

この情報を表示する、[トレース メッセージのプレフィックス](trace-message-prefix.md)を各トレース メッセージの前に、定義済みのプレフィックス変数 % トレースを追加\_形式\_%path% 環境変数のプレフィックス。 [Tracefmt](tracefmt.md) % トレースを使用して、その他のトレース コンシューマーと\_形式\_プレフィックス % にトレース メッセージの書式設定します。

たとえば、トレース メッセージのプレフィックスにコンポーネント名、関数名、ファイル名、および行番号を追加するに % トレースの値に、次の変数を追加\_形式\_プレフィックス %。

|変数|説明|
|----|----|
|**%!COMPNAME!**|コンポーネント名を追加します。|
|**%!FUNC!**|関数名を追加します。|
|**%2**|名前、ソース ファイルとトレース ステートメントの行番号を追加します。|

**%2**変数は、次の文字列を返します。

```command
filename_NNN
```

場所、ドット (**.**) ファイルの名前はアンダー スコアに置き換えられます (**\_**) と*NNN*の行番号です。

次の例の SET ステートメントを追加、 **% です。COMPNAME**、 **% です。FUNC!** **%2** % トレースの既定値に変数\_形式\_プレフィックス % です。 **! S!** サブパラ メーターを指定する値の **%2**は文字列として書式設定します。 追加された変数は、太字で表示されます。

```command
set TRACE\_FORMAT\_PREFIX="\[%9!d!\]%8!04X!.%3!04X!::%4!s! \[%1!s!\](**%!COMPNAME!**:**%!FUNC!**:**%2**!s!)"
```

結果として得られるプレフィックスには、次の形式があります。 かっこ内に新しい要素が表示されます。

\[*CPUNumber*\]*ProcessID*.*ThreadID*::*SystemTime* \[ *MessageGUIDFriendlyName*\](*ComponentName*:*FunctionName*:*Filename*\_*LineNumber*)

詳細の例では、次を参照してください。[例 7。トレース メッセージのプレフィックスをカスタマイズする](example-7--customizing-the-trace-message-prefix.md)します。 トレース メッセージのプレフィックスに含まれるすべての定義済み変数の一覧では、次を参照してください。[トレース メッセージのプレフィックス](trace-message-prefix.md)します。
