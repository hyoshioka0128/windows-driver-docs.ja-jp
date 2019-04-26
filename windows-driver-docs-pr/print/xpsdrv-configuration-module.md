---
title: XPSDrv 構成モジュール
description: XPSDrv 構成モジュール
ms.assetid: 439d7769-57d1-41f9-a3db-da254b4b7cae
keywords:
- XPSDrv プリンター ドライバー WDK、モジュールの構成
- 構成モジュール WDK XPSDrv、モジュールの構成について
- レンダリングの WDK XPSDrv 変換モジュール
- WDK XPSDrv 通知
- イベント通知 WDK XPSDrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 285383a33f7bccdabb724ed3818343456ccb4016
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354764"
---
# <a name="xpsdrv-configuration-module"></a>XPSDrv 構成モジュール


XPSDrv プリンター ドライバーは、XPS スプール ファイルを使用し、プリンターが使用できるページ記述言語 (PDL) データを出力する XPS 印刷パスのコンポーネントです。 構成のモジュールには、通信プリンターの機能とアプリケーションを設定するドライバー コンポーネントが含まれています。 XPSDrv プリンター ドライバーでは、Microsoft Win32 ベースのアプリケーションと Windows Presentation Foundation の WPF ベースのアプリケーションを使用する通信方法をサポートします。

Win32 ベースのアプリケーションと WPF アプリケーションの両方が XPSDrv プリンター ドライバーを印刷できます。 Win32 アプリケーションは、GDI 印刷アプリケーション プログラミング インターフェイス (API) を使用し、Microsoft が指定した変換のレンダリング モジュールが、印刷、印刷フィルター パイプラインに XPS スプール ファイルを作成します。 WPF アプリケーションでは、WPF の印刷 API を使用して、アプリケーションから直接 XPS スプール ファイルを作成します。

次の図は、XPSDrv 構成アーキテクチャを示します。

![xpsdrv 構成アーキテクチャを示す図](images/xpsconfig.png)

モジュールの構成セクションでは、3 つのオブジェクトが相互に排他的なことに注意してください。

XPSDrv プリンターのドライバーの 2 つの主要なコンポーネントは、[バージョン 3 の印刷ドライバー モジュール](version-3-xpsdrv-print-driver-components.md)と[XPS フィルター パイプライン](filter-pipeline-configuration-file.md)します。 これらの各コンポーネントには、構成ファイルとモジュールの 1 つ以上が必要です。

### <a name="xpsdrv-document-events"></a>XPSDrv ドキュメント イベント

XPSDrv ドライバーを通じて GDI ドキュメント イベントを受信できる、 [ **DrvDocumentEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff548544)関数には、印刷は Win32 ベースのアプリケーションとドライバーを XPS ドキュメントのイベントを受信できます。DrvDocumentEvent に WPF アプリケーションを印刷するとき。 XPSDrv ドキュメント イベントの詳細については、次を参照してください。 [XPSDrv ドライバーのドキュメント イベント](xps-driver-document-events.md)します。

### <a name="xpsdrv-driver-installation"></a>XPSDrv ドライバーのインストール

XPSDrv ドライバーでは、インストールの特定の要件があります。 XPSDrv ドライバーのインストールの詳細については、次を参照してください。 [XPSDrv インストール](xpsdrv-installation.md)します。

 

 




