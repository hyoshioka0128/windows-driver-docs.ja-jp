---
title: XPSDrv ドライバー オプション
description: XPSDrv ドライバー オプション
ms.assetid: 51db3cce-a95a-4084-9927-542c2d06312a
keywords:
- バージョン 3 XPS ドライバー WDK XPSDrv、オプション
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3262266b384cd4db9201604e90318157590d6c40
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390242"
---
# <a name="xpsdrv-driver-options"></a>XPSDrv ドライバー オプション


次のメソッドのいずれかを使用して、XPSDrv プリンター ドライバーの構成モジュールを実装できます。

<a href="" id="text-file-only-------"></a>**テキスト ファイルのみ**   
構成モジュールが GPD または PPD ファイルによって定義され、Undriv または PScript5 構成モジュールを使用して、すべての構成関数を実装します。 テキスト ファイルの唯一の方法は、開発時間が最も速いと開発コストが最も低いが、カスタマイズのサポートが限られています。 このメソッドは、XPSDrv パススルーまたは基本的な XPSDrv プリンター ドライバーに最適です。

<a href="" id="plug-in-------"></a>**プラグイン**   
構成のモジュールが GPD または PPD ファイルによって定義され、Unidrv または PScript5 の 1 つまたは複数の印刷ドライバーの構成にプラグインします。プラグインのメソッドには、他のすべての側面の Unidrv または PScript5 構成モジュールに依存しながら、構成の動作とユーザー エクスペリエンスの特定の側面をカスタマイズする柔軟ができます。 このメソッドに必要な開発時間は、印刷ドライバーに必要なカスタマイズの程度によって異なります。 このメソッドは、すべての種類のプリンター ドライバーに適しています。

このような 1 つプラグイン、Mxdwdui.dll、Microsoft が提供経由で Microsoft XPS ドキュメント コンバーター (MXDC) の構成を有効にする、 [IPrintOemUIMXDC COM インターフェイス](iprintoemuimxdc-com-interface.md)します。 MXDC は、XPS パッケージを生成するために、GDI ベースのアプリケーションからの出力を変換します。 この使用率、XPS ドライバーにすばやく機能を追加するプラグインの独自のプラグインと何ができるの例に示します。

<a href="" id="monolithic"></a>**モノリシック**  
完全に定義し、構成モジュールを実装します。 モノリシック メソッドは通常、最もコストのかかるメソッドすべての印刷ドライバーを実行する必要がありますので、開発とテストが、このメソッドは、カスタマイズの営業案件最大限も提供されます。

 

 




