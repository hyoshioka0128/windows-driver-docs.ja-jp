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
ms.openlocfilehash: 450bc5bc7cc5a7c02918c42a745def6afde25d95
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382285"
---
# <a name="retrieving-information-from-an-inf-file"></a>INF ファイルからの情報の取得





ハンドルを INF ファイルを作成したら、さまざまな方法でそこから情報を取得できます。 などの関数[ **SetupGetInfInformation**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupgetinfinformationa)、 [ **SetupQueryInfFileInformation**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupqueryinffileinformationa)、および[ **SetupQueryInfVersionInformation** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupqueryinfversioninformationa)指定した INF ファイルに関する情報を取得します。

などの他の関数[ **SetupGetSourceInfo** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupgetsourceinfoa)と[ **SetupGetTargetPath**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupgettargetpatha)、ソース ファイルに関する情報を取得し、ターゲット ディレクトリ。

などの関数[ **SetupGetLineText** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupgetlinetexta)と[ **SetupGetStringField** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupgetstringfielda)に格納されている情報に直接アクセスするため、行または INF ファイルのフィールド。 これらの関数は、高レベルによって内部的に使用[SetupAPI](setupapi.md)関数が、行またはフィールド レベルの情報に直接アクセスする必要がある場合に使用できます。

 

 





