---
title: Bitlocker のリスクが原因で、ファームウェアの更新が保留中のマシンの割合
description: この測定値は、28 日間のスライディング ウィンドウからのテレメトリを、ファームウェアのインストールを試行したマシンに対する Bitlocker によってブロックされたマシンの割合に集計したものです
ms.topic: article
ms.date: 10/31/2019
ms.localizationpriority: medium
ms.openlocfilehash: 3c684f0f77439a5732f7036873c2457fbd105b0e
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "79083129"
---
# <a name="percent-of-machines-with-pending-firmware-updates-due-to-bitlocker-risk"></a>Bitlocker のリスクが原因で、ファームウェアの更新が保留中のマシンの割合

## <a name="description"></a>説明

インストール後に Bitlocker 回復に入る可能性があるため、ファームウェア更新が保留中のマシンの割合。 これは、2018 年 6 月の累積的な更新プログラムを適用した Windows 10 より前のバージョンを実行しているお客様が対象です。

## <a name="measure-attributes"></a>測定値の属性

|属性|値|
|----|----|
|**オーディエンス**|小売と内部関係者|
|**期間**|28 日間のスライディング ウィンドウ|
|**測定基準**|マシンの集計|
|**最小インスタンス**|250|
|**合格基準**|<= 10%|
|**測定 ID**|23153969|

## <a name="calculation"></a>計算

Bitlocker によってブロックされたマシンの数 /

ファームウェアのインストールを試行したマシンの数

