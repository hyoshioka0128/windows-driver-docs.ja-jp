---
title: ESRT からのファームウェアの最大再試行回数の上限を超えたマシンの割合
description: この測定値は、28 日間のスライディング ウィンドウからのテレメトリを、インストール イベントが発生したマシンに対する最大再試行回数に達したマシンの割合に集計したものです
ms.topic: article
ms.date: 10/31/2019
ms.localizationpriority: medium
ms.openlocfilehash: 68e996c34dc638c43955a3e2ef05b97d67e9cb92
ms.sourcegitcommit: 07b2926c15f4782e1914e8d3cf6c5c511a3a6111
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/14/2019
ms.locfileid: "74097490"
---
# <a name="percent-of-machines-exceeded-firmware-max-retry-limit-from-esrt"></a>ESRT からのファームウェアの最大再試行回数の上限を超えたマシンの割合

## <a name="description"></a>説明

正常にインストールされ、ファームウェアをインストールしようとして、ファームウェアの最大再試行回数 (既定値は 3) を超えたマシンの割合

この測定値は、28 日間のスライディング ウィンドウからのテレメトリを、インストール イベントが発生したマシンに対する最大再試行回数に達したマシンの割合に集計したものです

## <a name="measure-attributes"></a>測定値の属性

|属性|Value|
|----|----|
|**オーディエンス**|小売と内部関係者|
|**期間**|28 日間のスライディング ウィンドウ|
|**測定基準**|マシンの集計|
|**最小インスタンス**|200|
|**合格基準**|5% 以下|
|**測定 ID**|20116755|

## <a name="calculation"></a>計算

最大再試行回数に達したファームウェアをインストールしたマシンの数 /

ファームウェア デバイスのドライバー インストール イベントを受け入れたマシンの数

