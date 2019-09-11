---
title: デバッガーデータモデル-テキスト Wrtier オブジェクト
description: ファイルにテキストを書き込みます。
ms.date: 12/13/2018
ms.localizationpriority: medium
ms.openlocfilehash: 3decf94b03848a8193677209083ae23a7320c5dd
ms.sourcegitcommit: dff3834724bd5204c4a47204540fe8125dd37b20
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/06/2019
ms.locfileid: "70750033"
---
# <a name="text-writer-objects"></a>テキストライターオブジェクト 
## <a name="summary"></a>Summary
テキストライターオブジェクトは、指定されたエンコーディングのテキストをファイルに書き込みます。

## <a name="object-methods"></a>オブジェクトメソッド
|名前|署名|説明|
|--- |--- |--- |
|書き込み|書き込み (オブジェクト)|指定したオブジェクトの文字列変換を、改行なしでファイルに書き込みます。|
|WriteLine|WriteLine (オブジェクト)|指定したオブジェクトの文字列変換をファイルに書き込み、続けて改行を書き込みます。|
|WriteContents|WriteContents (オブジェクト)|*オブジェクト*を反復処理し、それぞれの間に改行をせずに、反復される各要素の文字列変換をファイルに書き込みます。|
|WriteLineContents|WriteLineContents (オブジェクト)|*オブジェクト*を反復処理し、それぞれの間の改行を使用して、反復される各要素の文字列変換をファイルに書き込みます。|