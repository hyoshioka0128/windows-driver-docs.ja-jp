---
title: ファイルは、プロセスにアタッチします。
description: ファイルは、プロセスにアタッチします。
ms.assetid: 6bd438a3-e9fb-444d-baf6-fffdee0487f2
keywords:
- ファイルは、プロセスにアタッチします。
- ファイルは、プロセスにアタッチ、デバッガーの開始
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: e44f12c5dd1d79fc7133e02c29ef4e0f844e96ea
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548581"
---
# <a name="file--attach-to-a-process"></a>ファイル |プロセスにアタッチします。


## <span id="ddk_file_attach_to_a_process_dbg"></span><span id="DDK_FILE_ATTACH_TO_A_PROCESS_DBG"></span>


をクリックして**プロセスにアタッチする**上、**ファイル**現在実行中のユーザー モード アプリケーションをデバッグするメニュー。

このコマンドは、F6 キーを押すと同じです。 このコマンドは、WinDbg が休止モードである場合にのみ使用できます。

### <a name="span-iddialogboxspanspan-iddialogboxspandialog-box"></a><span id="dialog_box"></span><span id="DIALOG_BOX"></span>ダイアログ ボックス

クリックすると**プロセスにアタッチする**、**プロセスにアタッチ** ダイアログ ボックスが表示され、次を行うことができます。

- 適切なプロセス ID と名前を含む行を選択します (プロセス ID を入力します。 または、**プロセス ID**ボックス)。
    **注**  表示されている各プロセスが、関連付けられているプラス記号 (**+**)。 そのプロセスのコマンドライン、サービス、および子プロセスに関する情報を表示、プラス記号をクリックすることができます。

    **注**   WinDbg の場合は、プロセス サーバーに接続されている、**プロセスにアタッチ**ダイアログ ボックスは、リモート コンピューターで実行されているプロセスに表示されます。 プロセス サーバーの詳細については、次を参照してください。 [**スマート クライアントのアクティブ化**](activating-a-smart-client.md)します。

- Noninvasively プロセスにアタッチする場合は、選択、 **Noninvasive**チェック ボックスをオンします。

選択を行ったら、**[OK]** をクリックします。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

およびその他のプロセスにアタッチの方法の詳細についてを参照してください。[デバッグ ユーザー モード プロセスを使用して WinDbg](debugging-a-user-mode-process-using-windbg.md)と[待合室 (ユーザー モード) のデバッグ](noninvasive-debugging--user-mode-.md)します。

 

 





