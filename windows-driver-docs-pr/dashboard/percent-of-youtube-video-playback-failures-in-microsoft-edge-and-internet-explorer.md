---
title: Microsoft Edge と Internet Explorer での YouTube ビデオ再生エラーの割合
description: この測定値は、Microsoft Edge または Internet Explorer での YouTube 再生エラーの割合として、7 日間のスライディング ウィンドウからのテレメトリを集計したものです
ms.topic: article
ms.date: 05/20/2019
ms.localizationpriority: medium
ms.openlocfilehash: 74a0af946d837fe120dd6dc7fe34086b661cadab
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "71016942"
---
# <a name="percent-of-youtube-video-playback-failures-in-microsoft-edge-and-internet-explorer"></a>Microsoft Edge と Internet Explorer での YouTube ビデオ再生エラーの割合

## <a name="description"></a>説明

ユーザーが Microsoft Edge または Internet Explorer を使用して YouTube ビデオを視聴する際、Web からのビデオ ストリームがグラフィックス コンポーネントによって処理されて、レンダリングされたビデオが画面に表示されます。 この測定値は、Microsoft Edge で YouTube ビデオを再生できない頻度を監視するものです。再生エラーが発生すると、ユーザーはビデオを読み込んで視聴することができなくなります。

## <a name="measure-attributes"></a>測定値の属性

|属性|値|
|----|----|
|**オーディエンス**|Standard |
|**期間**|7 日間のスライディング ウィンドウ|
|**測定基準**|インスタンスの集計|
|**最小インスタンス**|50 回 (YouTube での再生回数)|
|**合格基準**|\<video>.error プロパティが設定されている YouTube ビデオ要素が 1% 以下|
|**測定 ID**|6195478|

## <a name="calculation"></a>計算

1. この測定値は、**Microsoft Edge または Internet Explorer での YouTube 再生エラーの割合**として、7 日間のスライディング ウィンドウからのテレメトリを集計したものです。
2. *セッション = YouTube メディア リソースを HTML5 \<video> 要素に読み込む 1 つのインスタンス*

   a。 1 台のマシンで複数のセッションが許可されます。

3. 再生エラー数 = Microsoft Edge または Internet Explorer で YouTube \<video>.error 要素が発生した回数

### <a name="final-calculation"></a>最終的な計算

"*Microsoft Edge または Internet Explorer での YouTube の HTML5 再生エラー数 = 再生エラー数 / セッション数*"
