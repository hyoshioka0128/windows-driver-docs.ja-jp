---
title: Wi-Fi 接続エラーの割合 (デバイスとアクセスポイントのペアの上位 95% から)
description: この測定値は、デバイスがアクセス ポイントに接続できなかったインスタンスの割合として、7 日間のスライディング ウィンドウからのテレメトリを集計したものです
ms.topic: article
ms.date: 05/20/2019
ms.localizationpriority: medium
ms.openlocfilehash: e8ac44992816693a18b1e8ae3d265949d74b2d5f
ms.sourcegitcommit: b33dff0fc9b5b90ee8bd07f62713c58c5f60b40f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/16/2019
ms.locfileid: "71016948"
---
# <a name="percent-of-wi-fi-connection-failures-from-the-top-95-percent-of-device-and-access-point-pairs"></a>Wi-Fi 接続エラーの割合 (デバイスとアクセスポイントのペアの上位 95% から) 

## <a name="description"></a>説明

Wi-Fi アクセス ポイント (AP) は、他の Wi-Fi 対応デバイスがワイヤレス ローカル エリア ネットワーク (WLAN) に接続できるようにするネットワーク ハードウェアです。 ユーザーが AP に接続できない場合、マシンに "*アクセス ポイントに接続できない*" という内容のエラー メッセージが表示され、WLAN や Wi-Fi にアクセスできません。

## <a name="measure-attributes"></a>測定値の属性

|属性|Value|
|----|----|
|**オーディエンス**|対象となる HWID と CHID|
|**期間**|7 日|
|**測定基準**|インスタンスの集計 |
|**最小インスタンス**|3,000|
|**合格基準**|AP に接続できなかったインスタンスが 2% 以下 |
|**測定 ID**|14642524|

## <a name="calculation"></a>計算

1. この測定値は、**デバイスが AP に接続できなかったインスタンスの割合**として、7 日間のスライディング ウィンドウからのテレメトリを集計したものです

   a. インスタンスは、デバイスと一意の AP のペアリングです。この測定値は、デバイスごとに、一意の AP への接続の全試行を集計したものです。

   b. この測定値では、シグナルの強さが 50% 未満のデバイスと AP のペアは集計されません。

   c. この測定値では、接続率がデバイスと AP のペアの下位 5 パーセンタイルの範囲内にあるデバイスと AP のペアは集計されません。

2. 接続の失敗は "100" とカウントされ、接続の成功は "0" とカウントされます

### <a name="final-calculation"></a>最終的な計算

"*デバイスと AP のペアの接続失敗率 = すべてのインスタンスの平均*"