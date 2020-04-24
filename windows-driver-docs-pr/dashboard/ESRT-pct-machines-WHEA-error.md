---
title: ファームウェアのインストール後に WHEA エラーが発生したマシンの割合
description: この測定値は、28 日間のスライディング ウィンドウからのテレメトリを、ファームウェアが正常にインストールされたマシンに対する致命的な WHEA イベントを報告したマシンの割合に集計したものです
ms.topic: article
ms.date: 10/31/2019
ms.localizationpriority: medium
ms.openlocfilehash: 7c9b46519daeb40725267ac9d285a1442bfd611b
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "79083123"
---
# <a name="percent-of-machines-with-windows-hardware-error-architecture-whea-error-after-firmware-installation"></a>ファームウェアのインストール後に Windows Hardware Error Architecture (WHEA) エラーが発生したマシンの割合

## <a name="description"></a>説明

ファームウェアのインストール後に致命的な WHEA イベント (WheaProvider.WheaDriverErrorExternal) を報告した、正常にインストールされたマシンの割合。

この測定値は、28 日間のスライディング ウィンドウからのテレメトリを、ファームウェアが正常にインストールされたマシンに対する致命的な WHEA イベントを報告したマシンの割合に集計したものです

WHEA イベントは 20H1 ビルドからのみ発生します。そのため、19H1 に対してバックポートされます。

## <a name="measure-attributes"></a>測定値の属性

|属性|値|
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

