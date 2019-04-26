---
title: LogViewer 関数一覧のフィルター処理
description: LogViewer 関数一覧のフィルター処理
ms.assetid: 258da8c3-ab94-40bd-bfa5-344571d34428
keywords:
- LogViewer、LogViewer 関数の一覧をフィルター処理
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: ebe5fa697b9c32a7211140cd41d221807d55df3d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348455"
---
# <a name="filtering-the-logviewer-function-list"></a>LogViewer 関数一覧のフィルター処理


## <span id="ddk_filtering_the_logviewer_function_list_dtoolq"></span><span id="DDK_FILTERING_THE_LOGVIEWER_FUNCTION_LIST_DTOOLQ"></span>


ロガーは、通常、分析に不要な一部の関数呼び出しをキャプチャします。 これら除外できますロガーによってログ ファイルの作成時にします。 ただし、ため、通常は、ログに記録し、LogViewer の表示をフィルターするすべての関数を許可することをお勧めこのプロセスは元に戻すことが、できません。

LogViewer で関数呼び出しを除外するためのいくつかの方法はあります。

-   メイン表示領域でをクリックするか、カーソル キーを使用して関数を選択します。 (関数を選択すると、LogViewer について概説が赤でします。)クリックし、キーを押して、DEL キーまたは右クリックして選択**を非表示に**します。 これは、ビューからその関数呼び出しのすべてのインスタンスを非表示になります。

-   選択**ビュー |Api の表示**します。 3 つの領域を持つダイアログ ボックスが表示されます。 右側には、すべての関数のアルファベット順の一覧と、左側はカテゴリ別のグループ化します。 有効にしたり、その名前の左側にあるボックスをオフにして、任意の関数の表示を無効にできます。

-   選択**ビュー |モジュールの表示**します。 ダイアログ ボックスが表示されます。 呼び出し元のモジュールを選択できるようにします。これらのモジュールから呼び出された関数のみが表示されます。

-   選択**ビュー |最初の呼び出しのステージだけ**です。 これにより、左の列に"d0"がある呼び出しのみが表示されます。 多くの場合、ログに記録された他の関数で行われる関数呼び出しを非表示にする必要があります。 (など、通常は必要ないということを認識**ShellExecuteEx** 30 の異なるレジストリ呼び出しは、実行の過程です)。

 

 





