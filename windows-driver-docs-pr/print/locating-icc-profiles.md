---
title: ICC プロファイルを検索する
description: ICC プロファイルを検索する
ms.assetid: 828b53cd-452a-4c4d-bfbb-45ea674ef49a
keywords:
- WDK の印刷、ICC プロファイルの特定の色の管理
- ICC プロファイル WDK を印刷します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0be3f82b5dc2fe126696bd8262c881330206dea8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579268"
---
# <a name="locating-icc-profiles"></a>ICC プロファイルを検索する





色の管理を有効にすると、GDI の適切な ICC プロファイルを使用して検索、次の手順。

1.  場合、ドライバーの[プリンター インターフェイス DLL](printer-interface-dll.md)提供、 [ **DrvQueryColorProfile** ](https://msdn.microsoft.com/library/windows/hardware/ff548573)関数、GDI クライアントは、ドライバーを指定する機会を提供する関数を呼び出す、プロファイル。 関数には、プロファイルが返された場合に使用されます。

2.  場合**DrvQueryColorProfile**が存在しないか、プロファイルは返されません GDI が指定されたプリンターの種類のインストールされているプロファイルの色のディレクトリを検索します。 解像度、メディアの種類、および滑らかに一致する見つかった最初のプロファイルを使用する GDI DEVMODE 構造体で設定します。

3.  色のディレクトリに指定された DEVMODE 内容に一致する指定されたプリンターの種類のプロファイルが含まれていない場合、GDI は、システムの既定の sRGB プロファイルを使用します。

詳細については、[ICC プロファイルのインストール](installing-icc-profiles.md)を参照してください。 Microsoft Windows sdk で ICC プロファイルに関する追加情報が見つかります。

 

 




