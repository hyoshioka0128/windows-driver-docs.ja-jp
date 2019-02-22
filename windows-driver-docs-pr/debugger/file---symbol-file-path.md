---
title: ファイルのシンボル ファイルのパス
description: ファイルのシンボル ファイルのパス
ms.assetid: 22d32b1b-d1b9-4627-99ed-08656da9b849
keywords:
- ファイルのシンボル ファイルのパス
- シンボル ファイルとパス、ファイルのシンボル ファイルのパス
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 28f4b2a4a734841f084667a39c09f82863b7cdca
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556530"
---
# <a name="file--symbol-file-path"></a>ファイル |シンボル ファイルのパス


## <span id="ddk_file_symbol_file_path_dbg"></span><span id="DDK_FILE_SYMBOL_FILE_PATH_DBG"></span>


クリックして**シンボル ファイルのパス**上、**ファイル** メニューの表示、設定、またはシンボル パスに追加します。

このコマンドは、CTRL キーを押しながら S キーを押すことと同等です。

### <a name="span-idsymbolsearchpathdialogboxspanspan-idsymbolsearchpathdialogboxspansymbol-search-path-dialog-box"></a><span id="symbol_search_path_dialog_box"></span><span id="SYMBOL_SEARCH_PATH_DIALOG_BOX"></span>シンボル検索パス ダイアログ ボックス

クリックすると**シンボル ファイルのパス**、**シンボルの検索パス** ダイアログ ボックスが表示されます。 このダイアログ ボックスでは、現在のシンボル パスが表示されます。 場合、**シンボル パス**ボックスは空白には、現在のシンボル パスはありません。

新しいパスを入力または古いパスを編集することができます。 1 つ以上のディレクトリを検索する場合は、セミコロンでディレクトリ名を区切ります。

をクリックして **[ok]** 変更を保存する**キャンセル**の変更を破棄します。

選択した場合、**再読み込み**チェック ボックスで、デバッガーが再度読み込ま読み込まれたすべてのシンボルとイメージをクリックした後**OK**します。 **再読み込み**コマンドを使用すると、 [ **.reload (モジュールの再読み込み)** ](-reload--reload-module-.md)コマンド。

クリックすることもできます**参照**を開く、**フォルダーの参照** ダイアログ ボックス。

### <a name="span-idbrowseforfolderdialogboxspanspan-idbrowseforfolderdialogboxspanbrowse-for-folder-dialog-box"></a><span id="browse_for_folder_dialog_box"></span><span id="BROWSE_FOR_FOLDER_DIALOG_BOX"></span>[フォルダ] ダイアログ ボックスの参照

**フォルダーの参照** ダイアログ ボックスを参照できますフォルダーをコンピューターまたはネットワークにします。 クリックすることも、**フォルダの新規**新しいフォルダーを作成するボタンをクリックします。 ファイルまたはこのダイアログ ボックスでフォルダーを右クリックした場合は、標準の Windows ショートカット メニューが表示されます。

をクリックして**OK**に戻って、選択したフォルダーをシンボル パスに追加する、**シンボルの検索パス** ダイアログ ボックス。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

詳細については、およびシンボル パスを変更するには、他の方法については、「[シンボル パス](symbol-path.md)します。

 

 





