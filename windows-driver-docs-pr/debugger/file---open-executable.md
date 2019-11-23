---
title: ファイルオープン実行可能ファイル
description: ファイルオープン実行可能ファイル
ms.assetid: dee75298-903d-438f-a66e-fddcfcd74ec7
keywords:
- ファイルオープン実行可能ファイル
- デバッガーを開始しています。ファイルオープン実行可能ファイル
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8be1c3c6bc727afb107cedbbefbce7648a949d67
ms.sourcegitcommit: dff3834724bd5204c4a47204540fe8125dd37b20
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/06/2019
ms.locfileid: "70750017"
---
# <a name="file--open-executable"></a>File | Open Executable (ファイル | 実行可能ファイルを開く)


## <span id="ddk_file_open_executable_dbg"></span><span id="DDK_FILE_OPEN_EXECUTABLE_DBG"></span>


**[ファイル]** メニューの **[実行可能]** ファイルを開く をクリックして、新しいユーザーモードプロセスを開始し、デバッグします。

このコマンドは、CTRL キーを押しながら E キーを押すことに相当します。 このコマンドは、WinDbg が休止モードの場合にのみ使用できます。

### <a name="span-iddialog_boxspanspan-iddialog_boxspandialog-box"></a><span id="dialog_box"></span><span id="DIALOG_BOX"></span>ダイアログボックス

**[実行可能ファイルを開く]** をクリックすると、 **[実行可能ファイルを開く]** ダイアログボックスが表示され、次の操作を実行できます。

-   **[ファイル名]** ボックスに、実行可能ファイルの完全なパスを入力します。 または、ダイアログボックスを使用して、適切なファイルを探して選択することもできます。 実行可能ファイルの正確なパスを指定する必要があります。 Microsoft Windows の **[実行]** ダイアログボックスおよびコマンドプロンプトウィンドウとは異なり、 **[実行可能ファイルを開く]** ダイアログボックスでは、現在のパスで実行可能ファイル名が検索されません。

-   実行可能ファイルでコマンドライン引数を使用する場合は、 **[引数]** ボックスに入力します。

-   既定のディレクトリから開始ディレクトリを変更する場合は、[ディレクトリの**開始**] ボックスにディレクトリパスを入力します。

-   WinDbg を任意の*子プロセス*(元のターゲットプロセスが開始した追加プロセス) にアタッチする場合は、[**子プロセスのデバッグ] も**選択します。

選択が完了したら、 **[開く]** をクリックします。

**注**   このコマンドを使用してソースファイルを開くと、そのファイルへのパスが自動的に[ソースパス](source-path.md)に追加されます。

 

WinDbg がプロセスサーバーに接続されている場合は、 **[実行可能ファイルを開く]** コマンドを使用することはできません。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

デバッグのために新しいプロセスを開始するための詳細およびその他の方法については、「 [WinDbg を使用したユーザーモードプロセスのデバッグ](debugging-a-user-mode-process-using-windbg.md)」を参照してください。

 

 





