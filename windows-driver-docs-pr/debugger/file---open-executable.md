---
title: ファイルの開いている実行可能ファイル
description: ファイルの開いている実行可能ファイル
ms.assetid: dee75298-903d-438f-a66e-fddcfcd74ec7
keywords:
- ファイルの開いている実行可能ファイル
- ファイルの開いている実行可能ファイル、デバッガーの開始
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8be1c3c6bc727afb107cedbbefbce7648a949d67
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581685"
---
# <a name="file--open-executable"></a>File | Open Executable (ファイル | 実行可能ファイルを開く)


## <span id="ddk_file_open_executable_dbg"></span><span id="DDK_FILE_OPEN_EXECUTABLE_DBG"></span>


をクリックして**実行可能ファイルのオープン**上、**ファイル**] メニューの [新しいユーザー モード プロセスを開始し、デバッグします。

このコマンドは、CTRL + E キーを押すと同じです。 このコマンドは、WinDbg が休止モードである場合にのみ使用できます。

### <a name="span-iddialogboxspanspan-iddialogboxspandialog-box"></a><span id="dialog_box"></span><span id="DIALOG_BOX"></span>ダイアログ ボックス

クリックすると**開いて実行可能ファイル**、**開いて実行可能ファイル** ダイアログ ボックスが表示され、次を行うことができます。

-   実行可能ファイルの完全なパスを入力、**ファイル名**ボックス。 またはを検索して、適切なファイルを選択 ダイアログ ボックスを使用することができます。 実行可能ファイルの正確なパスを指定する必要があります。 Microsoft Windows とは異なり**実行** ダイアログ ボックスと、コマンド プロンプト ウィンドウを**開いて実行可能** ダイアログ ボックスでは、実行可能ファイル名の現在のパスを検索しません。

-   実行可能ファイルを使用してコマンドライン引数を使用する場合は、それらを入力します。、**引数**ボックス。

-   既定のディレクトリから開始ディレクトリを変更する場合でのディレクトリ パスを入力、**開始ディレクトリ**ボックス。

-   WinDbg をいずれかにアタッチする場合*子プロセス*(追加のプロセス、元のターゲット プロセスを開始した) 選択**も子プロセスのデバッグ**します。

選択した後に、クリックして**オープン**します。

**注**  に、そのファイルへのパスを自動的に追加ソース ファイルを開きます次のコマンドを使用する場合、[ソース パス](source-path.md)します。

 

WinDbg がプロセス サーバーに接続されている場合は使用できません、**実行可能ファイルのオープン**コマンド。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

およびその他のデバッグ用の新しいプロセスの開始方法の詳細についてを参照してください。[デバッグ ユーザー モード プロセスを使用して WinDbg](debugging-a-user-mode-process-using-windbg.md)します。

 

 





