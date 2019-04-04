---
title: カーネルモード ダンプ ファイルの分析
description: カーネルモード ダンプ ファイルの分析
ms.assetid: 2bda51c2-b022-4740-8df9-5a2cf2382e3e
keywords:
- ダンプ ファイル、カーネル モードのダンプ ファイルの分析
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2af1c6b4306b919504ec2aec70a5c1a9a28e03d6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571756"
---
# <a name="analyzing-a-kernel-mode-dump-file"></a>カーネルモード ダンプ ファイルの分析


## <span id="ddk_analyzing_a_kernel_mode_dump_file_dbg"></span><span id="DDK_ANALYZING_A_KERNEL_MODE_DUMP_FILE_DBG"></span>


このセクションの内容:

[KD とカーネル モードのダンプ ファイルの分析](analyzing-a-kernel-mode-dump-file-with-kd.md)

[WinDbg をカーネル モードのダンプ ファイルの分析](analyzing-a-kernel-mode-dump-file-with-windbg.md)

[KAnalyze とカーネル モードのダンプ ファイルの分析](analyzing-a-kernel-mode-dump-file-with-kanalyze.md)

### <a name="span-idinstallingsymbolfilesspanspan-idinstallingsymbolfilesspaninstalling-symbol-files"></a><span id="installing_symbol_files"></span><span id="INSTALLING_SYMBOL_FILES"></span>シンボル ファイルをインストールします。

どのツールを使用するのに関係なくダンプ ファイルを生成した Windows のバージョンのシンボル ファイルをインストールする必要があります。 これらのファイルは、ダンプ ファイルの分析に使用するデバッガーによって使用されます。 シンボル ファイルの適切なインストールの詳細については、[Windows シンボル ファイルのインストール](installing-windows-symbol-files.md)を参照してください。

### <a name="span-idddkdumpexamdbgspanspan-idddkdumpexamdbgspandumpexam"></a><span id="ddk_dumpexam_dbg"></span><span id="DDK_DUMPEXAM_DBG"></span>DumpExam

DumpExam ツールが廃止されています。 クラッシュ ダンプ ファイルの分析では必要なくなりました。

 

 





