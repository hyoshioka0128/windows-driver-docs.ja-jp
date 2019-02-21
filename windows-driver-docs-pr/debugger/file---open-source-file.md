---
title: ファイルのオープン ソース ファイル
description: ファイルのオープン ソース ファイル
ms.assetid: 27007865-7517-40df-a30a-26ecf3cec9f5
keywords:
- ファイルのオープン ソース ファイル
- ソース ファイルのオープン ソース ファイルをデバッグします。
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: bcd7041e4deceefaec71de6e784c4be9910c7d85
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527843"
---
# <a name="file--open-source-file"></a>ファイル |ソース ファイルを開く


## <span id="ddk_file_open_source_file_dbg"></span><span id="DDK_FILE_OPEN_SOURCE_FILE_DBG"></span>


クリックして**ソース ファイルを開く**上、**ファイル** メニューの特定のソース ファイルを読み込めません。

このコマンドは、CTRL キーを押しながら O キーを押すか、クリックしてに相当、**オープン ソース ファイル (Ctrl + O)** ボタン (![オープン ソース ファイル ボタンのスクリーン ショット](images/tbopen.png))。

### <a name="span-iddialogboxspanspan-iddialogboxspandialog-box"></a><span id="dialog_box"></span><span id="DIALOG_BOX"></span>ダイアログ ボックス

クリックすると**ソース ファイルを開く**、**ソース ファイルを開く** ダイアログ ボックスが表示されます。 ファイルを開くには、次の操作を行います。

1.  **検索**一覧で、ファイルがあるディレクトリを選択します。 最後に開かれたディレクトリは、既定で選択されます。

2.  **ファイルの種類**一覧で、開くファイルの種類を選択します。 選択した拡張子を持つファイルのみが表示されます、**ソース ファイルを開く** ダイアログ ボックス。
    **注**  ワイルドカードのパターンを使用することもできます、**ファイル名**特定の拡張子を持つファイルのみを表示するボックスです。 新しいワイルドカード パターンは、セッションを変更するまで保持されます。 ワイルドカード パターンをセミコロンで区切られたの任意の組み合わせを使用することができます。 たとえば、入力**\*します。INC;\*.H;\*.CPP**これらの拡張機能のすべてのファイルを表示します。 行にある文字の最大数は、251 です。

     

3.  ファイルを検索する場合、ファイル名をダブルクリックまたはファイル名をクリックして、をクリックして**オープン**します。

    または

    変更を破棄し、ダイアログ ボックスを閉じ、次のようにクリックします。**キャンセル**します。

ポイントすると、WinDbg で最も最近開かれた 4 つのファイルの名前が表示されます**最近使ったファイル**上、**ファイル**メニュー。 これらのファイルを開くには、その名前をクリックします。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

ソース ファイルとソース パスの詳細については、およびソース ファイルを読み込むには、他の方法については、「[ソース パス](source-path.md)します。

 

 





