---
title: Bluetooth 接続エラー率
description: この測定値は、Bluetooth デバイスが別のデバイスとの接続に失敗したインスタンスの割合として、7 日間のスライディング ウィンドウからのテレメトリを集計したものです。
ms.topic: article
ms.date: 05/20/2019
ms.localizationpriority: medium
ms.openlocfilehash: f7df03da49a8be8b7119aafe4ff6da97b1e90349
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "71017088"
---
# <a name="percent-of-bluetooth-connection-failures"></a>Bluetooth 接続エラー率

## <a name="description"></a>説明

2 つのデバイスが Bluetooth で接続できない場合、ユーザーは他方のデバイスとコンテンツの送受信を行えません。 切断状態は、デバイス間に通信の問題があることを示唆している可能性もあります。 この測定値では Bluetooth 接続の失敗率を計算します。

## <a name="measure-attributes"></a>測定値の属性

|属性|値|
|----|----|
|**オーディエンス**|Standard|
|**期間**|7 日間のスライディング ウィンドウ|
|**測定基準**|インスタンスの集計|
|**最小母集団**|10 個のインスタンス|
|**合格基準**|接続に失敗したインスタンスが 10% 未満|
|**測定 ID**|13897278|

## <a name="calculation"></a>計算

1. この測定値は、**Bluetooth デバイスが別のデバイスとの接続に失敗したインスタンスの割合**として、7 日間のスライディング ウィンドウからのテレメトリを集計したものです。

   a。 この測定では、単一のデバイスで複数のペアリング インスタンスがカウントされる場合があります

2. インスタンスの種類:

   a。 "*成功した接続または切断イベント = 0% の失敗*"

   b. "*接続の失敗または切断の成功 = 100% の失敗*"

### <a name="final-calculation"></a>最終的な計算

"*Bluetooth 接続の失敗率 = すべてのインスタンスの平均*"