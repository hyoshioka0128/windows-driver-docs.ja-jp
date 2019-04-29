---
title: LogViewer ファイルのテキストへのエクスポート
description: LogViewer ファイルのテキストへのエクスポート
ms.assetid: b014dc23-ca6e-4563-aa8d-f4dd19c89f80
keywords:
- LogViewer、テキスト ファイルをエクスポートします。
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: fab8c7e2d24af8c73434d25cc3802995f6bbfa54
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332118"
---
# <a name="exporting-logviewer-files-to-text"></a>LogViewer ファイルのテキストへのエクスポート


## <span id="ddk_exporting_logviewer_files_to_text_dtoolq"></span><span id="DDK_EXPORTING_LOGVIEWER_FILES_TO_TEXT_DTOOLQ"></span>


ログ ファイルを操作する強力な方法は、テキストをそれらをエクスポートします。 これにより、任意のテキスト エディターの検索機能を使用して特定のパラメーター値を検索することができます。 ロガーから直接生成するテキスト ファイルのことはできますが、LogViewer を使用して、関数呼び出しをフィルター処理またはエイリアスを追加して、テキスト ファイルには、この情報をエクスポートしより柔軟になります。

.Lgv ファイルからテキスト ファイルを作成するには、LogViewer でファイルを開きを選び**ファイル |テキスト ファイルにエクスポート**します。 ダイアログ ボックスで、ファイル名と場所を選択します。

ダイアログ ボックスの下部にあるいくつかのオプションがあります。

<span id="Export_Diff_Information"></span><span id="export_diff_information"></span><span id="EXPORT_DIFF_INFORMATION"></span>**差分情報をエクスポートします。**  
このオプションは、すべてのポインター、ハンドル値、および実行から別の実行を変更する他の値では別名です。 LogViewer は、ポインター (たとえば、"0x00123FA2") の実際の値を出力ではなく「ポインターです」が出力されます。 同様に、ハンドルはエイリアスの"HeapHandle1"またはその他として登録できませんの値としてでは、 *diff*差分ツールを使用して 2 つのファイルを比較するとします。

<span id="Include_Non-Visible_Rows"></span><span id="include_non-visible_rows"></span><span id="INCLUDE_NON-VISIBLE_ROWS"></span>**非表示の行を含める**  
このオプションは、どのようなフィルターは、エクスポート中に、ビューに現在適用されて無効にします。

<span id="Create_a_Separate_File_For_Each_Thread"></span><span id="create_a_separate_file_for_each_thread"></span><span id="CREATE_A_SEPARATE_FILE_FOR_EACH_THREAD"></span>**スレッドごとに個別のファイルを作成します。**  
このオプションは、次の実行のスレッドをやすくするためのスレッドによってテキスト ファイルを分割します。 これは、2 つのインスタンスの実行"diff"にする場合に便利です。

<span id="Export_Range"></span><span id="export_range"></span><span id="EXPORT_RANGE"></span>**エクスポート範囲**  
このオプションは、エクスポートする行の範囲を指定します。

 

 





