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
ms.openlocfilehash: d477e0f5fa1da4ace403258679f4a2a3af74050c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379904"
---
# <a name="installation-requirements-for-display-miniport-and-user-mode-display-drivers"></a>ディスプレイ ミニポートおよびユーザー モード ディスプレイ ドライバーのインストール要件


としてマークされている INF ファイルを使用して、オペレーティング システムでグラフィックス デバイスのディスプレイのミニポート ドライバーがインストールされている**クラスの表示を =** します。 この INF は、ドライバーのインストール中に、システム提供の表示のクラスのインストーラーによって解釈されます。

Windows Vista 以降、グラフィックス デバイスのディスプレイ ミニポート ドライバーの INF ファイルは、すべてのソフトウェアの設定を格納する必要があります、 [ **DDInstall セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-section)します。 これにより、オペレーティング システム、プラグ アンド プレイ (PnP) にすべてのレジストリ値をコピーするソフトウェア キー、レジストリで。

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

参照してください、 [INF ファイルの概要](https://docs.microsoft.com/windows-hardware/drivers/install/overview-of-inf-files)と[INF ファイルのセクションとディレクティブ](https://docs.microsoft.com/windows-hardware/drivers/install/inf-file-sections-and-directives)ミニポート ドライバーの INF ファイルの表示を作成する一般的な情報についてのセクションでします。 レジストリの詳細については、ルートなど、識別子**HKR**を参照してください[ **INF AddReg ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)します。

**注**   INF セクションではありませんしをアンインストールするためのディレクティブは、グラフィック デバイスに固有のドライバーを表示します。

 

 

 





