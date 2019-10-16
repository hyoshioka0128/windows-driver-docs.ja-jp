---
title: ファイルオープンソースファイル
description: ファイルオープンソースファイル
ms.assetid: 27007865-7517-40df-a30a-26ecf3cec9f5
keywords:
- ファイルオープンソースファイル
- ソースデバッグ、ファイルオープンソースファイル
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: bcd7041e4deceefaec71de6e784c4be9910c7d85
ms.sourcegitcommit: f017184b00f59b088df87a5bd85fec51b7aed8b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2019
ms.locfileid: "72323604"
---
# <a name="file--open-source-file"></a>File | Open Source File (ファイル | ソース ファイルを開く)


## <span id="ddk_file_open_source_file_dbg"></span><span id="DDK_FILE_OPEN_SOURCE_FILE_DBG"></span>


**[ファイル]** メニューの **[ソースファイルを開く]** をクリックして、特定のソースファイルを読み込みます。

このコマンドは、CTRL キーを押しながら O キーを押すか、または **ソースファイルを開く] (ctrl + o)** ボタンをクリックした場合と同じです (![ [オープンソースファイル] ボタン @ no__t-2)。

### <a name="span-iddialog_boxspanspan-iddialog_boxspandialog-box"></a><span id="dialog_box"></span><span id="DIALOG_BOX"></span>ダイアログボックス

**[ソースファイルを開く]** をクリックすると、 **[ソースファイルを開く]** ダイアログボックスが表示されます。 ファイルを開くには、次の手順を実行します。

1.  **[検索対象]** ボックスの一覧で、ファイルが置かれているディレクトリを選択します。 既定では、最後に開いたディレクトリが選択されています。

2.  **[ファイルの種類]** ボックスの一覧で、開くファイルの種類を選択します。 **[ソースファイルを開く]** ダイアログボックスには、選択した拡張子を持つファイルのみが表示されます。
    **注**  you**ファイル名** ボックスでワイルドカードパターンを使用して、特定の拡張子を持つファイルのみを表示することもできます。 新しいワイルドカードパターンは、変更するまでセッションに保持されます。 ワイルドカードパターンの任意の組み合わせをセミコロンで区切って使用できます。 たとえば、 **\* と入力します。◇\*.始め\*.CPP**では、これらの拡張子を持つすべてのファイルが表示されます。 行の最大文字数は251文字です。

     

3.  目的のファイルが見つかった場合は、ファイル名をダブルクリックするか、ファイル名をクリックして **[開く]** をクリックします。

    または

    変更を破棄してダイアログボックスを閉じるには、 **[キャンセル]** をクリックします。

**[ファイル]** メニューの **[最近使ったファイル]** をポイントすると、WinDbg で最近開いた4つのファイルの名前が表示されます。 これらのファイルのいずれかを開くには、名前をクリックします。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

ソースファイルとソースパス、およびその他のソースファイルの読み込み方法の詳細については、「[ソースパス](source-path.md)」を参照してください。

 

 





