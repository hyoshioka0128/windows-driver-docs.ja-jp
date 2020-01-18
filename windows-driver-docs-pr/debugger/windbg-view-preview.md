---
title: WinDbg プレビュー-[表示] メニュー
description: ここでは、[表示] メニューの操作方法について説明します。
ms.date: 01/10/2020
ms.localizationpriority: medium
ms.openlocfilehash: 8fbd91f829ad6c9d02ab4cd74f3d643a703be172
ms.sourcegitcommit: 6d930ed810124ade8e29a617c7abcd399113696f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/17/2020
ms.locfileid: "76256691"
---
# <a name="windbg-preview---view-menu"></a>WinDbg プレビュー-[表示] メニュー

![WinDbg プレビューの小さなロゴ](images/windbgx-preview-logo.png)

ここでは、WinDbg Preview の [表示] メニューを操作する方法について説明します。

![デバッガーの [表示] メニュー](images/windbgx-view-menu.png)

[表示] メニューでは、項目ごとに新しいウィンドウが開きます。または、既に開いている場合は、既存のウィンドウにフォーカスを移動します。

## <a name="command"></a>コマンド

[コマンド] ウィンドウでは、デバッガーコマンドを入力できます。 デバッガーコマンドの詳細については、「[デバッガーコマンド](debugger-commands.md)」を参照してください。

## <a name="watch"></a>視聴する

[ウォッチ] ウィンドウでは、ローカル変数とレジスタをウォッチできます。 

[ローカル] ウィンドウと [ウォッチ] ウィンドウは、どちらも dx コマンドで使用されるデータモデルに基づいています。 つまり、[ローカル] ウィンドウと [ウォッチ] ウィンドウでは、読み込まれた NatVis または JavaScript の拡張機能を利用でき、dx コマンドと同様に、完全な LINQ クエリをサポートします。 データモデルの詳細については、「 [WinDbg プレビュー-データモデル](windbg-data-model-preview.md)」を参照してください。

## <a name="locals"></a>ローカル

[ローカル] ウィンドウには、現在のスコープ内のすべてのローカル変数に関する情報が表示されます。 [ローカル] ウィンドウでは、前のコードの実行中に変更された値が強調表示されます。

![デバッガーの [ローカル] ウィンドウ](images/windbgx-locals-window.png)

## <a name="registers"></a>レジスタ

レジスタは、プロセッサが使用可能になったときに、その内容を表示します。 レジスタの詳細については、「 [WinDbg での](registers-window.md)レジスタの登録と表示および編集」[を参照し](registers.md)てください。

## <a name="memory"></a>メモリ

メモリの場所を表示するには、[メモリ] ウィンドウを使用します。 メモリアドレスを指定するだけでなく、$scopeip や $eventip などの擬似レジスタ値を使用してメモリを調べることもできます。 [メモリ] ウィンドウの擬似レジスタ値 (`@$scopeip`など) を使用するように、@ 記号を事前に追加します。 詳細については、「[擬似レジスタの構文](pseudo-register-syntax.md)」を参照してください。

## <a name="stack"></a>Stack

現在の呼び出し履歴を表示するには、[スタック] ウィンドウを使用します。 スタックウィンドウは、現在のフレームの基本的な強調表示を提供します。 

## <a name="disassembly"></a>逆アセンブリ

[逆アセンブル] ウィンドウでは、現在の命令が強調表示され、スクロール時にその位置が保持されます。 

![ デバッガーの [逆アセンブリ] ウィンドウ](images/windbgx-disassembly.png)

## <a name="threads"></a>スレッド数

[スレッド] ウィンドウには、現在のスレッドが強調表示されます。

## <a name="breakpoints"></a>ブレークポイント

[ブレークポイント] ウィンドウを使用すると、ブレークポイントの表示、有効化、およびクリアを行うことができます。

![ デバッガーの [逆アセンブリ] ウィンドウ](images/windbgx-breakpoints-window.png)

## <a name="logs"></a>ログ

 このログは、WinDbg プレビューの内部構造です。 実行時間の長いプロセスを監視し、デバッガー自体のトラブルシューティングを行うために表示できます。

 引き続き、logopen コマンドを使用して、従来のデバッガーコマンドログを作成できます。 詳細については、「 [WinDbg でのログファイルの保持](keeping-a-log-file-in-windbg.md)」を参照してください。

## <a name="notes"></a>注意

メモオプションを使用して、メモウィンドウを開きます。

## <a name="timelines"></a>所要時間

タイムラインウィンドウを開くか、またはタイムラインウィンドウにフォーカスを移動するには、タイムラインを使用します。 タイムラインの詳細については、「 [WinDbg Preview-タイムライン](windbg-timeline-preview.md)」を参照してください。

## <a name="layouts"></a>レイアウト

[レイアウト] プルダウンメニューを使用して、3つのウィンドウレイアウトから選択します。

## <a name="reset-windows"></a>Windows のリセット

デバッガーウィンドウを既定の位置にリセットするには、この関数を使用します。

## <a name="accent-color"></a>アクセント カラー

ドロップダウンメニューを使用して、デバッガーのアクセントカラーを設定します。

## <a name="see-also"></a>関連項目

[WinDbg プレビューを使用したデバッグ](debugging-using-windbg-preview.md)
