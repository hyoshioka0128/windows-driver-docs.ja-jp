---
title: WinDbg プレビュー-[表示] メニュー
description: ここでは、[表示] メニューの操作方法について説明します。
ms.date: 07/02/2020
ms.localizationpriority: medium
ms.openlocfilehash: 8ec196b6f1cf452a47fb756929b3d2bd26d55cd0
ms.sourcegitcommit: f788aa204a3923f9023d8690488459a4d9bc2495
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86141306"
---
# <a name="windbg-preview---view-menu"></a>WinDbg プレビュー-[表示] メニュー

![WinDbg プレビューの小さなロゴ](images/windbgx-preview-logo.png)

ここでは、WinDbg Preview の [表示] メニューを操作する方法について説明します。

![デバッガーの [表示] メニュー](images/windbgx-view-menu.png)

[表示] メニューでは、項目ごとに新しいウィンドウが開きます。または、既に開いている場合は、既存のウィンドウにフォーカスを移動します。

## <a name="command"></a>コマンド

[コマンド] ウィンドウでは、デバッガーコマンドを入力できます。 デバッガーコマンドの詳細については、「[デバッガーコマンド](debugger-commands.md)」を参照してください。

## <a name="watch"></a>Watch

[ウォッチ] ウィンドウでは、ローカル変数とレジスタをウォッチできます。 

[ローカル] ウィンドウと [ウォッチ] ウィンドウは、どちらも dx コマンドで使用されるデータモデルに基づいています。 つまり、[ローカル] ウィンドウと [ウォッチ] ウィンドウでは、読み込まれた NatVis または JavaScript の拡張機能を利用でき、dx コマンドと同様に、完全な LINQ クエリをサポートします。 データモデルの詳細については、「 [WinDbg プレビュー-データモデル](windbg-data-model-preview.md)」を参照してください。

## <a name="locals"></a>ローカル

[ローカル] ウィンドウには、現在のスコープ内のすべてのローカル変数に関する情報が表示されます。 [ローカル] ウィンドウでは、前のコードの実行中に変更された値が強調表示されます。

![デバッガーの [ローカル] ウィンドウ](images/windbgx-locals-window.png)

## <a name="registers"></a>レジスタ

レジスタは、プロセッサが使用可能になったときに、その内容を表示します。 レジスタの詳細については、「 [WinDbg での](registers-window.md)レジスタの登録と表示および編集」[を参照し](registers.md)てください。

## <a name="memory"></a>メモリ

メモリの場所を表示するには、[メモリ] ウィンドウを使用します。 メモリアドレスを指定するだけでなく、$scopeip や $eventip などの擬似レジスタ値を使用してメモリを調べることもできます。 [メモリ] ウィンドウの擬似レジスタ値 (など) を使用するように、@ 記号を事前に追加し `@$scopeip` ます。 詳細については、「[擬似レジスタの構文](pseudo-register-syntax.md)」を参照してください。

## <a name="stack"></a>スタック

現在の呼び出し履歴を表示するには、[スタック] ウィンドウを使用します。 スタックウィンドウは、現在のフレームの基本的な強調表示を提供します。 

## <a name="disassembly"></a>逆アセンブリ

[逆アセンブル] ウィンドウでは、現在の命令が強調表示され、スクロール時にその位置が保持されます。 

![ デバッガーの [逆アセンブリ] ウィンドウ](images/windbgx-disassembly.png)

## <a name="threads"></a>Threads

[スレッド] ウィンドウには、現在のスレッドが強調表示されます。

## <a name="breakpoints"></a>ブレークポイント

[ブレークポイント] ウィンドウを使用すると、ブレークポイントの表示、有効化、およびクリアを行うことができます。

![ デバッガーの [逆アセンブリ] ウィンドウ](images/windbgx-breakpoints-window.png)

## <a name="logs"></a>ログ

 このログは、WinDbg プレビューの内部構造です。 実行時間の長いプロセスを監視し、デバッガー自体のトラブルシューティングを行うために表示できます。

 引き続き、logopen コマンドを使用して、従来のデバッガーコマンドログを作成できます。 詳細については、「 [WinDbg でのログファイルの保持](keeping-a-log-file-in-windbg.md)」を参照してください。

## <a name="notes"></a>メモ

メモオプションを使用して、メモウィンドウを開きます。

## <a name="timelines"></a>タイムライン

タイムラインウィンドウを開くか、またはタイムラインウィンドウにフォーカスを移動するには、タイムラインを使用します。 タイムラインの詳細については、「 [WinDbg Preview-タイムライン](windbg-timeline-preview.md)」を参照してください。

## <a name="modules"></a>モジュール

モジュールを使用して、読み込まれたモジュールとその関連情報を表示します。 モジュールには次のものが表示されます。

- パスの場所を含むモジュールの名前
- 読み込まれたモジュールのサイズ (バイト単位)
- モジュールが読み込まれるベースアドレス。
- ファイル バージョン

![5つのモジュールが表示されているモジュールビューウィンドウ](images/windbgx-view-modules.png)

## <a name="layouts"></a>レイアウト

[レイアウト] プルダウンメニューを使用して、3つのウィンドウレイアウトから選択します。

## <a name="reset-windows"></a>Windows のリセット

デバッガーウィンドウを既定の位置にリセットするには、この関数を使用します。

## <a name="accent-color"></a>アクセントカラー

ドロップダウンメニューを使用して、デバッガーのアクセントカラーを設定します。

## <a name="see-also"></a>参照

[WinDbg プレビューを使用したデバッグ](debugging-using-windbg-preview.md)
