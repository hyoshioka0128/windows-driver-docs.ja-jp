---
title: カメラの初期化エラー率
description: この測定値は、カメラ デバイスで初期化が失敗したインスタンスの割合として、7 日間のスライディング ウィンドウからのテレメトリを集計したものです
ms.topic: article
ms.date: 05/20/2019
ms.author: paslote
author: parkeratmicrosoft
ms.localizationpriority: medium
ms.openlocfilehash: d35a4bcbbe35fa8b29863a336c3f18aff2c60381
ms.sourcegitcommit: 04da1962e34908adeca54fcf5bbfbaa456efca5f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/03/2019
ms.locfileid: "70224054"
---
# <a name="percent-of-camera-initialization-failures"></a>カメラの初期化エラー率

## <a name="description"></a>説明

マシンのカメラ デバイスにアクセスするアプリケーションをユーザーが使用するとき、カメラ機能は最初に初期化される必要があります。 この初期化が失敗すると、ユーザーはマシンのカメラを使用してコンテンツをキャプチャすることができず、初期化プロセスをやり直す必要があります。

## <a name="measure-attributes"></a>測定値の属性

|属性|Value|
|----|----|
|**オーディエンス**|標準|
|**期間**|7 日間のスライディング ウィンドウ|
|**測定基準**|インスタンスの集計|
|**最小母集団**|10 個のインスタンス|
|**合格基準**|初期化に失敗したインスタンスが 5% 以下|
|**測定 ID**|16998810|

## <a name="calculation"></a>計算

1. この測定値は、**カメラ デバイスで初期化が失敗したインスタンスの割合**として、7 日間のスライディング ウィンドウからのテレメトリを集計したものです。

   a. 一意のデバイスで、1 時間あたり 1 つの初期化インスタンスがカウントされます。

2. インスタンスの種類:

   a. "*成功した初期化イベント = 0% の失敗*"

       i. MF_CAPTURE_ENGINE_INITIALIZED with an HRESULT == 0

   b. "*失敗した初期化イベント = 100% の失敗*"

         i. MF_E_NO_CAPTURE_DEVICES_AVAILABLE
        ii. E_ACCESSDENIED
       iii. ERROR_BAD_UNIT

### <a name="final-calculation"></a>最終的な計算

"*カメラの初期化の失敗率 = すべてのインスタンスの平均*"