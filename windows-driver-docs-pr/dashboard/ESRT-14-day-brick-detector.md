---
title: 14 日以内にファームウェアが正常にインストールされ、ハートビートが確認されていないマシンの割合
description: この測定値は、28 日間のスライディング ウィンドウからのテレメトリを、ファームウェアが正常にインストールされたマシンに対する 14 日間テレメトリを報告しなかったマシンの割合に集計したものです
ms.topic: article
ms.date: 10/31/2019
ms.localizationpriority: medium
ms.openlocfilehash: 1d8e46ef69b3c9b9a40c2d596fd6ebd15bcf06f1
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "79083147"
---
# <a name="percent-of-machines-that-successfully-installed-firmware-and-have-seen-no-heartbeat-within-14-days"></a>14 日以内にファームウェアが正常にインストールされ、ハートビートが確認されていないマシンの割合

## <a name="description"></a>説明

14 日間ハートビートが確認されていないファームウェアを正常にインストールしたマシンの割合。   

この測定値は、28 日間のスライディング ウィンドウからのテレメトリを、ファームウェアが正常にインストールされたマシンに対する 14 日間テレメトリを報告しなかったマシンの割合に集計したものです

これは、停止した可能性のあるマシンを検出するためのものです。 

## <a name="measure-attributes"></a>測定値の属性

|属性|値|
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

