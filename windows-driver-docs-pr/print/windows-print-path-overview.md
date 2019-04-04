---
title: Windows 印刷パスの概要
description: Windows 印刷パスの概要
ms.assetid: c06e122b-a4d8-4b3a-9db0-0bc8f2728177
keywords:
- XPSDrv プリンター ドライバー WDK、印刷パス
- 印刷パス WDK XPSDrv
- GDI 印刷パス WDK XPSDrv
- XPS 印刷パス WDK XPSDrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 848068adda4ac0f0e310ef4c24fca5bc65707aef
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580693"
---
# <a name="windows-print-path-overview"></a>Windows 印刷パスの概要

Windows では、2 つの主な印刷パスと 2 つの追加の変換パスを提供します。 2 つの主な印刷パスは次のとおりです。

-   GDI 印刷パス (Windows Server 2003 の印刷パスに似ています)。 このパスは、Win32 パスとも呼ばれます、GDI グラフィックス API を使用して Win32 アプリケーションで発生します。

-   XPS 印刷パスです。 このパスは、Windows Presentation Foundation (WPF) アプリケーションまたは XPS 印刷 API から生成されます。

2 つの変換オプション。

-   GDI-XPS 変換 (MXDC)。

-   XPS-への変換 (XGC)。

### <a name="general-data-flow"></a>一般的なデータ フロー

次の図は、さまざまな印刷 XPSDrv サブシステムのパスと変換のオプションを示します。

![xpsdrv サブシステムのさまざまな印刷パスと変換オプションを示す図](images/printpathoverview.png)

フィルター パイプラインのサービスを構成する方法の詳細については、[フィルター パイプライン構成ファイル](filter-pipeline-configuration-file.md)を参照してください。

バージョン 3 印刷ドライバーを Windows Vista と Windows の以降のバージョンの構成に関する詳細については、[バージョン 3 XPSDrv 印刷ドライバー コンポーネント](version-3-xpsdrv-print-driver-components.md)を参照してください。
