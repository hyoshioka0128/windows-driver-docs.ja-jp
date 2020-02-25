---
title: Microsoft Bluetooth テストプラットフォーム
description: Bluetooth テストプラットフォーム (BTP) でサポートされているハードウェア (HID)。
ms.assetid: a6beeecb-5967-4e08-bfe2-b8aae26861ad
ms.date: 2/14/2020
ms.localizationpriority: medium
ms.openlocfilehash: f068742df4ef1eb685a4ec73b716bffebc0c2bc7
ms.sourcegitcommit: d03c24342b9852013301a37e2ec95592804204f1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/21/2020
ms.locfileid: "77528932"
---
# <a name="hid-capable-peripheral-radios"></a>HID 対応の周辺機器無線 #

Bluetooth テストプラットフォーム (BTP) Traduci には、任意のラジオモジュールと通信するための12ピンコネクタが必要です。 ここに一覧表示されている HID ラジオとテクニカルは、ラジオモジュールを受け取り、必要なピンを12ピンのレイアウトに分解します。

| ラジオ | 機能 | パラメーター |
| --- | --- | --- |
| RN42 | 基本料金 (BR) オプション | rn42 (例 RunPairingTests rn42) |
| Bluefruit | 低エネルギー (LE) ラジオ | bluefruit (例 RunPairingTests bluefruit) |

## <a name="pmod-bt2-rn42-radio"></a>PMOD BT2 (RN42 radio) ##

RN42 は、キーボードやマウスなどの HID 周辺機器として動作することができる、ロービングネットワークからの基本料金 (BR) ラジオです。 現在、BTP ペアリングと HID テストでサポートされています。 詳細については、「 [Digilent](https://store.digilentinc.com/pmod-bt2-bluetooth-interface/) 」および「[**マイクロチップ**](https://www.microchip.com/wwwproducts/en/RN42)RN42 リファレンス」を参照してください。

Pmod BT2 radio は[Digilent](https://store.digilentinc.com/pmod-bt2-bluetooth-interface/)で購入できます。

### <a name="rn42-radio"></a>RN42 Radio ###

![RN42 ラジオの写真](images/RN42.png)

### <a name="bluetooth-test-platform-traduci-board-and-diligent-sled"></a>Bluetooth テストプラットフォーム Traduci ボードと入念なスレッド ###

![Digilent スレッドでの RN42 ラジオの写真](images/Traduci_and_DigilentRN42.jpg)

> [!NOTE]
> RN42 radio は、"ジュークボード" というラベルが付いた Bluetooth テストプラットフォームの Traduci ボードポートに**のみ**接続できます。

- UART データ接続
- HID プロファイルと Bluetooth データリンクをサポートします。
- 完全に認定されたクラス 2 BR Bluetooth 2.1 以降
- 小さなフォームファクター、低電力、surface マウントモジュール

## <a name="bluefruit-le-uart-friend-nrf51-radio"></a>Bluefruit LE UART Friend (nRF51 radio) ##

NRF51 は、(キーボードやマウスなどの) HID 周辺機器として動作することができる北欧半導体からの低エネルギー (LE) ラジオです。 現在、BTP ペアリングと HID テストでサポートされています。 詳細については、「 [」および「](https://www.adafruit.com/product/2479) [北欧](https://www.nordicsemi.com/Products/Low-power-short-range-wireless/nRF51822)nRF51822 リファレンス」を参照してください。

Bluefruit LE UART Friend は、 [Adafで](https://www.adafruit.com/product/2479)購入できます。

> [!NOTE]
> Bluefruit radio は、"JC" というラベルが付いた Bluetooth テストプラットフォーム Traduci ボードポートに**のみ**接続できます。

- UART データ接続
- HID およびその他の GATT ベースのサービスをサポートします。
- 完全に認定された低エネルギー Bluetooth 4.1 ラジオ
- 構成可能な ATT データベース
- 小さなフォームファクター、低電力、surface マウントモジュール
