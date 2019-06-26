---
title: ICC プロファイルを検索する
description: ICC プロファイルを検索する
ms.assetid: 828b53cd-452a-4c4d-bfbb-45ea674ef49a
keywords:
- WDK の印刷、ICC プロファイルの特定の色の管理
- ICC プロファイル WDK を印刷します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2f8c54485eb06c6aaa2b80e740f87598fd1cff9b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353516"
---
# <a name="locating-icc-profiles"></a>ICC プロファイルを検索する





色の管理を有効にすると、GDI の適切な ICC プロファイルを使用して検索、次の手順。

1.  場合、ドライバーの[プリンター インターフェイス DLL](printer-interface-dll.md)提供、 [ **DrvQueryColorProfile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winddiui/nf-winddiui-drvquerycolorprofile)関数、GDI クライアントは、ドライバーを指定する機会を提供する関数を呼び出す、プロファイル。 関数には、プロファイルが返された場合に使用されます。

2.  場合**DrvQueryColorProfile**が存在しないか、プロファイルは返されません GDI が指定されたプリンターの種類のインストールされているプロファイルの色のディレクトリを検索します。 解像度、メディアの種類、および滑らかに一致する見つかった最初のプロファイルを使用する GDI DEVMODE 構造体で設定します。

3.  色のディレクトリに指定された DEVMODE 内容に一致する指定されたプリンターの種類のプロファイルが含まれていない場合、GDI は、システムの既定の sRGB プロファイルを使用します。

詳細については、次を参照してください。 [ICC プロファイルのインストール](installing-icc-profiles.md)します。 Microsoft Windows sdk で ICC プロファイルに関する追加情報が見つかります。

 

 




