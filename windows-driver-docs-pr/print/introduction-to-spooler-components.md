---
title: スプーラー コンポーネントの概要
description: スプーラー コンポーネントの概要
ms.assetid: 4eb6e84a-f75f-4ec2-af4f-0007678d120b
keywords:
- スプーラー コンポーネント図 WDK の印刷
- 印刷スプーラー コンポーネント図 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b2d5595061d401fcfb4b4e58b510ceee4dc12940
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382615"
---
# <a name="introduction-to-spooler-components"></a>スプーラー コンポーネントの概要





Microsoft Windows 2000 およびそれ以降の印刷スプーラーの主要コンポーネントは、次の図に示します。

![印刷スプーラを後で、windows 2000 の主要なコンポーネントを示す図](images/spoocomp.png)

<a href="" id="application-"></a>**アプリケーション**   
印刷アプリケーションは、GDI 関数を呼び出すことによって、印刷ジョブを作成します。

<a href="" id="gdi-"></a>**GDI**   
グラフィックス デバイス インターフェイス (*GDI*) ユーザー モードとカーネル モードの両方のコンポーネントが含まれています。 Microsoft Win32 GDI や、ユーザー モード コンポーネントは、グラフィックスのサポートを必要とする Win32 アプリケーションによって使用されます。 カーネル モード コンポーネント、*グラフィックス エンジン*(またはグラフィックスのレンダリング エンジン) サービスとグラフィックス デバイス ドライバーを使用する関数をエクスポートします。

<a href="" id="winspool-drv-"></a>**Winspool.drv**   
Winspool.drv は、スプーラーにクライアントのインターフェイスです。 スプーラの Win32 API を構成する関数をエクスポートし、サーバーにアクセスするための RPC のスタブを提供します。 (GDI は、プライマリのクライアントがアプリケーションでもいくつかの Win32 関数を呼び出します)。

<a href="" id="spoolsv-exe-"></a>**Spoolsv.exe**   
Spoolsv.exe は、スプーラーの API サーバーです。 オペレーティング システムの起動時に開始される Windows 2000 (またはそれ以降) サービスとして実装されます。 このモジュールは、スプーラーの Win32 API のサーバー側の RPC インターフェイスをエクスポートします。 Spoolsv.exe のクライアントには (リモート) Winspool.drv (ローカル) と Win32spl.dll が含まれます。 モジュールには、一部の API 関数が実装されていますが、ほとんどの関数呼び出しに渡される、[印刷プロバイダー](print-providers.md)ルーター (Spoolss.dll) を使用しています。

<a href="" id="router-"></a>**ルーター**   
Spoolss.dll、ルーターは、プリンター名またはの各関数呼び出しで指定されたハンドルに基づく呼び出すには、印刷プロバイダーを決定し、関数呼び出し、適切なプロバイダーを渡します。

<a href="" id="print-provider-"></a>**印刷のプロバイダー**   
指定した印刷デバイスをサポートする印刷プロバイダー。

<a href="" id="print-monitor-"></a>**モニターを印刷します。**   
Windows XP は、2 種類のモニターの印刷をサポートしています。 言語モニター、およびポート モニター。

プリンターのハードウェアが、アプリケーションが実行されているシステムにローカルの場合は、「クライアント」および"server"は、同じシステム (ただし、図ではありません)。

すべてのスプーラー コンポーネントは、ユーザー モードで実行します。

 

 




