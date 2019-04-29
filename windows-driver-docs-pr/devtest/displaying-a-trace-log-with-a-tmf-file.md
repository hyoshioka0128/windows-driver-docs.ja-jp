---
title: TMF ファイルでのトレース ログの表示
description: TMF ファイルでのトレース ログの表示
ms.assetid: 1d592ed3-44d2-4d12-9d31-19b07e6962ea
keywords:
- トレース メッセージのフォーマット ファイル WDK
- TMF ファイル WDK、トレース ログを表示します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4dbfc7f30e1627885971841f3d0aed0652d45c75
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63329687"
---
# <a name="displaying-a-trace-log-with-a-tmf-file"></a>TMF ファイルでのトレース ログの表示


## <span id="ddk_using_a_tmf_file_tools"></span><span id="DDK_USING_A_TMF_FILE_TOOLS"></span>


ない場合、 [PDB シンボル ファイル](pdb-symbol-files.md)トレース プロバイダーのトレース ログの内容を表示する、次の手順を使用します。

1.  [Traceview で開始](starting-and-exiting-traceview.md)します。

2.  **ファイル** メニューのをクリックして**既存のログ ファイルを開く**します。

3.  **ログ ファイル名**ボックスに、イベント トレース ログ ファイル (.etl) の名前とパスを入力します。 または、省略記号ボタンをクリックします (**.**)、ファイルに移動します。

4.  **ログ ファイルの選択** ダイアログ ボックスで設定することも選択するその他の生成オプションは、ログ ファイルからファイルを出力します。 この手順は省略可能です。 詳細については、次を参照してください。[トレース ログ オプションの設定](setting-trace-log-options.md)します。

5.  **[OK]** をクリックします。

6.  クリックして**TMF (トレース形式) ファイル**順にクリックします**OK**します。

7.  次のいずれかの操作を行います。
    -   1 つまたは複数の TMF ファイルを指定するには、次のようにクリックします。 **TMF ファイルの選択**、 をクリック**ok**、 をクリック**追加**、を参照し、ディレクトリから 1 つ以上の TMF ファイルを選択します。 別のディレクトリから TMF ファイルを選択する をクリックして、**追加**もう一度ボタンをクリックします。 それ以外の場合、をクリックして**完了**します。
    -   Traceview で指定したディレクトリ内の TMF ファイルを検索するを指示するには、次のようにクリックします。 **TMF 検索パスの設定**、 をクリック**ok**で、ディレクトリを参照し、順にクリックします**OK**。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

TMF ファイルを指定する方法については、TMF ファイルの選択および TMF 検索パスの設定を参照してください。

 

 





