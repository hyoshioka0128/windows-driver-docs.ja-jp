---
title: 使用量によって正規化されたコミュニケーションおよびコラボレーション アプリケーションでのユーザー モードのクラッシュ数 <= ベースライン目標
description: この測定値は、年換算の総実行時間について、グラフィックス ドライバーに起因するコミュニケーションおよびコラボレーション アプリケーションのクラッシュの割合として、7 日間のスライディング ウィンドウからのテレメトリを集計したものです。
ms.topic: article
ms.date: 05/11/2020
ms.localizationpriority: medium
ms.openlocfilehash: c219625a0ba3882cfeefb8c90a4d89bf2857130a
ms.sourcegitcommit: cb5f370b867ceab28b6b6c64a3586b0bb3831b3d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/07/2020
ms.locfileid: "86036023"
---
# <a name="number-of-user-mode-crashes-in-communication-and-collaboration-applications-normalized-by-usage--baseline-goal-ecosystem"></a>使用量によって正規化されたコミュニケーションおよびコラボレーション アプリケーションでのユーザー モードのクラッシュ数 <= ベースライン目標 (エコシステム)

## <a name="description"></a>説明

この測定値では、コミュニケーションおよびコラボレーション アプリケーションのコンテキスト内で発生したディスプレイ ドライバーのクラッシュの数をカウントし、更新されたドライバーがインストールされているすべてのマシンにおけるそれらのアプリケーションの実行時間を計算します。 次に、測定値は年換算の累積アプリケーション実行時間によってクラッシュ数を正規化します (HOART - アプリケーション実行時間におけるヒット)。

この測定値で考慮されるコミュニケーションおよびコラボレーション アプリケーションの例を次に示します。

* MICROSOFT.SKYPEAPP
* DISCORD.EXE
* SKYPE.EXE
* TEAMVIEWER.EXE
* LYNC.EXE
* WECHAT.EXE
* QQ.EXE
* SLACK.EXE
* KAKAOTALK.EXE
* ZOOM.EXE
* ZOOM
* WHATSAPP.EXE
* LINE.EXE
* YOUCAMSERVICE.EXE
* TELEGRAM.EXE
* VIBER.EXE
* MICROSOFT.SKYPEROOMSYSTEM

これは、[使用量により正規化されたコミュニケーションおよびコラボレーション アプリケーションでのユーザー モードのクラッシュ数 <= ベースライン目標](https://docs.microsoft.com/windows-hardware/drivers/dashboard/graphics-user-mode-crashes-collaboration-standard)の測定値のエコシステムに対応するものです。

## <a name="measure-attributes"></a>測定値の属性

|属性|値|
|----|----|
|**オーディエンス**|エコシステム|
|**期間**|7 日間のスライディング ウィンドウ|
|**測定基準**|コミュニケーションおよびコラボレーション アプリケーションの年換算の実行時間の集計|
|**最小母集団**|10,000 時間のコミュニケーションおよびコラボレーション アプリケーションの実行時間|
|**合格基準**|<= 累積実行時間 1 年あたり 1 回のクラッシュ|
|**測定 ID**|25912731|

## <a name="calculation"></a>計算

この測定値は、年換算の総実行時間について、グラフィックス ドライバーに起因する Microsoft Edge Chromium のクラッシュの割合として、7 日間のスライディング ウィンドウからのテレメトリを集計したものです

Edge Chromium の総クラッシュ = ドライバーがインストールされているマシンで Edge Chromium がクラッシュした回数

Edge Chromium の総実行時間 = ドライバーがインストールされている各マシンにおける Edge Chromium の実行時間の合計

年換算の実行時間 = Edge Chromium 総実行時間 ∗ 60 (分) ∗ 60 (時間) ∗ 24 (日) ∗ 365 (年)

### <a name="final-calculation"></a>最終的な計算

使用量 = Edge Chromium の総クラッシュ回数/年間実行時間で正規化した Edge Chromium のクラッシュ回数
