---
title: 開く/閉じるログ ファイルを編集します。
description: 開く/閉じるログ ファイルを編集します。
ms.assetid: f63549f7-1516-48a0-8af8-38cca103215c
keywords:
- 開く/閉じるログ ファイルを編集します。
- ログ ファイルを開く/閉じるログ ファイルの編集
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3fa0901060663ed5f1484d6d2b5bdd99ff67903d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331405"
---
# <a name="edit--openclose-log-file"></a>Edit | Open/Close Log File (編集 | ログ ファイルを開く/閉じる)


## <span id="ddk_edit_open_close_log_file_dbg"></span><span id="DDK_EDIT_OPEN_CLOSE_LOG_FILE_DBG"></span>


をクリックして**ログ ファイルを開く/閉じる**上、**編集**] メニューの [新しいログ ファイルに書き込み、既存のログ ファイルを追加または開いているログ ファイルを閉じます。

### <a name="span-iddialogboxspanspan-iddialogboxspandialog-box"></a><span id="dialog_box"></span><span id="DIALOG_BOX"></span>ダイアログ ボックス

クリックすると**ログ ファイルを開く/閉じる**、**ログ ファイルを開く/閉じる** ダイアログ ボックスが表示されます。 このダイアログ ボックスでは、1 つ既に開いている場合、現在のログ ファイルが表示されます。

場合、**ログ ファイル名**チェック ボックスがオフ、ログ ファイルの名前を入力することができます。 選択しない限り、WinDbg で既存のファイルが上書きされますこのファイルが既に存在する場合、 **Append**チェック ボックスをオンします。 ファイル名がないパスを指定する場合、WinDbg は WinDbg からを起動する既定のディレクトリにファイルを挿入します。

場合、**ログ ファイル名**ボックスは、ファイル名を既にが表示されます。 をクリックする**開くログ ファイルを閉じる**ファイルを閉じます。 オフにした場合、**ログ ファイル名**ボックスに新しいログ ファイル名を入力し、以前のログ ファイルは閉じられます。

をクリックして **[ok]** 変更を保存する**キャンセル**の変更を破棄します。

クリックすると**OK**とログ ファイル名には表示されません、**ログ ファイル名**ボックスで、影響を与えません。 WinDbg はしないログ ファイルを閉じますがログ ファイルを開きます。

ただし、ログ ファイルが既にある場合アクティブをクリックして **[ok]** の名前をクリアするかを選択することがなく**Append**WinDbg がログ ファイルを削除し、同じ名前を持つ新しいファイルを使用します。

 

 





