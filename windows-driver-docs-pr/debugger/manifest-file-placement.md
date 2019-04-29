---
title: マニフェスト ファイルの配置
description: マニフェスト ファイルの配置
ms.assetid: ebf10463-3aa1-403a-8508-1462259a5f8a
keywords:
- LogViewer、マニフェスト、ファイルの配置
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 802c9a859f59f703e5addf1d832c58a759bbd544
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383302"
---
# <a name="manifest-file-placement"></a>マニフェスト ファイルの配置


## <span id="ddk_manifest_file_placement_dtoolq"></span><span id="DDK_MANIFEST_FILE_PLACEMENT_DTOOLQ"></span>


プライマリのマニフェスト ファイルは、Main.h という名前する必要があります。

ロガーが実行されている場合は、マニフェスト Logexts.dll を含むディレクトリのサブディレクトリに Main.h を置く必要があります。

LogViewer はロガーよりも柔軟です。 この順序で次のディレクトリに Main.h を検索します。

1.  Logviewer.exe を含むディレクトリに下位のマニフェストのディレクトリ

2.  WinExt\\logviewer.exe を含むディレクトリに下位のマニフェストのディレクトリ

3.  %Windir%\\System32\\マニフェスト ディレクトリ

4.  %Windir%\\システム\\マニフェスト ディレクトリ

追加のマニフェスト ファイルをすべては、Main.h と同じディレクトリ内に存在する必要があります。

 

 





