---
title: Debugger Data Model - 逆アセンブラー オブジェクト
description: オブジェクトの逆アセンブラーは、特定のアーキテクチャ用のコードを逆アセンブルする機能を有効にします。
ms.date: 12/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9bd54cb1aafc31f42cbf39f5cfa36db4fa6cbf97
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580954"
---
# <a name="disassembler-objects"></a>オブジェクトの逆アセンブラー
## <a name="summary"></a>まとめ
オブジェクトの逆アセンブラーは、特定のアーキテクチャ用のコードを逆アセンブルする機能を有効にします。
## <a name="object-methods"></a>オブジェクトのメソッド
|名前|戻り値の型|署名|説明|
|--- |--- |--- |--- |
|DisassembleBlocks|[コレクション](dbgmodel-namespace-collections.md)の[基本ブロック](dbgmodel-object-basic-block.md)|DisassembleBlocks(address)|逆アセンブルを開始*アドレス*を返します、[コレクション](dbgmodel-namespace-collections.md)の基本的な要素です。 ここで、逆アセンブルは直線的に転送*アドレス*命令、命令によってごとにします。 これは、関数の完全なフロー分析を実行していない、ため、このメソッドによって返される要素の中央にジャンプすることも可能です。 各; から 1 つの終了ポイントなりますただしします。|
|DisassembleInstructions|[コレクション](dbgmodel-namespace-collections.md)の[命令](dbgmodel-object-instruction.md)|DisassembleInstructions(address)|開始に逆アセンブル*アドレス*します。 |
|DisassembleFunction|[コレクション](dbgmodel-namespace-collections.md)の[基本ブロック](dbgmodel-object-basic-block.md)|DisassembleFunction(address)|関数と仮定した場合、始まり*アドレス*、これは関数の完全なフロー分析を実行します。 結果は、[コレクション](dbgmodel-namespace-collections.md)の基本的な要素を 1 つのエントリ ポイントと 1 つの終了ポイント。|
|GetRegister|[登録](dbgmodel-object-register.md)|GetRegister(regId)|指定された登録 id には、register オブジェクトを返します。|
## <a name="remarks"></a>コメント
詳細なシンボリック情報が、逆アセンブルした関数の存在する場合、ここで指定した逆アセンブラーが逆アセンブリ出力を大幅に向上 (例:: 構造体/共用体のフィールドの操作を決定するアドレスとオペランドのサイズが使用されます)。

逆アセンブラーの特定のインスタンスは、優れたエクスペリエンスを実現するために大量のデータをキャッシュする可能性があります。