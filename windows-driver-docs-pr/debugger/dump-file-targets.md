---
title: ダンプファイル ターゲット
description: ダンプファイル ターゲット
ms.assetid: 83fb6753-a6c1-4899-9b06-a6331b3c31a8
keywords:
- ダンプ ファイルのターゲット
- ダンプ ファイル
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 95d96f7a7548c5396c1180576cdd7c7f9b9af7a3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361393"
---
# <a name="dump-file-targets"></a>ダンプファイル ターゲット


## <span id="ddk_dump_file_targets_dbx"></span><span id="DDK_DUMP_FILE_TARGETS_DBX"></span>


概要とクラッシュ ダンプ ファイルの概要については、次を参照してください。[クラッシュ ダンプ ファイル](crash-dump-files.md)します。

### <a name="span-idopeningdumpfilesspanspan-idopeningdumpfilesspanspan-idopeningdumpfilesspanopening-dump-files"></a><span id="Opening_Dump_Files"></span><span id="opening_dump_files"></span><span id="OPENING_DUMP_FILES"></span>ダンプ ファイルを開く

デバッガーのターゲットとして使用するためのクラッシュ ダンプ ファイルを開くには、次のように使用します。 [ **OpenDumpFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-opendumpfile)または[ **OpenDumpfileWide**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-opendumpfilewide)します。 これらのメソッドはのような[ **.opendump** ](-opendump--open-dump-file-.md)デバッガー コマンド。

**注**  までダンプ ファイルに、エンジンがアタッチが完全に、 [ **WaitForEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-waitforevent)メソッドが呼び出されました。 プロセスまたはカーネルからダンプ ファイルが作成されると、最後のイベントに関する情報がダンプ ファイルに格納されます。 ダンプ ファイルが開かれた後に次の時間の実行が試行された、エンジンのイベントのコールバックには、このイベントが生成されます。 その後、ダンプ ファイルにはデバッグ セッションで使用できます。 参照してください[デバッグ セッションと実行モデル](debugging-session-and-execution-model.md)の詳細。

 

追加のファイルは、クラッシュ ダンプ ファイルのデバッグを支援するために使用できます。 メソッド[ **AddDumpInformationFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-adddumpinformationfile)と[ **AddDumpInformationFileWide** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-adddumpinformationfilewide)ページ ファイル情報を含むファイルを登録します。[次へ] のダンプ ファイルを開いたときに使用されます。 ダンプ ファイルが開かれる前に、これらのメソッドを呼び出す必要があります。 [**GetNumberDumpFiles** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-getnumberdumpfiles)は現在のダンプ ファイルが開かれたときに使用されたこのようなファイルの数を返しますと[ **GetDumpFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-getdumpfile)はこれらの説明を返しますファイル。

ユーザー モードのミニダンプ ファイルには、いくつかの情報の流れが含まれます。 使用してこれらのストリームを読み取ることができます、 [**要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugadvanced3-request)操作[**デバッグ\_要求\_読み取り\_ユーザー\_ミニダンプ\_ストリーム**](https://docs.microsoft.com/previous-versions/ff541575(v=vs.85))します。

### <a name="span-idcreatingdumpfilesspanspan-idcreatingdumpfilesspanspan-idcreatingdumpfilesspancreating-dump-files"></a><span id="Creating_Dump_Files"></span><span id="creating_dump_files"></span><span id="CREATING_DUMP_FILES"></span>ダンプ ファイルを作成します。

現在のターゲット ユーザー モードまたはカーネル モードの使用のクラッシュ ダンプ ファイルを作成する[ **WriteDumpFile2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-writedumpfile2)します。 このメソッドは、 [ **.dump** ](-dump--create-dump-file-.md)デバッガー コマンド。

 

 





