---
title: カーネルモード ダンプ ファイルの分析
description: カーネルモード ダンプ ファイルの分析
ms.assetid: 2bda51c2-b022-4740-8df9-5a2cf2382e3e
keywords:
- ダンプファイル、カーネルモードダンプファイルの分析
ms.date: 06/05/2020
ms.localizationpriority: medium
ms.openlocfilehash: d7c87329b9d90b24ed510d49814dfd2d11380942
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84533919"
---
# <a name="analyzing-a-kernel-mode-dump-file"></a>カーネルモード ダンプ ファイルの分析

ここでは、以下の内容について説明します。

[KD によるカーネルモード ダンプ ファイルの分析](analyzing-a-kernel-mode-dump-file-with-kd.md)

[WinDbg によるカーネルモード ダンプ ファイルの分析](analyzing-a-kernel-mode-dump-file-with-windbg.md)

### <a name="installing-symbol-files"></a>シンボルファイルのインストール

使用するツールに関係なく、ダンプファイルを生成したバージョンの Windows のシンボルファイルをインストールする必要があります。 これらのファイルは、ダンプファイルの分析に使用するように選択したデバッガーによって使用されます。 シンボルファイルの適切なインストールの詳細については、「 [Windows シンボルファイルのインストール](installing-windows-symbol-files.md)」を参照してください。

### <a name="dumpexam"></a>DumpExam

DumpExam ツールは互換性のために残されています。 クラッシュダンプファイルの分析では、これは不要になりました。
