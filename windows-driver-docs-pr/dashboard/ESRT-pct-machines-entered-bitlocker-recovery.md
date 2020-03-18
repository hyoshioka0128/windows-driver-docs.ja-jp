---
title: 更新され、Bitlocker 回復が正常にロック解除されたマシンの割合
description: この測定値は、28 日間のスライディング ウィンドウからのテレメトリを、ファームウェアのインストールを試行したマシンに対する Bitlocker 回復イベントを報告したマシンの割合に集計したものです
ms.topic: article
ms.date: 10/31/2019
ms.localizationpriority: medium
ms.openlocfilehash: 6243b76e8c7011e368fdbdbeb39b20edd8824413
ms.sourcegitcommit: 387de60712790691970924e059b0564325e211bc
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/11/2020
ms.locfileid: "79083128"
---
# <a name="percent-of-machines-updated-and-successfully-unlocked-bitlocker-recovery"></a>更新され、Bitlocker 回復が正常にロック解除されたマシンの割合

## <a name="description"></a>説明

ファームウェアをインストールし、Bitlocker 回復に入ったマシンによって、顧客が Bitlocker 回復キーを入力して回復したマシンの割合

この測定値は、28 日間のスライディング ウィンドウからのテレメトリを、ファームウェアのインストールを試行したマシンに対する Bitlocker 回復イベントを報告したマシンの割合に集計したものです

## <a name="measure-attributes"></a>測定値の属性

|属性|値|
|----|----|
|**オーディエンス**|小売と内部関係者|
|**期間**|28 日間のスライディング ウィンドウ|
|**測定基準**|マシンの集計|
|**最小インスタンス**|250|
|**合格基準**|<= 10%|
|**測定 ID**|23154031|

## <a name="calculation"></a>計算

ブート時に Bitlocker 回復イベントを報告したマシンの数 /

ファームウェアのインストールを試行したマシンの数

