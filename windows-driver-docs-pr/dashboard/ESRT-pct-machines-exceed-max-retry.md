---
title: ESRT からのファームウェアの最大再試行回数の上限を超えたマシンの割合
description: この測定値は、28 日間のスライディング ウィンドウからのテレメトリを、インストール イベントが発生したマシンに対する最大再試行回数に達したマシンの割合に集計したものです
ms.topic: article
ms.date: 10/31/2019
ms.localizationpriority: medium
ms.openlocfilehash: d4f59740ce37d92e4e1032ae4db4cec32fa6f332
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "79083140"
---
# <a name="percent-of-machines-exceeded-firmware-max-retry-limit-from-esrt"></a>ESRT からのファームウェアの最大再試行回数の上限を超えたマシンの割合

## <a name="description"></a>説明

正常にインストールされ、ファームウェアをインストールしようとして、ファームウェアの最大再試行回数 (既定値は 3) を超えたマシンの割合。

この測定値は、28 日間のスライディング ウィンドウからのテレメトリを、インストール イベントが発生したマシンに対する最大再試行回数に達したマシンの割合に集計したものです。

報告された ESRT のバージョンが、インストール前のマシン上の以前のバージョンと同じであるため、この測定値に失敗する多くのファームウェアは、ESRT LastAttemptStatus フィールドがエラー コードを報告していないコントラクトに準拠していません。 

[このドキュメントのセクション 3](https://docs.microsoft.com/windows-hardware/manufacture/desktop/validating-windows-uefi-firmware-update-platform-functionality) では、ファームウェアの実装がこの要件を満たしていることを確認するための基本的な検証シナリオについて説明します。  

## <a name="measure-attributes"></a>測定値の属性

|属性|値|
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

