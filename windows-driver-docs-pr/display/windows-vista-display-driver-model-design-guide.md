---
title: Windows Display Driver Model (WDDM) の設計ガイド
description: Windows Display Driver Model (WDDM) は Windows Vista 以降で使用でき、windows 8 以降で必要です。 このセクションでは、WDDM ドライバーの要件、仕様、および動作について説明します。
ms.assetid: d9dc0d48-aea4-4614-a23b-e2449800469f
keywords:
- WDDM 設計ガイド WDK
- ドライバーモデルの表示 WDK Windows Vista
- Windows Vista display driver model WDK
- デバイスの WDK を表示する
- ディスプレイドライバー WDK、Windows Vista
- ディスプレイドライバーモデル WDK Windows Vista、ディスプレイドライバーモデルについて
- Windows Vista display driver model WDK、display driver model の概要
- ミニポート ドライバー WDK ディスプレイ
- ミニポートドライバーの表示 WDK 「ミニポートドライバーの WDK ディスプレイ」を参照してください。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 28f2f70abaaed11398fb99aa3f9ff4304da9f9af
ms.sourcegitcommit: d395d4b36f39d3557adda53735a4fdc8745a6408
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83642554"
---
# <a name="windows-display-driver-model-wddm-design-guide"></a>Windows Display Driver Model (WDDM) の設計ガイド

Windows Display Driver Model (WDDM) は Windows Vista 以降で使用でき、windows 8 以降で必要です。 このセクションでは、WDDM ドライバーの要件、仕様、および動作について説明します。

## <span id="wddm_id"></span><span id="WDDM_ID"></span>

**注**  [Windows 2000 Display Driver Model (XDDM)](windows-2000-display-driver-model-design-guide.md)と VGA ドライバーは、windows 8 以降のバージョンではコンパイルされません。 WDDM 1.2 以降のサポートを認定されたドライバーのない Windows 8 コンピューターにディスプレイ ハードウェアが接続されている場合、システムは既定で Microsoft Basic Display Driver を実行します。

次のセクションでは、Windows Display Driver Model (WDDM) について説明します。

[Windows 10 ディスプレイおよびグラフィックス ドライバーの新機能](what-s-new-for-windows-10-display-and-graphics-drivers.md)

[Windows 8.1 ディスプレイ ドライバー (WDDM 1.3) の新機能](what-s-new-for-windows-8-1-display-drivers--wddm-1-3-.md)

[Windows 8 ディスプレイ ドライバー (WDDM 1.2) の新機能](what-s-new-for-windows-8-display-drivers.md)

[Windows 7 ディスプレイ ドライバー (WDDM 1.1) の新機能](what-s-new-for-windows-7-display-drivers--wddm-1-1-.md)

[WDDM 2.0 と Windows 10](wddm-2-0-and-windows-10.md)

[WDDM 1.2 と Windows 8](wddm-in-windows-8.md)

[Windows Display Driver Model (WDDM) の概要](introduction-to-the-windows-vista-and-later-display-driver-model.md)

[ディスプレイ ミニポートおよびユーザー モード ディスプレイ ドライバーのインストール要件](installing-display-miniport-and-user-mode-display-drivers.md)

[Windows 7 以降用に最適化されたディスプレイ ドライバーのインストール要件](installing-display-drivers-optimized-for-windows-7-and-later.md)

[ディスプレイ ミニポートおよびユーザー モード ディスプレイ ドライバーの初期化](initializing-display-miniport-and-user-mode-display-drivers.md)

[Windows Vista の表示ドライバーのスレッド処理と同期モデル](windows-vista-display-driver-threading-and-synchronization-model.md)

[ビデオ メモリ管理と GPU スケジュール設定](video-memory-management-and-gpu-scheduling.md)

[ユーザー モード ディスプレイ ドライバー](user-mode-display-drivers.md)

[モニター ドライバー](monitor-drivers.md)

[複数モニターとビデオ表現ネットワーク](multiple-monitors-and-video-present-networks.md)

[Windows Display Driver Model (WDDM) のタスク](tasks-in-the-windows-vista-display-driver-model.md)

[Windows Display Driver Model (WDDM) のデバッグのヒント](debugging-tips-for-the-windows-vista-display-driver-model.md)

[Windows Display Driver Model (WDDM) の実装に関するヒントと要件](implementation-tips-and-requirements-for-the-windows-vista-display-dri.md)

[ディスプレイのサンプル](display-samples.md)

[DX 以外の Api のコンテナーサポート](container-non-dx.md)

**メモ**   WDDM ドライバーでは、Windows グラフィックスデバイスインターフェイス (GDI) エンジンのサービスは直接使用されません。そのため、[ [GDI](gdi.md) ] セクションは、WDDM ドライバーモデルのディスプレイドライバーの記述には関係ありません。
