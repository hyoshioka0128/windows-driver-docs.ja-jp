---
title: ドライバーの機能スコアの設定
description: ドライバーの機能スコアの設定
ms.assetid: 833e8f29-b90a-4754-9c0a-d8356a731ae4
keywords:
- INF ファイル WDK の表示、FeatureScore ディレクティブ
- FeatureScore ディレクティブ WDK の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5b6ab89db8104ef636baac8990b0f3e79b930aa7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390435"
---
# <a name="setting-the-driver-feature-score"></a>ドライバーの機能スコアの設定


**FeatureScore**ディレクティブは、Windows Vista およびそれ以降のオペレーティング システムをインストールして実行するすべてのドライバーに必要です。

**注**   Windows 7 およびそれ以降のバージョンにのみ適用されます。
有無に基づいて、ディスプレイ ドライバーをインストールするかどうかを決定するシステム提供の表示のクラスのインストーラー、 **FeatureScore**ディレクティブと値を**FeatureScore**ディレクティブを設定します。 特徴のスコアのセットを持たないディスプレイ ドライバーをインストールしようとした場合は、エラー メッセージが表示されます。

 

**注**  ロゴ テスト要件は、Windows XP と以前のオペレーティング システムと Windows Server 2003 以前のオペレーティング システムをインストールして実行するためのドライバーが設定されていないこと、 **FeatureScore**ディレクティブ。

 

使用する必要があります、 **FeatureScore**ディレクティブに、ドライバーが書き込まれる display driver model、ドライバーの配布方法に応じて、次の値を特徴のスコアを設定します。

-   **F8** Windows Display Driver Model (WDDM) に記述されたインボックス ドライバー

-   **F6 キーを押して**WDDM に書き込まれるベンダーから提供されたドライバー

-   **FC**に書き込まれるベンダーから提供されたドライバー、 [Windows 2000 のディスプレイ ドライバー モデル](windows-2000-display-driver-model-design-guide.md)

次の例を追加する方法を示して、 **FeatureScore**ディレクティブ。

```inf
[R200_RV200]
FeatureScore=F6
CopyFiles=R200.Miniport, R200.Display
AddReg = R200_SoftwareDeviceSettings
AddReg = R200_RV200_SoftwareDeviceSettings
DelReg = R200_RemoveDeviceSettings

[R200_R200]
FeatureScore=F6
CopyFiles=R200.Miniport, R200.Display
AddReg = R200_SoftwareDeviceSettings
AddReg = R200_R200_SoftwareDeviceSettings
DelReg = R200_RemoveDeviceSettings

[R200_RV250]
FeatureScore=F6
CopyFiles=R200.Miniport, R200.Display
AddReg = R200_SoftwareDeviceSettings
AddReg = R200_RV250_SoftwareDeviceSettings
DelReg = R200_RemoveDeviceSettings
```

 
