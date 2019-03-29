---
title: UMDH ログの解釈
description: UMDH ログの解釈
ms.assetid: c5c74a3a-9598-4d89-8c5b-445138ae845f
keywords:
- UMDH、UMDH ログの解釈
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9bb576f15fd99bc8667b4b38c65a7a5cb674e8ea
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572043"
---
# <a name="interpreting-a-umdh-log"></a>UMDH ログの解釈


## <span id="ddk_interpreting_a_umdh_log_dtools"></span><span id="DDK_INTERPRETING_A_UMDH_LOG_DTOOLS"></span>


ユーザー モード ダンプ ヒープ (UMDH) ログ ファイルは、プロセスと、割り当てが行われたスタックでヒープ割り当ての一覧を表示します。

この例では、ログを 1204 の ID を持つプロセスを作成する方法を示します。 ログは、ファイル log1.txt に書き込まれます。

```console
umdh -p:1204 -f:log1.txt
```

シンボルは解決されませんので、ログ ファイルを読み取れません。 UMDH は、ログを分析するときに、シンボルを解決します。 この例では、log1.txt を分析し、result.txt で結果を格納する方法を示します。

```console
umdh -v log1.txt  > result.txt
```

## <a name="span-idsymbolfilesforanalyzingalogfilespanspan-idsymbolfilesforanalyzingalogfilespanspan-idsymbolfilesforanalyzingalogfilespansymbol-files-for-analyzing-a-log-file"></a><span id="Symbol_Files_for_Analyzing_a_Log_File"></span><span id="symbol_files_for_analyzing_a_log_file"></span><span id="SYMBOL_FILES_FOR_ANALYZING_A_LOG_FILE"></span>ログ ファイルの分析のシンボル ファイル


2 台のコンピューターがあるとします。、*コンピューターへのログオン*UMDH ログを作成すると、*分析コンピューター* UMDH ログを分析します。 分析のコンピューター上のシンボル パスは、ログが行われた時にログ記録のコンピューターに読み込まれている Windows のバージョンのシンボルを指す必要があります。 シンボル サーバーを分析コンピューターにシンボル パスを指していません。 場合は、UMDH は分析のコンピューターで実行されている Windows のバージョンのシンボルを取得し、UMDH に意味のある結果は表示されません。

 

 





