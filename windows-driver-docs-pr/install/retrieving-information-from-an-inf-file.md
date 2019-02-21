---
title: INF ファイルから情報を取得します。
description: INF ファイルから情報を取得します。
ms.assetid: 4174357f-bca3-43b8-8ad6-331b9accd905
keywords:
- INF ファイル WDK デバイス インストールでは、情報の取得
- INF ファイルの情報を取得します。
- ステータス情報の WDK INF ファイル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e304467888391b5856db1f6717a439e9de470eb8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536014"
---
# <a name="retrieving-information-from-an-inf-file"></a>INF ファイルから情報を取得します。





ハンドルを INF ファイルを作成したら、さまざまな方法でそこから情報を取得できます。 などの関数[ **SetupGetInfInformation**](https://msdn.microsoft.com/library/windows/desktop/aa377383)、 [ **SetupQueryInfFileInformation**](https://msdn.microsoft.com/library/windows/desktop/aa377416)、および[ **SetupQueryInfVersionInformation** ](https://msdn.microsoft.com/library/windows/desktop/aa377418)指定した INF ファイルに関する情報を取得します。

などの他の関数[ **SetupGetSourceInfo** ](https://msdn.microsoft.com/library/windows/desktop/aa377392)と[ **SetupGetTargetPath**](https://msdn.microsoft.com/library/windows/desktop/aa377394)、ソース ファイルに関する情報を取得し、ターゲット ディレクトリ。

などの関数[ **SetupGetLineText** ](https://msdn.microsoft.com/library/windows/desktop/aa377388)と[ **SetupGetStringField** ](https://msdn.microsoft.com/library/windows/desktop/aa377393)に格納されている情報に直接アクセスするため、行または INF ファイルのフィールド。 これらの関数は、高レベルによって内部的に使用[SetupAPI](setupapi.md)関数が、行またはフィールド レベルの情報に直接アクセスする必要がある場合に使用できます。

 

 





