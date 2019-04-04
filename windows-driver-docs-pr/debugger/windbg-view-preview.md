---
title: WinDbg Preview - View Menu
description: このセクションの説明の表示 メニューを操作する方法。
ms.date: 08/09/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4ddc15ec2dfc944a782910eecf35b28d2747cc2c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573156"
---
# <a name="windbg-preview---view-menu"></a>WinDbg Preview - View Menu 

このセクションについて説明します WinDbg プレビューで表示 メニューを操作する方法。

![デバッガーでの表示 メニュー](images/windbgx-view-menu.png)

[表示] メニューを項目ごとに新しいウィンドウを開くまたは 1 つ既に開いている場合は、既存のウィンドウにフォーカスを移動します。

## <a name="command"></a>コマンド 
コマンド ウィンドウを使用すると、デバッガー コマンドを入力できます。 デバッガーのコマンドの詳細については、[デバッガー コマンド](debugger-commands.md)を参照してください。

## <a name="watch"></a>視聴する 

ウォッチ ウィンドウを使用するローカル変数とレジスタを監視できます。 

[ローカル] と [ウォッチ] ウィンドウ、dx コマンドによって使用されるデータ モデルから基づいています。 これは、NatVis または JavaScript の拡張が読み込まれて、dx コマンドと同様の完全な LINQ クエリをサポートする任意のローカル ウィンドウと ウォッチ ウィンドウが役立つことを意味します。 データ モデルの詳細については、[WinDbg Preview - データ モデル](windbg-data-model-preview.md)を参照してください。

## <a name="locals"></a>[ローカル]
[ローカル] ウィンドウには、現在のスコープ内のすべてのローカル変数に関する情報が表示されます。 [ローカル] ウィンドウには、前のコードの実行中に変更された値が強調表示されます。

![デバッガーで [ローカル] ウィンドウ](images/windbgx-locals-window.png)

## <a name="registers"></a>レジスタ

レジスタは、利用可能なプロセッサのレジスタの内容を表示します。 レジスタの詳細については、[登録](registers.md)と[表示と編集、WinDbg で登録](registers-window.md)を参照してください。

## <a name="memory"></a>Memory

メモリの場所を表示するのにには、[メモリ] ウィンドウを使用します。 メモリ アドレスを提供するだけでなく、メモリを調べる $scopeip $eventip などの擬似レジスタの値を使用できます。 追加済みのメモリ ウィンドウに擬似レジスタ値を使用する @ `@$scopeip`。 詳細については、次を参照してください[擬似レジスタ構文。](pseudo-register-syntax.md)


## <a name="stack"></a>スタック 

スタック ウィンドウを使用すると、現在の呼び出し履歴を表示します。 [履歴] ウィンドウでは、現在のフレームの基本的な強調表示を提供します。 

## <a name="disassembly"></a>逆アセンブリ

逆アセンブル ウィンドウでは、現在の命令を強調表示し、スクロールすると、その位置が保持されます。 

![ デバッガーで逆アセンブル ウィンドウ](images/windbgx-disassembly.png)


## <a name="threads"></a>スレッド数

スレッド ウィンドウには、現在のスレッドが強調表示されます。 


## <a name="breakpoints"></a>ブレークポイント

[ブレークポイント] ウィンドウを使用して、表示、有効にし、ブレークポイントをクリアします。

![ デバッガーで逆アセンブル ウィンドウ](images/windbgx-breakpoints-window.png)


## <a name="logs"></a>ログ

 このログは、WinDbg プレビュー内部は。 デバッガー自体のトラブルシューティングに長時間実行されるモニターを表示できます。 
 
 .Logopen コマンドを使用して従来のデバッガー コマンドのログの作成を続行できます。 その詳細については、[WinDbg にログ ファイルを保持](keeping-a-log-file-in-windbg.md)を参照してください。

## <a name="reset-windows"></a>Windows をリセットします。

既定の位置に、デバッガー ウィンドウをリセットするのにには、この関数を使用します。 


## <a name="see-also"></a>関連項目

[WinDbg のプレビューを使用したデバッグ](debugging-using-windbg-preview.md)

 

 





