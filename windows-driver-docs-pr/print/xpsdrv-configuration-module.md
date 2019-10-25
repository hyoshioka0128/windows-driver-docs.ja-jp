---
title: XPSDrv 構成モジュール
description: XPSDrv 構成モジュール
ms.assetid: 439d7769-57d1-41f9-a3db-da254b4b7cae
keywords:
- XPSDrv プリンタードライバー WDK、構成モジュール
- 構成モジュール WDK XPSDrv、構成モジュールについて
- 変換レンダリングモジュール WDK XPSDrv
- 通知 WDK XPSDrv
- イベント通知 WDK XPSDrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 155824e4efc84d70618913f4470c63769d52cb76
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826979"
---
# <a name="xpsdrv-configuration-module"></a>XPSDrv 構成モジュール


XPSDrv 印刷ドライバーは、xps スプールファイルを使用し、プリンターが使用できるページ記述言語 (PDL) データを出力する XPS 印刷パスのコンポーネントです。 構成モジュールには、プリンターの機能と設定をアプリケーションに伝えるドライバーコンポーネントが含まれています。 XPSDrv プリンタードライバーは、Microsoft Win32 ベースのアプリケーションおよび Windows Presentation Foundation (WPF) ベースのアプリケーションが使用する通信方法をサポートしています。

Win32 ベースのアプリケーションと WPF アプリケーションはどちらも、XPSDrv 印刷ドライバーに出力できます。 Win32 アプリケーションは GDI 印刷アプリケーションプログラミングインターフェイス (API) を使用し、Microsoft が提供する変換レンダリングモジュールは、印刷フィルターパイプラインに印刷するための XPS スプールファイルを作成します。 WPF アプリケーションは、WPF 印刷 API を使用して、アプリケーションから直接 XPS スプールファイルを作成します。

次の図は、XPSDrv 構成アーキテクチャを示しています。

![xpsdrv 構成アーキテクチャを示す図](images/xpsconfig.png)

構成モジュールセクションの3つのオブジェクトは相互に排他的であることに注意してください。

XPSDrv 印刷ドライバーの2つの主要なコンポーネントは、[バージョン3の印刷ドライバーモジュール](version-3-xpsdrv-print-driver-components.md)と[XPS フィルターパイプライン](filter-pipeline-configuration-file.md)です。 これらの各コンポーネントには、1つまたは複数の構成ファイルとモジュールが必要です。

### <a name="xpsdrv-document-events"></a>XPSDrv ドキュメントイベント

XPSDrv ドライバーは、Win32 ベースのアプリケーションがそれに対して出力を行うときに、 [**DrvDocumentEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvdocumentevent)関数を介して GDI ドキュメントイベントを受け取ることができます。また、WPF アプリケーションがに出力されるときに、ドライバーは DrvDocumentEvent を使用して XPS ドキュメントイベントを受け取ることができます。もらう. XPSDrv document イベントの詳細については、「 [XPSDrv Driver Document events](xps-driver-document-events.md)」を参照してください。

### <a name="xpsdrv-driver-installation"></a>XPSDrv ドライバーのインストール

XPSDrv ドライバーには、インストールに関する特定の要件があります。 XPSDrv ドライバーのインストールの詳細については、「 [XPSDrv のインストール](xpsdrv-installation.md)」を参照してください。

 

 




