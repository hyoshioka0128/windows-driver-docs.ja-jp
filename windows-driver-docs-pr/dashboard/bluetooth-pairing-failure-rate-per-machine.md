---
title: Bluetooth ペアリング エラー率
description: ''
ms.topic: article
ms.date: 05/20/2019
ms.localizationpriority: medium
ms.openlocfilehash: 85ec8300e547130bdd9b665175e41a1a12022ac8
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "71017084"
---
# <a name="percent-of-bluetooth-pairing-failures"></a>Bluetooth ペアリング エラー率

## <a name="description"></a>説明

Bluetooth ペアリングが成功すると、将来の使用に備えて認証情報がローカルに保存されます。 デバイスでペアリングを実行できない場合、ユーザーは接続を認証できず、デバイス間でコンテンツをストリーム配信できません。

## <a name="measure-attributes"></a>測定値の属性

|属性|値|
|----|----|
|**オーディエンス**|Standard|
|**期間**|7 日間のスライディング ウィンドウ|
|**測定基準**|インスタンスの集計|
|**最小母集団**|10 個のインスタンス|
|**合格基準**|ペアリングに失敗するインスタンスが 5% 以下|
|**測定 ID**|14612509|

## <a name="calculation"></a>計算

1. この測定値は、**Bluetooth デバイスが別のデバイスとのペアリングに失敗したインスタンスの割合**として、7 日間のスライディング ウィンドウからのテレメトリを集計したものです。

   a。 "*この測定では、単一のマシンで複数のペアリング インスタンスがカウントされる場合があります*"

2. インスタンスの種類:

   a。 "*ペアリングの成功イベント = 0% の失敗*"

   b. "*ペアリングのキャンセル イベントまたはニュートラルなペアリング = 5% の失敗*"

   c. "*タイムアウト = 20% の失敗*"

   d. "*ペアリングの失敗イベント = 100% の失敗*"

### <a name="final-calculation"></a>最終的な計算

"*Bluetooth ペアリングの失敗率 = すべてのインスタンスの平均*"