---
title: ファームウェアのインストール後に WHEA エラーが発生したマシンの割合
description: この測定値は、28 日間のスライディング ウィンドウからのテレメトリを、ファームウェアが正常にインストールされたマシンに対する致命的な WHEA イベントを報告したマシンの割合に集計したものです
ms.topic: article
ms.date: 10/31/2019
ms.localizationpriority: medium
ms.openlocfilehash: 30f38e1329e47918ad5b0ec1d6abfcc4d7d3852d
ms.sourcegitcommit: 07b2926c15f4782e1914e8d3cf6c5c511a3a6111
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/14/2019
ms.locfileid: "74097506"
---
# <a name="percent-of-machines-with-whea-error-after-firmware-installation"></a>ファームウェアのインストール後に WHEA エラーが発生したマシンの割合

## <a name="description"></a>説明

ファームウェアのインストール後に致命的な WHEA イベント (WheaProvider.WheaDriverErrorExternal) を報告した、正常にインストールされたマシンの割合。

この測定値は、28 日間のスライディング ウィンドウからのテレメトリを、ファームウェアが正常にインストールされたマシンに対する致命的な WHEA イベントを報告したマシンの割合に集計したものです

WHEA イベントは 20H1 ビルドからのみ発生します。そのため、19H1 に対してバックポートされます。

## <a name="measure-attributes"></a>測定値の属性

|属性|Value|
|----|----|
|**オーディエンス**|小売と内部関係者|
|**期間**|28 日間のスライディング ウィンドウ|
|**測定基準**|マシンの集計|
|**最小インスタンス**|200|
|**合格基準**|5% 以下|
|**測定 ID**|20319726|

## <a name="calculation"></a>計算

致命的な WHEA エラーを報告したマシン /

ファームウェアが正常にインストールされたマシン (測定 20116729 で定義)

