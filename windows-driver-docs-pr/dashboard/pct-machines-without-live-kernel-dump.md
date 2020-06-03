---
title: ライブ カーネル ダンプなしのマシンの割合
description: この測定値は、ライブ カーネル ダンプが発生しなかったマシンの割合として、14 日間のスライディング ウィンドウからのテレメトリを集計したものです
ms.topic: article
ms.date: 05/22/2020
ms.localizationpriority: medium
ms.openlocfilehash: d39be63c246f232c0f917a919a9dac06517e8c56
ms.sourcegitcommit: d7b5e6049db3109fdcbe83279875f24f3fa6acdd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2020
ms.locfileid: "84108609"
---
# <a name="percent-of-machines-without-a-live-kernel-dump"></a>ライブ カーネル ダンプなしのマシンの割合

## <a name="description"></a>説明

ライブ カーネル ダンプ (LKD) は、カーネル エラーが原因で発生し、クラッシュすることなくマシンを回復できます。 LKD が発生すると、アプリケーションがハングしたりクラッシュしたりする可能性があります。 一般的な種類の LKD は、タイムアウトの検出と回復 (TDR) で、グラフィックス ドライバーがクラッシュし、ドライバーが回復するまで表示が少しの間黒くなります。

## <a name="measure-attributes"></a>測定値の属性

|属性|値|
|----|----|
|**オーディエンス**|Standard|
|**期間**|14 日間のスライディング ウィンドウ|
|**測定基準**|マシンの集計|
|**最小母集団**|100 台のマシン|
|**合格基準**|LKD が発生しなかったマシンが 90% 以上|
|**コーホートが有効**|はい|
|**コーホートあたりの最小母集団**|500 台のマシン|
|**測定 ID**|19888731|

## <a name="calculation"></a>計算

1. この測定値は、**LKD が発生しなかったマシンの割合**として、14 日間のスライディング ウィンドウからのテレメトリを集計したものです
2. "*LKD が発生しなかったマシンの台数 = LKD が発生せずにドライバーがインストールされたマシンの台数*"
3. "*総マシン数 = ドライバーが正常にインストールされたマシンの台数*"

### <a name="final-calculation"></a>最終的な計算

"*LKD が発生しなかったマシンの割合 = LKD が発生しなかったマシンの台数 / 総マシン数*"
