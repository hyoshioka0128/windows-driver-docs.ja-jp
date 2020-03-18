---
title: 7 日以内にファームウェアが正常にインストールされ、ハートビートが確認されていないマシンの割合
description: この測定値は、28 日間のスライディング ウィンドウからのテレメトリを、ファームウェアが正常にインストールされたマシンに対する 7 日間テレメトリを報告しなかったマシンの割合に集計したものです
ms.topic: article
ms.date: 10/31/2019
ms.localizationpriority: medium
ms.openlocfilehash: c324f996aa6dbf53184a7e889e02e4897eb394f9
ms.sourcegitcommit: 387de60712790691970924e059b0564325e211bc
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/11/2020
ms.locfileid: "79083146"
---
# <a name="percent-of-machines-that-successfully-installed-firmware-and-have-seen-no-heartbeat-within-7-days"></a>7 日以内にファームウェアが正常にインストールされ、ハートビートが確認されていないマシンの割合

## <a name="description"></a>説明

7 日間ハートビートが確認されていないファームウェアを正常にインストールしたマシンの割合。   

この測定値は、28 日間のスライディング ウィンドウからのテレメトリを、ファームウェアが正常にインストールされたマシンに対する 7 日間テレメトリを報告しなかったマシンの割合に集計したものです

これは、停止した可能性のあるマシンを検出するためのものです。 

## <a name="measure-attributes"></a>測定値の属性

|属性|値|
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

