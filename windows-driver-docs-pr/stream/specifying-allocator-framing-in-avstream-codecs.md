---
title: AVStream コーデックのアロケーターのフレーム処理の指定
description: AVStream コーデックのアロケーターのフレーム処理の指定
ms.assetid: e5b042ae-9b9c-48e9-9f0c-449e205316a9
keywords:
- AVStream ハードウェアコーデックサポート WDK、アロケーターフレームの指定
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8ccb9b1481fdef6e11bd990047a60a3a434078d5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843316"
---
# <a name="specifying-allocator-framing-in-avstream-codecs"></a>AVStream コーデックのアロケーターのフレーム処理の指定


一般に、KS pin のアロケーター要件によって、AVStream によって提供されるストリーミングバッファーの物理サイズが決まります。

ただし、入力ピンはサンプルを下流に渡すだけなので、入力ピンの KSALLOCATOR\_フレーミング\_EX ([**KS\_フレーミング\_ITEM**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ks_framing_item)に指定されたバッファーサイズの要件を満たしています。**PhysicalRange**) は使用されません。 メディアの種類が設定された後も、ドライバーは入力フレームサイズを決定し、それに応じて内部構造を調整する必要があります。

ドライバーは入力ピンのフレームサイズに影響を与えることはありませんが、未処理のフレームの最大数 (KS\_フレーミング\_項目です。**フレーム**) は、pin のアロケーター要件によって異なります。 ストリーミングコンポーネント間のスムーズなデータフローの場合は、少なくとも3つの未処理のフレームをサポートする入力ピンとデコーダーフィルターを使用することをお勧めします。

[**Kspin\_記述子\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_descriptor_ex)デバイス初期化時にアロケーターフレーム情報を提供するだけでなく、ドライバーは関連する[**ksallocator\_フレーミング\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksallocator_framing_ex)構造も更新する必要があります。 この更新は、ベンダーから提供されている[*AVStrMiniPinSetDataFormat*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnkspinsetdataformat)コールバックルーチンの pin の接続メディアの種類に基づいている必要があります。

 

 




