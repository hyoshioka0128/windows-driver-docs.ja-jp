---
title: 更新され、Bitlocker 回復が正常にロック解除されたマシンの割合
description: この測定値は、28 日間のスライディング ウィンドウからのテレメトリを、ファームウェアのインストールを試行したマシンに対する Bitlocker 回復イベントを報告したマシンの割合に集計したものです
ms.topic: article
ms.date: 10/31/2019
ms.localizationpriority: medium
ms.openlocfilehash: ad467e0025a56e2d689cc3f57e505811cd5236f5
ms.sourcegitcommit: 07b2926c15f4782e1914e8d3cf6c5c511a3a6111
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/14/2019
ms.locfileid: "74097494"
---
# <a name="percent-of-machines-updated-and-successfully-unlocked-bitlocker-recovery"></a>更新され、Bitlocker 回復が正常にロック解除されたマシンの割合

## <a name="description"></a>説明

ファームウェアをインストールし、Bitlocker 回復に入ったマシンによって、顧客が Bitlocker 回復キーを入力して回復したマシンの割合

この測定値は、28 日間のスライディング ウィンドウからのテレメトリを、ファームウェアのインストールを試行したマシンに対する Bitlocker 回復イベントを報告したマシンの割合に集計したものです

## <a name="measure-attributes"></a>測定値の属性

|属性|Value|
|----|----|
|**オーディエンス**|小売と内部関係者|
|**期間**|28 日間のスライディング ウィンドウ|
|**測定基準**|マシンの集計|
|**最小インスタンス**|250|
|**合格基準**|90% 以上|
|**測定 ID**|23154031|

## <a name="calculation"></a>計算

ブート時に Bitlocker 回復イベントを報告したマシンの数 /

ファームウェアのインストールを試行したマシンの数

