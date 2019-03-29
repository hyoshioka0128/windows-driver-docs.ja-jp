---
title: PDB ファイルでのトレース ログの表示
description: PDB ファイルでのトレース ログの表示
ms.assetid: 267a5d34-6fd0-43b6-aa07-5154bdb2b9a7
keywords:
- プログラム データベース シンボル ファイル WDK
- PDB シンボル ファイルの WDK
- シンボル ファイルの WDK ソフトウェア トレース
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4dc70de6eefd456a9c04fb313d5bba7e1057834e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577856"
---
# <a name="displaying-a-trace-log-with-a-pdb-file"></a>PDB ファイルでのトレース ログの表示


## <span id="ddk_using_a_pdb_file_tools"></span><span id="DDK_USING_A_PDB_FILE_TOOLS"></span>


トレース ログを表示するには、traceview でにログに格納されているトレース メッセージを書式設定する方法を伝える必要があります。 この書式設定情報が記載されて、 [PDB シンボル ファイル](pdb-symbol-files.md)プロバイダー。

をプロバイダーの PDB シンボル ファイルがある場合は、トレース ログを表示する、次の手順を使用します。 PDB シンボル ファイルがないを参照してください。 [TMF ファイルを使用してトレース ログを表示する](displaying-a-trace-log-with-a-tmf-file.md)します。

1.  [Traceview で開始](starting-and-exiting-traceview.md)します。

2.  **ファイル** メニューのをクリックして**既存のログ ファイルを開く**します。

3.  **ログ ファイル名**ボックスに、イベント トレース ログ ファイル (.etl) の名前とパスを入力します。 または、省略記号ボタンをクリックします (**.**)、ファイルに移動します。

4.  **ログ ファイルの選択** ダイアログ ボックスで設定することも選択するその他の生成オプションは、ログ ファイルからファイルを出力します。 この手順は省略可能です。 詳細については、次を参照してください[トレース ログ オプションの設定](setting-trace-log-options.md).。

5.  **[OK]** をクリックします。

6.  をクリックして**PDB (Debug Information) ファイル**へのパスを入力し、 [PDB シンボル ファイル](pdb-symbol-files.md)トレース プロバイダー。 または、省略記号ボタンをクリックします (**.**)、ファイルに移動します。

7.  **[OK]** をクリックします。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

ログの内容を表示する場合にファイルで期待した値、**状態**トレース セッションの一覧の列が**既存**します。 この値は、トレース メッセージをログから取得することを示します、実行中のトレース セッションされません。

 

 





