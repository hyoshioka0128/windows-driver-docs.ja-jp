---
title: 編集行へジャンプ
description: 編集行へジャンプ
ms.assetid: af7f2afc-95cb-4dcd-9b74-1bd46713239f
keywords:
- 編集行へジャンプ
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8da4755023abac4168106b0c3329d47757d370be
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557802"
---
# <a name="edit--go-to-line"></a>編集 |行に移動します。


## <span id="ddk_edit_go_to_line_dbg"></span><span id="DDK_EDIT_GO_TO_LINE_DBG"></span>


をクリックして**行に移動する**上、**編集**メニューで、現在のアクティブな特定の行を検索する[ソース ウィンドウ](source-window.md)。 アクティブなウィンドウがソース ウィンドウではない場合は、このコマンドに効果はありません。

このコマンドは、CTRL + L キーを押すと同じです。

### <a name="span-iddialogboxspanspan-iddialogboxspandialog-box"></a><span id="dialog_box"></span><span id="DIALOG_BOX"></span>ダイアログ ボックス

クリックすると**行に移動する**、**行に移動する** ダイアログ ボックスが表示されます。 このダイアログ ボックスでをクリックして検索する行番号を入力**OK**します。 デバッガーはその行にキャレット (^) に移動します。 行番号が、ファイルの最終行よりも大きい場合は、カーソルは、ファイルの末尾に移動します。

**行に移動する**コマンドのみ WinDbg 表示を変更します。 このコマンドは、ターゲットまたは他のデバッガー操作の実行には影響しません。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

その他のデバッグ情報のウィンドウでテキストの検索方法の詳細については、次を参照してください。[ウィンドウの移動](moving-through-a-window.md)します。

 

 





