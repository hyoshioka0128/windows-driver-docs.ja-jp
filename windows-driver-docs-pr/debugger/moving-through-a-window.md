---
title: ウィンドウ内を移動
description: ウィンドウ内を移動
ms.assetid: c164a446-1f6c-4d37-8ad6-aa254d3268bc
keywords:
- デバッグ情報ウィンドウを移動します。
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 45f14eadd827386e503aca77ebddb6f2669f1fab
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532695"
---
# <a name="moving-through-a-window"></a>ウィンドウ内を移動


## <span id="ddk_moving_through_a_window_dbg"></span><span id="DDK_MOVING_THROUGH_A_WINDOW_DBG"></span>


デバッグ情報 ウィンドウから移動する際のいくつかの方法はあります。

ウィンドウで、スクロール バーが表示された場合は、ウィンドウの表示に使用できます。

さらに、いくつかのウィンドウのサポート、**検索**、**アドレスにアクセスして**、または**行に移動する**コマンド。 これらのコマンドは、WinDbg 表示のみを変更します。 ターゲットまたは他のデバッガー操作の実行には影響しません。

### <a name="span-idfindcommandspanspan-idfindcommandspanfind-command"></a><span id="find_command"></span><span id="FIND_COMMAND"></span>Find コマンド

使用することができます、**検索**コマンド、[デバッガー コマンド ウィンドウ](debugger-command-window.md)または、[ソース ウィンドウ](source-window.md)します。

これらのウィンドウがアクティブなときにをクリックして**検索**上、**編集**メニューまたは ctrl キーを押しながら F キーを押します。 **検索** ダイアログ ボックスが表示されます。

ダイアログ ボックスで、検索して選択するテキストを入力**を**または**ダウン**検索の方向を判断します。 検索では、カーソルがウィンドウで任意の場所を開始します。 任意の時点でカーソルを移動するには、マウスを使用します。

選択、**単語単位で**チェック ボックスを 1 つの単語を検索する場合。 (このチェック ボックスをオンにし、複数の単語を入力して、このチェック ボックスは無視されます。)選択、**大文字**検索を実行する チェック ボックス。

閉じた場合、**検索**ダイアログ ボックスをクリックすると、順方向に、前回の検索を繰り返すことができます**次を検索**上、**編集**メニューまたは f3 キーを押しています。 SHIFT + F3 キーを押すと、逆方向に検索を繰り返すことができます。

### <a name="span-idgotoaddresscommandspanspan-idgotoaddresscommandspango-to-address-command"></a><span id="go_to_address_command"></span><span id="GO_TO_ADDRESS_COMMAND"></span>コマンドのアドレスに移動

**アドレスにアクセスして**コマンドをデバッグしているアプリケーションでは、住所を検索します。 このオプションを使用する をクリックして**アドレスにアクセスして**上、**編集**メニューまたは CTRL + G キーを押します。

ときに、**ビュー コード オフセット** ダイアログ ボックスが表示されたら、検索するアドレスを入力します。 このアドレスは、関数、シンボル、または整数のメモリ アドレスなど、式として入力できます。 アドレスがあいまいな場合は、すべてあいまいな項目の一覧が表示されます。

クリックした後**OK**、デバッガーが関数または内のアドレスの先頭にカーソルを移動、[逆アセンブル ウィンドウ](disassembly-window.md)または[ソース ウィンドウ](source-window.md)します。

使用することができます、**アドレスにアクセスして**するデバッグ情報ウィンドウが開いてに関係なくコマンド。 デバッガーは、逆アセンブル モードでは、デバッガーは、逆アセンブル ウィンドウで検索するアドレスを検索します。 デバッガーは、元のモードでは、デバッガーは、ソース ウィンドウで、アドレスを検索しようとします。 デバッガーがソース ウィンドウで、アドレスを見つけられない場合、デバッガーは、逆アセンブル ウィンドウで、アドレスを検索します。 必要なウィンドウが開いていない場合は、デバッガーが開きます。

### <a name="span-idmovingtoaspecificlinespanspan-idmovingtoaspecificlinespanmoving-to-a-specific-line"></a><span id="moving_to_a_specific_line"></span><span id="MOVING_TO_A_SPECIFIC_LINE"></span>特定の行に移動

**行に移動する**コマンドの作業中のソース ウィンドウ内の行番号を検索します。 アクティブなウィンドウがソース ウィンドウではない場合は使用できません、**行に移動する**コマンド。

このオプションを有効にするには、クリックして**行に移動する**上、**編集**メニューまたは CTRL + L キーを押します。

ときに、**行に移動する** ダイアログ ボックスが表示されたらをクリックして検索する行番号を入力**OK**します。 デバッガーは、その行にカーソルを移動します。 行番号が、ファイルの最終行よりも大きい場合は、ファイルの末尾にカーソルが移動します。

 

 





