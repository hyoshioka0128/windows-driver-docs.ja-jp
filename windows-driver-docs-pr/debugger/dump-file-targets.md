---
title: ダンプ ファイルのターゲット
description: ダンプ ファイルのターゲット
ms.assetid: 83fb6753-a6c1-4899-9b06-a6331b3c31a8
keywords:
- ダンプ ファイルのターゲット
- ダンプ ファイル
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: d124852715e4e2f85d410c6122477fbe1322dad9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560468"
---
# <a name="dump-file-targets"></a>ダンプ ファイルのターゲット


## <span id="ddk_dump_file_targets_dbx"></span><span id="DDK_DUMP_FILE_TARGETS_DBX"></span>


概要とクラッシュ ダンプ ファイルの概要については、[クラッシュ ダンプ ファイル](crash-dump-files.md)を参照してください。

### <a name="span-idopeningdumpfilesspanspan-idopeningdumpfilesspanspan-idopeningdumpfilesspanopening-dump-files"></a><span id="Opening_Dump_Files"></span><span id="opening_dump_files"></span><span id="OPENING_DUMP_FILES"></span>ダンプ ファイルを開く

デバッガーのターゲットとして使用するためのクラッシュ ダンプ ファイルを開くには、次のように使用します。 [ **OpenDumpFile** ](https://msdn.microsoft.com/library/windows/hardware/ff552322)または[ **OpenDumpfileWide**](https://msdn.microsoft.com/library/windows/hardware/ff552324)します。 これらのメソッドはのような[ **.opendump** ](-opendump--open-dump-file-.md)デバッガー コマンド。

**注**  までダンプ ファイルに、エンジンがアタッチが完全に、 [ **WaitForEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff561229)メソッドが呼び出されました。 プロセスまたはカーネルからダンプ ファイルが作成されると、最後のイベントに関する情報がダンプ ファイルに格納されます。 ダンプ ファイルが開かれた後に次の時間の実行が試行された、エンジンのイベントのコールバックには、このイベントが生成されます。 その後、ダンプ ファイルにはデバッグ セッションで使用できます。 参照してください[デバッグ セッションと実行モデル](debugging-session-and-execution-model.md)の詳細。

 

追加のファイルは、クラッシュ ダンプ ファイルのデバッグを支援するために使用できます。 メソッド[ **AddDumpInformationFile** ](https://msdn.microsoft.com/library/windows/hardware/ff537865)と[ **AddDumpInformationFileWide** ](https://msdn.microsoft.com/library/windows/hardware/ff537874)ページ ファイル情報を含むファイルを登録します。[次へ] のダンプ ファイルを開いたときに使用されます。 ダンプ ファイルが開かれる前に、これらのメソッドを呼び出す必要があります。 [**GetNumberDumpFiles** ](https://msdn.microsoft.com/library/windows/hardware/ff547887)は現在のダンプ ファイルが開かれたときに使用されたこのようなファイルの数を返しますと[ **GetDumpFile** ](https://msdn.microsoft.com/library/windows/hardware/ff546586)はこれらの説明を返しますファイル。

ユーザー モードのミニダンプ ファイルには、いくつかの情報の流れが含まれます。 使用してこれらのストリームを読み取ることができます、 [**要求**](https://msdn.microsoft.com/library/windows/hardware/ff554564)操作[**デバッグ\_要求\_読み取り\_ユーザー\_ミニダンプ\_ストリーム**](https://msdn.microsoft.com/library/windows/hardware/ff541575)します。

### <a name="span-idcreatingdumpfilesspanspan-idcreatingdumpfilesspanspan-idcreatingdumpfilesspancreating-dump-files"></a><span id="Creating_Dump_Files"></span><span id="creating_dump_files"></span><span id="CREATING_DUMP_FILES"></span>ダンプ ファイルを作成します。

現在のターゲット ユーザー モードまたはカーネル モードの使用のクラッシュ ダンプ ファイルを作成する[ **WriteDumpFile2**](https://msdn.microsoft.com/library/windows/hardware/ff561382)します。 このメソッドは、 [ **.dump** ](-dump--create-dump-file-.md)デバッガー コマンド。

 

 





