---
title: デバッガーのデータ モデル - テキスト Wrtier オブジェクト
description: テキスト ファイルを書き込みます。
ms.date: 12/13/2018
ms.localizationpriority: medium
ms.openlocfilehash: 3decf94b03848a8193677209083ae23a7320c5dd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579761"
---
# <a name="text-writer-objects"></a>テキスト ライター オブジェクト 
## <a name="summary"></a>まとめ
テキスト ライター オブジェクトは、ファイルに指定されたエンコーディングのテキストを作成します。

## <a name="object-methods"></a>オブジェクトのメソッド
|名前|署名|説明|
|--- |--- |--- |
|書き込み|Write(object)|指定したオブジェクトの文字列の変換を改行なしのファイルに書き込みます。|
|WriteLine|WriteLine(object)|指定したオブジェクトの文字列の変換を後に改行をファイルに書き込みます。|
|WriteContents|WriteContents(object)|反復処理*オブジェクト*し、各反復処理される要素の文字列の変換を各間の改行なしのファイルに書き込みます。|
|WriteLineContents|WriteLineContents(object)|反復処理*オブジェクト*し、各反復処理される要素の文字列の変換を各間の改行を使用して、ファイルに書き込みます。|