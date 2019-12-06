---
title: 以前のバージョンの Windows の XPS サポート
description: 以前のバージョンの Windows の XPS サポート
ms.assetid: e13b43f5-e926-404d-9f76-c2dfef6e0637
keywords:
- XPSDrv プリンタードライバー WDK、以前のバージョンの Windows
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b291ac69a78f7e464b850f0b4fb4ef8004ba4b9a
ms.sourcegitcommit: 3ee05aabaf9c5e14af56ce5f1dde588c2c7eb4ec
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/06/2019
ms.locfileid: "74881920"
---
# <a name="xps-support-in-earlier-versions-of-windows"></a>以前のバージョンの Windows の XPS サポート

Windows Vista に加えて、XPS ベースのテクノロジは、microsoft WinFX Runtime Component 3.0 を通じて、Microsoft Windows Server 2003 および Windows XP でサポートされています。 XPS 印刷は、これらのオペレーティングシステムを使用したポイントアンドプリントシナリオで機能します。

Windows Server 2003 および Windows XP のサポートは、次の方法で提供されます。

- Win32 および Windows Presentation Foundation (WPF) アプリケーションの出力の透過的な変換。 レンダリングの出力は Win32 と Windows Presentation Foundation (WPF) アプリケーションによって大きく異なりますが、XPSDrv ドライバーモデルでは、両方のアプリケーションの種類が1つのドライバーに出力できるようになっています。 印刷用の出力は、アプリケーションの種類とドライバーの種類の間で適切に変換されます。これにより、GDI および XPS ベースのプリンターに出力する Win32 アプリケーションと WPF アプリケーションの完全なサポートマトリックスが有効になります。 XPSDrv インフラストラクチャは、Windows Server 2003 および Windows XP でも使用できます。

- 一貫したフィルターパイプラインモデル。 Windows Vista、Windows Server 2003、および Windows XP のフィルターパイプラインでは、フィルター、プラグインモデル、パイプライン構成ファイル、およびイベントログに対して同じインターフェイスがサポートされています。 以前のバージョンの Windows での通知のサポートが減少しているなど、いくつかの違いがあります。 Windows Vista では、表示フィルターは通知を完全に制御し、フィルターが処理しているあらゆる種類の "パーツ" (ドキュメント、ページ、フォント、画像など) に関する通知を送信できます。 以前のバージョンの Windows でのスケーラブルなコンシューマーの場合、通知はページの境界でのみ行われます。

- XPS ベースのプリントプロセッサ。 Windows Server 2003 および Windows XP では、XPSDrv を有効にする XPS ベースのプリントプロセッサが用意されています。 XPS ベースのプリントプロセッサは、XPSDrv ドライバーをホストし、これらのオペレーティングシステムの既存のスプーラと通信します。 特定の XPS 印刷パス機能は Windows Vista でのみ使用できます。そのため、以前のバージョンの Windows では、XPSDrv ドライバーが適切に機能しなくなる必要があります。

XPS の詳細については、 [「XML Paper Specification の概要」](https://download.microsoft.com/download/1/6/a/16acc601-1b7a-42ad-8d4e-4f0aa156ec3e/XPS_1_0.exe)をダウンロードしてください。
