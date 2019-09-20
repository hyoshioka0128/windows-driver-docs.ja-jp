---
title: Netflix での SWDRM 再生エラーの割合
description: この測定値は、Netflix での SWDRM 再生エラーの割合として、7 日間のスライディング ウィンドウからのテレメトリを集計したものです
ms.topic: article
ms.date: 05/20/2019
ms.localizationpriority: medium
ms.openlocfilehash: ba21858cb369ffb8e783618476aa1be5bd0c7053
ms.sourcegitcommit: b33dff0fc9b5b90ee8bd07f62713c58c5f60b40f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/16/2019
ms.locfileid: "71016936"
---
# <a name="percent-of-swdrm-playback-failures-on-netflix"></a>Netflix での SWDRM 再生エラーの割合

## <a name="description"></a>説明

ソフトウェア デジタル著作権管理 (SWDRM) は、コンテンツ ディストリビューターがコンテンツの使用方法を制御できるようにする機能です。 この機能は、秘密キーやコンテンツ キーなどのデジタル キーと、暗号化解除された圧縮および非圧縮ビデオを保護します。 SWDRM エラーが発生すると、ユーザーは Netflix などの特定のサービスでビデオを再生できなくなります。

## <a name="measure-attributes"></a>測定値の属性

|属性|Value|
|----|----|
|**オーディエンス**|エコシステム|
|**期間**|7 日間のスライディング ウィンドウ|
|**測定基準**|インスタンスの集計|
|**最小インスタンス**|200 回 (Netflix での再生回数)|
|**合格基準**|SWDRM エラーが発生した Netflix での再生が 1% 以下|
|**測定 ID**|19170139|

## <a name="calculation"></a>計算

1. この測定値は、**Netflix での SWDRM 再生エラーの割合**として、7 日間のスライディング ウィンドウからのテレメトリを集計したものです。

   a. "*再生エラー = Netflix ビデオに対して \<video>.error 要素が設定されている*"

2. "*Netflix での SWDRM 再生エラー数 = 再生エラーの回数*"
3. "*Netflix の総ビデオ数 = Netflix に対する \<video> 要素の数*"

### <a name="final-calculation"></a>最終的な計算

"*Netflix での SWDRM 再生エラーの割合 = Netflix での HWDRM 再生エラー数 / Netflix の総ビデオ数*"
