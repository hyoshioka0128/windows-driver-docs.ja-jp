---
title: UMDH ログの分析
description: 説明されている構文を使用して UMDH を実行して作成されたユーザー モード ダンプ ヒープ (UMDH) ログを分析するには、次のコマンドの使用は、実行中のプロセスを分析します。
ms.assetid: 66e559b2-0335-4a1d-ba6c-dde6b826dc5f
keywords:
- デバッグ UMDH ログの Windows を分析します。
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- Analyze UMDH Logs
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3300e26ed433a558d2590c973d67501bf4276731
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572449"
---
# <a name="analyze-umdh-logs"></a>UMDH ログの分析


次のコマンドを使用して、説明する構文と UMDH を実行して作成されたユーザー モード ダンプ ヒープ (UMDH) のログ分析[**実行中のプロセスを分析**](analyze-a-running-process.md)します。 この分析は、スタック トレースではなく、割り当てについて説明します。

単一のログ ファイルを分析したり、さまざまな実行時間の経過と共に、プログラムまたはドライバーのメモリ ダンプの割り当ての変更を検出するためにログを比較できます。

```dbgcmd
umdh [-d] [-v] [-l] File1 [File2] [-h | ?]
```

## <a name="span-idddkanalyzeumdhlogsdtoolsspanspan-idddkanalyzeumdhlogsdtoolsspanparameters"></a><span id="ddk_analyze_umdh_logs_dtools"></span><span id="DDK_ANALYZE_UMDH_LOGS_DTOOLS"></span>パラメーター


<span id="_______-d______"></span><span id="_______-D______"></span> **-d**   
10 進数で数値データを表示します。 既定では 16 進数です。

<span id="_______-v______"></span><span id="_______-V______"></span> **-v**   
詳細モード。 トレースと概要情報が含まれています。 トレースは、単一のログ ファイルを分析するときに最も役立ちます。

<span id="_______-l______"></span><span id="_______-L______"></span> **-l**   
ログには、ファイル名や行番号が含まれています。 (なお、パラメーターを小文字の"L"、番号 1 ではありません。)

<span id="_______File1__File2_"></span><span id="_______file1__file2_"></span><span id="_______FILE1__FILE2_"></span> *File1* \[*File2*\]  
分析する UMDH ログ ファイルを指定します。

UMDH がで実行すると、ログ ファイルを作成、 [**実行中のプロセスを分析**](analyze-a-running-process.md)モード、テキスト ファイルにログの内容を保存し、(**-f**)。

1 つのログ ファイルを指定すると、ファイルと割り当てられたバイト数の降順で各トレース内の関数呼び出しが表示されます UMDH を分析します。

2 つのログ ファイルを指定すると、UMDH はファイルを比較し、降順での割り当てが 2 つの試用版の間のほとんどに拡大関数呼び出しを表示します。

<span id="_______-h____"></span><span id="_______-H____"></span> **-h | ?**  
ヘルプを表示します。

### <a name="span-idsampleusagespanspan-idsampleusagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>サンプルの使用法

```dbgcmd
umdh dump.txt
umdh -d -v dump.txt
umdh dump1.txt dump2.txt
```

<a name="remarks"></a>コメント
-------

2 台のコンピューターがあるとします。、*コンピューターへのログオン*UMDH ログを作成すると、*分析コンピューター* UMDH ログを分析します。 分析のコンピューター上のシンボル パスは、ログが行われた時にログ記録のコンピューターに読み込まれている Windows のバージョンのシンボルを指す必要があります。 シンボル サーバーを分析コンピューターにシンボル パスを指していません。 場合は、UMDH は分析のコンピューターで実行されている Windows のバージョンのシンボルを取得し、UMDH に意味のある結果は表示されません。

 

 





