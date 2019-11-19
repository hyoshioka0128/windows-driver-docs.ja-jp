---
title: 14日以内にファームウェアが正常にインストールされ、ハートビートしないマシンの割合
description: この測定値は、28 日間のスライディング ウィンドウからのテレメトリを、ファームウェアが正常にインストールされたマシンに対する 14 日間テレメトリを報告しなかったマシンの割合に集計したものです
ms.topic: article
ms.date: 10/31/2019
ms.localizationpriority: medium
ms.openlocfilehash: 09120b2e914c95f7c0d563378804b9833e3d6494
ms.sourcegitcommit: 07b2926c15f4782e1914e8d3cf6c5c511a3a6111
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/14/2019
ms.locfileid: "74097502"
---
# <a name="percent-of-machines-that-successfully-installed-firmware-and-not-heartbeat-within-14-days"></a>14日以内にファームウェアが正常にインストールされ、ハートビートしないマシンの割合

## <a name="description"></a>説明

14 日間ハートビートがない、ファームウェアが正常にインストールされたマシンの割合。   

この測定値は、28 日間のスライディング ウィンドウからのテレメトリを、ファームウェアが正常にインストールされたマシンに対する 14 日間テレメトリを報告しなかったマシンの割合に集計したものです

これは、停止した可能性のあるマシンを検出するためのものです。 

## <a name="measure-attributes"></a>測定値の属性

|属性|Value|
|----|----|
|**オーディエンス**|小売と内部関係者|
|**期間**|28 日間のスライディング ウィンドウ|
|**測定基準**|マシンの集計|
|**最小インスタンス**|250|
|**合格基準**|50% を上回る|
|**測定 ID**|23095170|

## <a name="calculation"></a>計算

14 日以内にハートビートがないマシン /

ファームウェアが正常にインストールされたマシン (測定 20116729 のとおり)

