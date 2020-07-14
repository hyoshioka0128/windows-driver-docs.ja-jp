---
title: グラフィックス ドライバー バイナリのクラッシュによってブルー スクリーンが表示された統合 GPU の無数のマシン
description: この測定値は、グラフィックス ドライバーのバイナリにおけるクラッシュが原因でブルー スクリーンが発生した統合 GPU の個別のマシンのミリアドに対する、7 日間のスライディング ウィンドウからのテレメトリを集計したものです
ms.topic: article
ms.date: 10/28/2019
ms.localizationpriority: medium
ms.openlocfilehash: 888f325db668dfc4d12f3f1e8fec68d4e8862df9
ms.sourcegitcommit: cb5f370b867ceab28b6b6c64a3586b0bb3831b3d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/07/2020
ms.locfileid: "86036014"
---
# <a name="myriad-of-machines-with-integrated-gpu-that-had-a-blue-screen-caused-by-a-crash-in-the-graphics-driver-binary-ecosystem"></a>グラフィックス ドライバー バイナリのクラッシュによってブルー スクリーンが表示された統合 GPU の無数のマシン (エコシステム)

## <a name="description"></a>説明

ユーザーのセッション中、グラフィックス ドライバーのバイナリにおけるクラッシュが原因でブルー スクリーンが発生し、その結果マシンが再起動されて、ユーザーのワークフローが中断されることがあります。 この測定では、グラフィックス ドライバーのバイナリにおけるクラッシュが原因でブルー スクリーンが生じたドライバーが存在する統合 GPU のマシンのミリアド (10,000 台に対する) が評価されます。 

これは、[グラフィックス ドライバーのバイナリにおけるクラッシュによってブルー スクリーンが表示された、統合 GPU のマシンのミリアド](https://docs.microsoft.com/windows-hardware/drivers/dashboard/myriad-of-machines-that-had-blue-screen-caused-by-crash-in-graphics-driver-binary-integrated-standard)の測定のエコシステムに対応するものです。

## <a name="measure-attributes"></a>測定値の属性

|属性|値|
|----|----|
|**オーディエンス**|エコシステム|
|**期間**|7 日間のスライディング ウィンドウ|
|**測定基準**|マシンの集計|
|**最小母集団**|20,000 台のマシン|
|**合格基準**|ブルー スクリーンの発生したマシンが 10,000 台中 3 台以下|
|**測定 ID**|23253402|

## <a name="calculation"></a>計算

この測定では、**グラフィックス ドライバーのバイナリにおけるクラッシュが原因でブルー スクリーンが発生した統合 GPU の個別のマシン**の**ミリアド**に対する、7 日間のスライディング ウィンドウからのテレメトリが集計されます。
1. *ブルー スクリーンが発生したマシン = ドライバーが入れられており、ブルー スクリーンが発生した統合 GPU のマシンの台数*
2. *総マシン数 = ドライバーが入れられている統合 GPU のマシンの台数*
3. *ブルー スクリーンが発生したマシンの割合 = ブルー スクリーンが発生したマシン/総マシン数*

### <a name="final-calculation"></a>最終的な計算

*母集団に対する個別のデバイス ヒット数 (DHoP) = ブルー スクリーンが発生したマシンの割合 * 10,000*

上記の計算では、結果は 10,000 台のマシンに正規化され、最終的な結果は次のようになります。       
[母集団に対する個別のデバイス ヒット数 (DHoP)] 10,000 台のマシンのうち、グラフィックス ドライバーのバイナリにおけるクラッシュが原因でブルー スクリーンが発生した個別のマシン
