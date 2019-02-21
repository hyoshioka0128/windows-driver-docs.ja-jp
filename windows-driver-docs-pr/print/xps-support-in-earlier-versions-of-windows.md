---
title: 以前のバージョンの Windows での XPS のサポート
description: 以前のバージョンの Windows での XPS のサポート
ms.assetid: e13b43f5-e926-404d-9f76-c2dfef6e0637
keywords:
- XPSDrv プリンター ドライバー WDK、Windows の以前のバージョン
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f4a85f89a820de51e585083c821a048df876f0f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528116"
---
# <a name="xps-support-in-earlier-versions-of-windows"></a>以前のバージョンの Windows での XPS のサポート


Windows Vista では、だけでなく、XPS ベースのテクノロジは、Microsoft Windows Server 2003 および Windows XP、Microsoft WinFX Runtime コンポーネント 3.0 でサポートされます。 XPS 印刷時点で作業をこれらのオペレーティング システムのシナリオを印刷します。

Windows Server 2003 および Windows XP のサポートは、次のように提供されます。

-   Win32、Windows Presentation Foundation (WPF) アプリケーションの出力の透過的な変換です。 表示出力は、Win32、Windows Presentation Foundation (WPF) アプリケーション間で大幅に異なる場合は、XPSDrv ドライバー モデルでは、両方を 1 つのドライバーを印刷するアプリケーションの種類を有効します。 印刷用の出力は、アプリケーションの種類と、GDI および XPS ベースのプリンターに印刷する Win32 と WPF のアプリケーション間で完全にサポート マトリックスを有効にすると、ドライバーの型の間で適切に変換されます。 XPSDrv インフラストラクチャも Windows Server 2003 および Windows XP で使用するために使用できます。

-   一貫性のあるフィルター パイプライン モデル。 フィルターは、Windows Vista、Windows Server 2003、および Windows XP のサポートのフィルター、プラグイン モデル、パイプラインの構成ファイル、およびイベントのログ記録と同じインターフェイスをパイプラインします。 以前のバージョンの Windows で通知の減少のサポートを含む、いくつかの違いがあります。 表示フィルター、Windows Vista の通知の完全な制御し、は、フィルター処理「部分」の任意の型に関する通知を送信することができます (つまり、ドキュメント、ページ、フォント、イメージ、およびなど)。 以前のバージョンの Windows で拡張性の高いコンシューマーは、通知はページの境界でのみ発生します。

-   XPS ベースのプリント プロセッサ。 Windows Server 2003 と Windows XP、XPS ベース プリント プロセッサが XPSDrv をできるようにします。 XPS ベースのプリント プロセッサは、XPSDrv ドライバーをホストし、これらのオペレーティング システム上の既存のスプーラーと通信します。 XPS 印刷パスの特定の機能は、XPSDrv ドライバーが Windows の以前のバージョンで適切に低下できる必要がありますので、Windows Vista でのみ使用できます。

XPS の詳細については、ダウンロード、 [XML 仕様概要](http://download.microsoft.com/download/1/6/a/16acc601-1b7a-42ad-8d4e-4f0aa156ec3e/XPS_1_0.exe)します。
