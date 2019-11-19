---
title: 7日以内にファームウェアが正常にインストールされ、ハートビートしないマシンの割合
description: この測定値は、28 日間のスライディング ウィンドウからのテレメトリを、ファームウェアが正常にインストールされたマシンに対する 7 日間テレメトリを報告しなかったマシンの割合に集計したものです
ms.topic: article
ms.date: 10/31/2019
ms.localizationpriority: medium
ms.openlocfilehash: 57e804d79df3dd6ca406615463697a974ed4ddb4
ms.sourcegitcommit: 07b2926c15f4782e1914e8d3cf6c5c511a3a6111
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/14/2019
ms.locfileid: "74097496"
---
# <a name="percent-of-machines-that-successfully-installed-firmware-and-not-heartbeat-within-7-days"></a>7日以内にファームウェアが正常にインストールされ、ハートビートしないマシンの割合

## <a name="description"></a>説明

7 日間ハートビートがない、ファームウェアが正常にインストールされマシンの割合。   

この測定値は、28 日間のスライディング ウィンドウからのテレメトリを、ファームウェアが正常にインストールされたマシンに対する 7 日間テレメトリを報告しなかったマシンの割合に集計したものです

これは、停止した可能性のあるマシンを検出するためのものです。 

## <a name="measure-attributes"></a>測定値の属性

|属性|Value|
|----|----|
|**オーディエンス**|小売と内部関係者|
|**期間**|28 日間のスライディング ウィンドウ|
|**測定基準**|マシンの集計|
|**最小インスタンス**|250|
|**合格基準**|50% を上回る|
|**測定 ID**|23095161|

## <a name="calculation"></a>計算

7 日以内にハートビートがないマシン /

ファームウェアが正常にインストールされたマシン (測定 20116729 のとおり)

