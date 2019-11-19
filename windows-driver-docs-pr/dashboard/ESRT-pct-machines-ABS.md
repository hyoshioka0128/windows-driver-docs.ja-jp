---
title: バグチェックまたは電源ボタンによるものではない異常なシャットダウンが発生したマシンの割合
description: この測定値は、28 日間のスライディング ウィンドウからのテレメトリを、インストールから 3 日以内に異常なシャットダウンが報告されたマシンと、正常にインストールされたマシンの割合に集計したものです
ms.topic: article
ms.date: 10/31/2019
ms.localizationpriority: medium
ms.openlocfilehash: f51fa24ee67d8d5fd1133e0c6853f54e834576cd
ms.sourcegitcommit: 07b2926c15f4782e1914e8d3cf6c5c511a3a6111
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/14/2019
ms.locfileid: "74097492"
---
# <a name="percent-of-machines-with-abnormal-shutdown-not-due-to-bugcheck-or-power-button"></a>バグチェックまたは電源ボタンによるものではない異常なシャットダウンが発生したマシンの割合

## <a name="description"></a>説明

インストールから 3 日以内にバグチェック (ABS を自動的にトリガーする) または異常な電源ボタンによるシャットダウン以外の理由でマシンが異常終了し、インストール前の 3 日間は異常終了していない、正常にインストールされたマシンの割合。

この測定値は、28 日間のスライディング ウィンドウからのテレメトリを、インストールから 3 日以内に異常なシャットダウンが報告されたマシンと、正常にインストールされたマシンの割合に集計したものです

## <a name="measure-attributes"></a>測定値の属性

|属性|Value|
|----|----|
|**オーディエンス**|小売と内部関係者|
|**期間**|28 日間のスライディング ウィンドウ|
|**測定基準**|マシンの集計|
|**最小インスタンス**|250|
|**合格基準**|50% を上回る|
|**測定 ID**|20431908|

## <a name="calculation"></a>計算

正常なインストールから 3 日以内に異常なシャットダウンを報告し (測定 20116729 で定義)、3 日前に ABS がないマシン /

正常にインストールしたマシン

