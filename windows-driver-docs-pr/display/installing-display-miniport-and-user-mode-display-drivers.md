---
title: 表示ミニポートとユーザー モードのディスプレイ ドライバーのインストール
description: ディスプレイ ミニポートおよびユーザー モード ディスプレイ ドライバーのインストール要件
ms.assetid: f813071d-897d-4100-bc46-326558de2e70
keywords:
- ドライバー モデル WDK Windows Vista では、ドライバーのインストールの表示します。
- Windows Vista display driver モデル WDK、ドライバーのインストール
- ドライバー モデル WDK Windows Vista では、表示をインストールします。
- ユーザー モード ドライバー WDK を表示します。
- INF ファイル WDK の表示
- グラフィック デバイス ディスプレイ ミニポート ドライバー WDK Windows Vista
- ドライバーのインストールについて、INF ファイル WDK の表示
- ミニポート ドライバー WDK の表示をインストールします。
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 3f49c9ad7f0fd1db6c5dcefe8054342cc68874d7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365453"
---
# <a name="installation-requirements-for-display-miniport-and-user-mode-display-drivers"></a>ディスプレイ ミニポートおよびユーザー モード ディスプレイ ドライバーのインストール要件


としてマークされている INF ファイルを使用して、オペレーティング システムでグラフィックス デバイスのディスプレイのミニポート ドライバーがインストールされている**クラスの表示を =** します。 この INF は、ドライバーのインストール中に、システム提供の表示のクラスのインストーラーによって解釈されます。

Windows Vista 以降、グラフィックス デバイスのディスプレイ ミニポート ドライバーの INF ファイルは、すべてのソフトウェアの設定を格納する必要があります、 [ **DDInstall セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547344)します。 これにより、オペレーティング システム、プラグ アンド プレイ (PnP) にすべてのレジストリ値をコピーするソフトウェア キー、レジストリで。

適切なインストールを確認するには、Windows 表示 Driver Model (WDDM) に準拠している任意の表示ミニポート ドライバーの INF ファイルで、次の情報を指定する必要があります。

[ドライバーの制御フラグを設定](setting-the-driver-control-flags.md)

[ソフトウェアのレジストリ設定を追加します。](adding-software-registry-settings.md)

[ユーザー モード ドライバーの表示名をレジストリに追加します。](adding-user-mode-display-driver-names-to-the-registry.md)

[ユーザー モードのディスプレイ ドライバーの読み込み](loading-a-user-mode-display-driver.md)

[ドライバーの特徴のスコアの設定](setting-the-driver-feature-score.md)

[PnP 停止をサポートするためにファイルのコピーのフラグを設定](setting-a-copy-file-flag-to-support-pnp-stop.md)

[開始の種類の値の設定](setting-the-start-type-value.md)

[OpenGL と相互運用性を無効にします。](disabling-interoperability-with-opengl.md)

[グラフィックス アダプターのわかりやすい文字列名に情報を追加](appending-information-to-the-friendly-string-names-of-graphics-adapter.md)

[LayoutFile と CatalogFile 情報を省略します。](omitting-layoutfile-and-catalogfile-information.md)

[ソース ディスクとファイルを識別します。](identifying-source-disks-and-files.md)

[X 64 の INF 情報には、[全般]](general-x64-inf-information.md)

[[全般] のインストール情報](general-install-information.md)

[モニター EDIDs、INF をオーバーライドします。](overriding-monitor-edids.md)

参照してください、 [INF ファイルの概要](https://msdn.microsoft.com/library/windows/hardware/ff549520)と[INF ファイルのセクションとディレクティブ](https://msdn.microsoft.com/library/windows/hardware/ff547433)ミニポート ドライバーの INF ファイルの表示を作成する一般的な情報についてのセクションでします。 レジストリの詳細については、ルートなど、識別子**HKR**を参照してください[ **INF AddReg ディレクティブ**](https://msdn.microsoft.com/library/windows/hardware/ff546320)します。

**注**   INF セクションではありませんしをアンインストールするためのディレクティブは、グラフィック デバイスに固有のドライバーを表示します。

 

 

 





