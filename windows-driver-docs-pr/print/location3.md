---
title: 場所 (ホチキス止め)
description: このプロパティには、出力ページのホチキス止め位置に関連するすべての値のエントリが含まれます。
ms.assetid: cbe6ec7f-36dd-484e-8db6-42e91e69577c
ms.date: 07/07/2020
ms.localizationpriority: medium
ms.openlocfilehash: a8a714ed9489c7919f7e181040da2d7a334ff450
ms.sourcegitcommit: ff2f72fe98f6ba559c1c01b17d25c773df7337c1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/07/2020
ms.locfileid: "86060849"
---
# <a name="location-staple"></a>場所 (ホチキス止め)

スキーマパス: \\ Printer... ステープル. 場所

ノードの種類: プロパティ

説明: このプロパティには、出力ページのホチキス止め位置に関連するすべての値のエントリが含まれます。

Location プロパティには、 **Currentvalue**と supported の2つの子値が含ま**れてい**ます。

## <a name="currentvalue"></a>CurrentValue

スキーマパス: \\ Printer... ステープル. Location: CurrentValue

ノードの種類: 値

データ型: BIDI \_ 文字列

説明: ホチキス止めが適用される現在の (既定の) 場所。

次の値を使用できます。

StapleTopLeft

左側にあるもの

StapleTopRight

最適

StapleDualLeft

StapleDualRight

StapleDualTop

StapleDualBottom

SaddleStitch

その他

Unknown

## <a name="supported"></a>サポートされています

スキーマパス: \\ Printer... ステープル. Location: サポートされています

ノードの種類: 値

データ型: BIDI \_ 文字列

説明: ホチキス止めの場所でサポートされているすべての値のコンマ区切りの一覧です。
