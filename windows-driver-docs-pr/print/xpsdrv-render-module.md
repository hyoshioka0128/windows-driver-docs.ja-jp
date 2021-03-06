---
title: XPSDrv レンダー モジュール
description: XPSDrv レンダー モジュール
ms.assetid: e844e320-bd3d-4855-bb47-fdfbdb157802
keywords:
- XPSDrv プリンター ドライバー WDK、モジュールを表示します。
- モジュール WDK XPSDrv、レンダリングのモジュールについての表示します。
- フィルター パイプラインを WDK XPSDrv
- フィルター パイプライン マネージャー WDK XPSDrv
- FPM WDK XPSDrv
- 間 Communicator WDK XPSDrv をフィルター処理します。
- IFC WDK XPSDrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: caa259f3d7463f3336fb321b2a47b52d4a3bd561
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390230"
---
# <a name="xpsdrv-render-module"></a>XPSDrv レンダー モジュール


XPSDrv プリンター ドライバーのレンダリングのモジュールには、プリンターに出力の XPS スプール ファイルの内容を表示するフィルターが含まれています。 ドライバーの表示フィルターのセットがインスタンス化され、フィルター パイプラインで実行します。 フィルター パイプライン Manager (FPM) は、フィルターを管理し、フィルター間 Communicator (IFC) は、フィルター間の相互作用を制御します。

次の図は、フィルター パイプラインを示します。

![フィルター パイプラインを示す図](images/xps-pipeline.png)

マイクロソフトでは、次の XPS ドライバー コンポーネントを提供します。

-   フィルタ パイプライン マネージャ

-   Communicator の間のフィルター

-   プロパティ バッグ

フィルター パイプライン マネージャーである必要があります。

1.  読み込みおよびフィルターを初期化します。

2.  フィルターの間でデータを管理します。

3.  印刷ジョブが完了すると、フィルターをアンロードします。

間フィルター送信者と受信者のフィルター間のデータ転送を管理し、フィルター パイプライン マネージャーがフィルターの間のコミュニケーターを管理します。

次のプロセスでは、パイプライン内のフィルターのセットに点について説明します。

1.  フィルター パイプライン マネージャーでは、フィルター パイプラインの構成 (FPC) ファイルを読み取ります。

2.  FPC を指定するフィルターが読み込まれます。

3.  フィルター パイプラインを初期化し、フィルター パイプライン マネージャーが、フィルター パイプラインを開始します。

4.  パイプラインの最初のフィルターは、フィルター パイプライン マネージャーが提供する XPS またはストリーム インターフェイスを使用して XPS データを読み取って、内容をフィルター処理します。

5.  最初のフィルターは、間フィルター Communicator を提供するインターフェイスを使用して、2 番目のフィルターに処理された XPS データを送信します。

6.  間フィルター Communicator は、2 番目のフィルターが準備できるまでに、中間処理の結果を保持します。

7.  手順 1. ~ 6. は最後のフィルターの結果が出力に対して、ドライバーが定義されているポートに送信されるまで、フィルターから繰り返されます。

プリンターは、ページ記述言語 (PDL) として XPS を使用するその他の処理が必要ない場合、空 (「パススルー」) のパイプラインを使用することができます。 XPS がプリンターの PDL でない場合は、XPS を他の処理と同様に、プリンターの PDL に変換するフィルターを記述する必要があります。

XPS ドライバーを開発するには、次のコンポーネントを作成する必要があります。

-   [XPS フィルター](xps-filters.md)

-   [XPS フィルター パイプライン構成ファイル](filter-pipeline-configuration-file.md)

追加することも[XPSDrv レンダリング モジュールに印刷チケットのサポート](print-ticket-support-in-the-xpsdrv-render-module.md)

 

 




