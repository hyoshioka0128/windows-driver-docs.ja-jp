---
title: INF ファイルからの情報の取得
description: INF ファイルからの情報の取得
ms.assetid: 4174357f-bca3-43b8-8ad6-331b9accd905
keywords:
- INF ファイル WDK デバイス インストールでは、情報の取得
- INF ファイルの情報を取得します。
- ステータス情報の WDK INF ファイル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e304467888391b5856db1f6717a439e9de470eb8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363321"
---
# <a name="retrieving-information-from-an-inf-file"></a>INF ファイルからの情報の取得





ハンドルを INF ファイルを作成したら、さまざまな方法でそこから情報を取得できます。 などの関数[ **SetupGetInfInformation**](https://msdn.microsoft.com/library/windows/desktop/aa377383)、 [ **SetupQueryInfFileInformation**](https://msdn.microsoft.com/library/windows/desktop/aa377416)、および[ **SetupQueryInfVersionInformation** ](https://msdn.microsoft.com/library/windows/desktop/aa377418)指定した INF ファイルに関する情報を取得します。

などの他の関数[ **SetupGetSourceInfo** ](https://msdn.microsoft.com/library/windows/desktop/aa377392)と[ **SetupGetTargetPath**](https://msdn.microsoft.com/library/windows/desktop/aa377394)、ソース ファイルに関する情報を取得し、ターゲット ディレクトリ。

などの関数[ **SetupGetLineText** ](https://msdn.microsoft.com/library/windows/desktop/aa377388)と[ **SetupGetStringField** ](https://msdn.microsoft.com/library/windows/desktop/aa377393)に格納されている情報に直接アクセスするため、行または INF ファイルのフィールド。 これらの関数は、高レベルによって内部的に使用[SetupAPI](setupapi.md)関数が、行またはフィールド レベルの情報に直接アクセスする必要がある場合に使用できます。

 

 





