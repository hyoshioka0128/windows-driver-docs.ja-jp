---
title: テーマの読み込み
description: テーマの読み込み
ms.assetid: 375b7365-6526-4282-893e-91b58a14c31f
keywords:
- テーマを読み込む
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 87ea987d8f75448fcd40c483e2a9b9e84be203b1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383336"
---
# <a name="loading-a-theme"></a>テーマの読み込み


テーマを読み込む前に、すべてのワークスペースのデータを消去することをお勧めします。 これは、次の 3 つの方法で実行できます。

WinDbg のユーザー インターフェイスを使用します。 下、**ファイル**メニューの **ワークスペースをクリアしています.** 選択**すべてクリア**でポップアップ ウィンドウをクリック**OK**します。

下のレジストリ キーを削除することによって**HKCU\\ソフトウェア\\Microsoft\\Windbg\\ワークスペース**します。

コマンドを実行して**reg 削除 HKCU\\ソフトウェア\\Microsoft\\Windbg**します。

結局、ワークスペースのデータが消去されたテーマのいずれかを実行します。 これらは、Windows のツールのデバッグのテーマのディレクトリ内の .reg ファイルとして保存されます。 テーマを実行するには、基本のワークスペースを再定義する、レジストリにその設定をインポートします。

テーマが読み込まれた後を変更するより密接に好みに合わせて可能性があります。 いくつかの一般的なオプションの詳細については、次を参照してください。[テーマのカスタマイズ](customizing-a-theme.md)します。

 

 





