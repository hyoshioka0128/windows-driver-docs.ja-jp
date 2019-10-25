---
title: ICC プロファイルを検索する
description: ICC プロファイルを検索する
ms.assetid: 828b53cd-452a-4c4d-bfbb-45ea674ef49a
keywords:
- カラー管理 WDK 印刷、ICC プロファイルの検索
- ICC プロファイル WDK 印刷
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 12a2db1c7dcc4e29b07ba9668c14df136a0cdbe4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842618"
---
# <a name="locating-icc-profiles"></a>ICC プロファイルを検索する





色の管理が有効になっている場合、GDI は次の手順を使用して適切な ICC プロファイルを検索します。

1.  ドライバーの[printer INTERFACE DLL](printer-interface-dll.md)で[**DrvQueryColorProfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvquerycolorprofile)関数が提供されている場合、GDI クライアントは関数を呼び出して、プロファイルを指定する機会をドライバーに与えます。 関数からプロファイルが返された場合は、それが使用されます。

2.  **DrvQueryColorProfile**が存在しない場合、またはプロファイルを返さない場合、GDI は、指定されたプリンターの種類に対してインストールされているプロファイルのカラーディレクトリを検索します。 GDI は、DEVMODE 構造体の解決、メディアの種類、およびディザリングの設定に一致する最初に検出されたプロファイルを使用します。

3.  指定した種類の DEVMODE コンテンツと一致する指定したプリンターの種類のプロファイルがカラーディレクトリに含まれていない場合、GDI はシステムの既定の sRGB プロファイルを使用します。

詳細については、「 [ICC プロファイルのインストール](installing-icc-profiles.md)」を参照してください。 ICC プロファイルに関する追加情報については、Microsoft Windows SDK のドキュメントを参照してください。

 

 




