---
title: アドレスに移動を編集します。
description: アドレスに移動を編集します。
ms.assetid: 152bdbb1-87e5-4a73-a1b7-1c4997f4a41c
keywords:
- アドレスに移動を編集します。
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 382806163042c46208aaeee42fade339070023e7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331406"
---
# <a name="edit--go-to-address"></a>Edit | Go to Address (編集 | アドレスに移動)


## <span id="ddk_edit_go_to_address_dbg"></span><span id="DDK_EDIT_GO_TO_ADDRESS_DBG"></span>


をクリックして**アドレスにアクセスして**で、**編集**] メニューの [ターゲットの仮想アドレス空間内のアドレスに移動します。

このコマンドは、CTRL キーを押しながら G キーを押すことと同等です。

### <a name="span-iddialogboxspanspan-iddialogboxspandialog-box"></a><span id="dialog_box"></span><span id="DIALOG_BOX"></span>ダイアログ ボックス

クリックすると**アドレスにアクセスして**、**ビュー コード オフセット** ダイアログ ボックスが表示されます。 このダイアログ ボックスに移動するアドレスを入力します。 このアドレスは、(関数、シンボル、または整数のメモリ アドレス) などの式、または任意の有効なアドレス指定できます。 アドレスがあいまいな場合は、ダイアログ ボックスには、すべてのあいまいな項目を含むリストが表示されます。

**注**  内の行にカーソルを配置する場合、[逆アセンブル ウィンドウ](disassembly-window.md)または[ソース ウィンドウ](source-window.md)しを使用して、**アドレスにアクセスして**コマンド、選択した行のアドレスが表示されます、**ビュー コード オフセット** ダイアログ ボックス。 このアドレスを使用したり、任意の任意のアドレスに置き換えます。

 

クリックした後**OK**デバッガーは関数または逆アセンブル ウィンドウまたはソース ウィンドウ内のアドレスの先頭にキャレット (^) を移動します。

使用することができます、**アドレスにアクセスして**現在アクティブになっている任意のウィンドウでコマンド。 デバッガーは、逆アセンブル モードでは、WinDbg は逆アセンブル ウィンドウで、アドレスを検索します。 デバッガーは、元のモードでは、WinDbg はソース ウィンドウで、アドレスを検索します。 ソース ウィンドウで、アドレスが見つからない場合、逆アセンブル ウィンドウ内で見つかった WinDbg します。 適切なウィンドウが開いていない場合は、WinDbg が開きます。

**アドレスにアクセスして**コマンドのみ WinDbg 表示を変更します。 このコマンドは、ターゲットまたは他のデバッガー操作の実行には影響しません。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

その他のデバッグ情報のウィンドウでテキストの検索方法の詳細については、次を参照してください。[ウィンドウの移動](moving-through-a-window.md)します。

 

 





