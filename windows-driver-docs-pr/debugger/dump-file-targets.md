---
title: ダンプファイル ターゲット
description: ダンプファイル ターゲット
ms.assetid: 83fb6753-a6c1-4899-9b06-a6331b3c31a8
keywords:
- ターゲット、ダンプファイル
- ダンプファイル
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c9a3a49909ebbcca4a90aa3b37c7d88374fd940
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837764"
---
# <a name="dump-file-targets"></a>ダンプファイル ターゲット


## <span id="ddk_dump_file_targets_dbx"></span><span id="DDK_DUMP_FILE_TARGETS_DBX"></span>


クラッシュダンプファイルの概要と概要については、「[クラッシュダンプファイル](crash-dump-files.md)」を参照してください。

### <a name="span-idopening_dump_filesspanspan-idopening_dump_filesspanspan-idopening_dump_filesspanopening-dump-files"></a><span id="Opening_Dump_Files"></span><span id="opening_dump_files"></span><span id="OPENING_DUMP_FILES"></span>ダンプファイルを開く

デバッガーターゲットとして使用するためのクラッシュダンプファイルを開くには、 [**OpenDumpFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-opendumpfile)または[**OpenDumpfileWide**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-opendumpfilewide)を使用します。 これらのメソッドは、 [**opendump**](-opendump--open-dump-file-.md)デバッガーコマンドに似ています。

[**Waitforevent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-waitforevent)メソッドが呼び出されるまで、エンジンはダンプファイルに完全にアタッチされない   に**注意**してください。 プロセスまたはカーネルからダンプファイルが作成されると、最後のイベントに関する情報がダンプファイルに格納されます。 ダンプファイルを開くと、次に実行が試行されたときに、エンジンによってイベントコールバック用にこのイベントが生成されます。 その後、デバッグセッションでダンプファイルが使用できるようになります。 詳細については[、「デバッグセッションと実行モデル](debugging-session-and-execution-model.md)」を参照してください。

 

クラッシュダンプファイルのデバッグを支援するために、追加のファイルを使用できます。 [**Adddumpinformationfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-adddumpinformationfile)メソッドと[**Adddumpinformationfilewide**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-adddumpinformationfilewide)レジスタファイルは、次のダンプファイルを開いたときに使用されるページファイルの情報を含んでいます。 これらのメソッドは、ダンプファイルを開く前に呼び出す必要があります。 [**Getnumber Dumpfiles**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-getnumberdumpfiles)は、現在のダンプファイルを開いたときに使用されたファイルの数を返し、 [**GetDumpFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-getdumpfile)はこれらのファイルの説明を返します。

ユーザーモードのミニダンプファイルには、情報のストリームがいくつか含まれています。 これらのストリームは、[**要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugadvanced3-request)操作の[**デバッグ\_要求\_読み取り\_ユーザー\_ミニダンプ\_ストリーム**](https://docs.microsoft.com/previous-versions/ff541575(v=vs.85))で読み取ることができます。

### <a name="span-idcreating_dump_filesspanspan-idcreating_dump_filesspanspan-idcreating_dump_filesspancreating-dump-files"></a><span id="Creating_Dump_Files"></span><span id="creating_dump_files"></span><span id="CREATING_DUMP_FILES"></span>ダンプファイルの作成

現在のターゲット (ユーザーモードまたはカーネルモード) のクラッシュダンプファイルを作成するには、 [**WriteDumpFile2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-writedumpfile2)を使用します。 このメソッドは、 [ **.dump**](-dump--create-dump-file-.md) debugger コマンドに似ています。

 

 





