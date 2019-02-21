---
title: デバッガーのデータ モデル - テキスト リーダー オブジェクト
description: ファイルからテキストを読み取ります。
ms.date: 12/13/2018
ms.localizationpriority: medium
ms.openlocfilehash: c6ab3867607fbc4e957c629826ec9a69c8e807de
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537614"
---
# <a name="text-reader-objects"></a>テキスト リーダー オブジェクト 
## <a name="summary"></a>概要
テキスト リーダー オブジェクトは、ファイルからテキストを読み取る。

## <a name="object-methods"></a>オブジェクトのメソッド
|名前|署名|説明|
|--- |--- |--- |
|ReadLine|ReadLine()|[次へ] 行の終わり (またはファイルの終わりマーカー) まで、ファイルから読み取りを文字列として読み取りを返します。|
|ReadLineContents|ReadLineContents()|文字列の反復可能なコレクションを返します。 コレクション内の各文字列は、ファイルの 1 つの行を表します。|