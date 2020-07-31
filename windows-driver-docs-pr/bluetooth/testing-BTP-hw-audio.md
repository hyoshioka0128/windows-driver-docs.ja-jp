---
title: Microsoft Bluetooth テストプラットフォーム-オーディオ対応の周辺機器無線
description: Bluetooth テストプラットフォーム (BTP) でサポートされているハードウェア (オーディオ)。
ms.assetid: a6beeecb-5967-4e08-bfe2-b8aae26861ad
ms.date: 2/14/2020
ms.localizationpriority: medium
ms.openlocfilehash: a0e32fd4bb85ce12fe403499198857773235af85
ms.sourcegitcommit: 7a7ce6070ed16673108cc64c33b3ddb894453cfb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/29/2020
ms.locfileid: "87412527"
---
# <a name="audio-capable-peripheral-radios"></a>オーディオ対応周辺機器無線

Bluetooth テストプラットフォーム (BTP) Traduci ボードには、任意のラジオモジュールと通信するための12ピンコネクタが必要です。 ここに一覧表示されているオーディオラジオとテクニカルは、ラジオモジュールを受け取り、必要な pin を必要な12ピンレイアウトに分解します。

| ラジオ | 機能 | パラメーター |
| --- | --- | --- |
| RN52 | 基本料金 (BR) オプション | rn52 (例 RunPairingTests.bat rn52) |

## <a name="audio-sled-rn52-radio"></a>オーディオスレッド (RN52 radio)

RN52 は、スピーカーやヘッドセットなどのオーディオ周辺機器として動作することができる、ロービングネットワークからの基本料金 (BR) ラジオです。 現在、今後の BTP オーディオテストのサポートが予定されています。 詳細については、「RN52」 ([**マイクロチップ**](https://www.microchip.com/wwwproducts/en/RN52)) のページを参照してください。 このスレッドでは、無線からのオーディオ出力データを分割し、検証を支援するために Traduci 上のオーディオコーデックとオーディオ処理 FPGA にルーティングします。

### <a name="rn52-radio"></a>RN52 Radio

![RN52 ラジオの写真](images/RN52.png)

### <a name="rn52-radio-on-btp-compatible-sled"></a>BTP 互換スレッドでの RN52 Radio

![スレッドの RN52 ラジオの写真](images/Traduci_and_RN52.jpg)

> [!NOTE]
> RN52 radio は、"JA" というラベルが付いた Traduci board 12 ピンのポートに**のみ**接続できます。

- ソフトウェアを構成する AT コマンドを使用した UART データ接続
- SPP、A2DP、HFP、および AVRCP プロファイルをサポートします。
- バージョン3.0 オーディオモジュール
- 完全に認定されたクラス 2 BR Bluetooth 2.1 + EDR
- 小さなフォームファクター、低電力、surface マウントモジュール
