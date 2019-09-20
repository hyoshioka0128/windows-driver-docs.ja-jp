---
title: 信号品質が 50% を超えるデバイスとアクセスポイントの上位 95% のインターネット接続エラーの割合
description: この測定値は、デバイスが Wi-Fi 経由でインターネットに接続できなかったインスタンスの割合として、7 日間のスライディング ウィンドウからのテレメトリを集計したものです。
ms.topic: article
ms.date: 05/20/2019
ms.localizationpriority: medium
ms.openlocfilehash: e9926776d8e700eadd0a1ab1fe0511e645a3e231
ms.sourcegitcommit: b33dff0fc9b5b90ee8bd07f62713c58c5f60b40f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/16/2019
ms.locfileid: "71016950"
---
# <a name="percent-of-internet-connection-failures-from-the-top-95-percent-of-device-and-access-point-pairs-that-have-greater-than-50-percent-signal-quality"></a>インターネット接続エラーの割合 (信号品質が 50% を超えるデバイスとアクセスポイントのペアの上位 95% から)

## <a name="description"></a>説明

デバイスは、アクセス ポイント (AP) に接続した後、その接続を使用して、Wi-Fi 経由でインターネットへの接続を試行できます。 ユーザーが Wi-Fi を使用してインターネットに接続できない場合、インターネット アクセス ボタンに警告アイコン (黄色地の感嘆符) が表示されます。 Wi-Fi を必要とするアプリケーションを完全に操作することはできません。

## <a name="measure-attributes"></a>測定値の属性

|属性|Value|
|----|----|
|**オーディエンス**|標準|
|**期間**|7 日|
|**測定基準**|インスタンスの集計|
|**最小インスタンス**|3,000|
|**合格基準**|Wi-Fi 経由でインターネットに接続できなかったインスタンスが 5% 以下|
|**測定 ID**|14649243|

## <a name="calculation"></a>計算

1. この測定値は、**デバイスが Wi-Fi 経由でインターネットに接続できなかったインスタンスの割合**として、7 日間のスライディング ウィンドウからのテレメトリを集計したものです。

   a. インスタンスは、マシンと一意の AP のペアリングです。この測定値は、デバイスと AP のペアごとに、1 つのデータ ポイントとして、Wi-Fi 経由によるインターネットへの接続の全試行を集計したものです。

   b. この測定値では、シグナルの強さが 50% 未満のデバイスと AP のペアは集計されません。

   c. この測定値では、接続率がデバイスと AP のペアの下位 5 パーセンタイルの範囲内にあるデバイスと AP のペアは集計されません。

2. 接続の失敗は "100" とカウントされ、接続の成功は "0" とカウントされます

### <a name="final-calculation"></a>最終的な計算

"*デバイスと AP のペアのインターネット接続失敗率 = すべてのインスタンスの平均*"