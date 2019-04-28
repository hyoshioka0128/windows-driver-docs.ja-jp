---
title: Windows Display Driver Model (WDDM) の設計ガイド
description: Windows Display Driver Model (WDDM) は、Windows Vista から使用できますが Windows 8 以降が必要です。 このセクションでは、要件、仕様、および WDDM ドライバーの動作について説明します。
ms.assetid: d9dc0d48-aea4-4614-a23b-e2449800469f
keywords:
- WDK WDDM の設計のガイド
- WDK の Windows Vista のドライバー モデルを表示します。
- Windows Vista display driver モデル WDK
- WDK のデバイスを表示します。
- ディスプレイ ドライバー WDK、Windows Vista
- WDK Windows Vista では、ディスプレイ ドライバー モデルは、ディスプレイ ドライバー モデルについて
- Windows Vista ディスプレイ ドライバー モデル WDK、ディスプレイ ドライバー モデルについて
- ミニポート ドライバー WDK ディスプレイ
- ミニポート ドライバー WDK を参照してくださいミニポート ドライバー WDK の表示を表示します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 03dbe538a843370d5fe33e1392f273918ff5f0c3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375864"
---
# <a name="windows-display-driver-model-wddm-design-guide"></a>Windows Display Driver Model (WDDM) の設計ガイド


Windows Display Driver Model (WDDM) は、Windows Vista から使用できますが Windows 8 以降が必要です。 このセクションでは、要件、仕様、および WDDM ドライバーの動作について説明します。

## <span id="wddm_id"></span><span id="WDDM_ID"></span>


**注**  [Windows 2000 Display Driver Model (XDDM)](windows-2000-display-driver-model-design-guide.md)と VGA ドライバーは、Windows 8 およびそれ以降のバージョンではコンパイルされません。 ディスプレイ ハードウェアが認定 WDDM 1.2 をサポートする、またはそれ以降であるドライバーがない Windows 8 コンピューターに接続されている場合は、Microsoft Basic 表示ドライバーを実行しているシステムが既定値です。

 

次のセクションでは、Windows Display Driver Model (WDDM) について説明します。

[Windows 10 のディスプレイ ドライバー (WDDM 2.0) の新機能については](what-s-new-for-windows-threshold-display-drivers--wddm-2-0-.md)

[Windows 8.1 のディスプレイ ドライバー (WDDM 1.3) の新機能については](what-s-new-for-windows-8-1-display-drivers--wddm-1-3-.md)

[Windows 8 のディスプレイ ドライバー (WDDM 1.2) の新機能については](what-s-new-for-windows-8-display-drivers.md)

[Windows 7 のディスプレイ ドライバー (WDDM 1.1) の新機能については](what-s-new-for-windows-7-display-drivers--wddm-1-1-.md)

[WDDM 2.0 および Windows 10](wddm-2-0-and-windows-10.md)

[Windows 8 および WDDM 1.2](wddm-in-windows-8.md)

[Windows Display Driver Model (WDDM) の概要](introduction-to-the-windows-vista-and-later-display-driver-model.md)

[表示ミニポートとユーザー モードのディスプレイ ドライバーのインストール要件](installing-display-miniport-and-user-mode-display-drivers.md)

[Windows 7 以降用に最適化されたディスプレイ ドライバーのインストール要件](installing-display-drivers-optimized-for-windows-7-and-later.md)

[表示ミニポートとユーザー モードのディスプレイ ドライバーの初期化](initializing-display-miniport-and-user-mode-display-drivers.md)

[Windows Vista ドライバーがスレッドと同期モデルの表示](windows-vista-display-driver-threading-and-synchronization-model.md)

[ビデオ メモリ管理と GPU がスケジュール設定](video-memory-management-and-gpu-scheduling.md)

[ユーザー モードのディスプレイ ドライバー](user-mode-display-drivers.md)

[モニターのドライバー](monitor-drivers.md)

[複数のモニターとビデオの存在するネットワーク](multiple-monitors-and-video-present-networks.md)

[Windows Display Driver Model (WDDM) 内のタスク](tasks-in-the-windows-vista-display-driver-model.md)

[Windows Display Driver Model (WDDM) のデバッグのヒント](debugging-tips-for-the-windows-vista-display-driver-model.md)

[実装のヒントと Windows Display Driver Model (WDDM) の要件](implementation-tips-and-requirements-for-the-windows-vista-display-dri.md)

[ディスプレイのサンプル](display-samples.md)

[DX された Api 用のコンテナーのサポート](container-non-dx.md)

**注**  WDDM ドライバーが Windows グラフィックス デバイス インターフェイス (GDI) エンジンのサービスを直接使用しないでください。 したがって、、 [GDI](gdi.md)セクションは、ディスプレイ ドライバー、WDDM ドライバー モデルの作成に関係がないです。

 

 

 





