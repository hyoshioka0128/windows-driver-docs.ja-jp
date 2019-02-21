---
title: アロケーター AVStream コーデックでフレームを指定します。
description: アロケーター AVStream コーデックでフレームを指定します。
ms.assetid: e5b042ae-9b9c-48e9-9f0c-449e205316a9
keywords:
- AVStream ハードウェア コーデック サポート WDK を指定するアロケーターのフレーム化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 18555ff315f8d963aa5ec7290cc0c5a8f267cba8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538152"
---
# <a name="specifying-allocator-framing-in-avstream-codecs"></a>アロケーター AVStream コーデックでフレームを指定します。


一般に、KS 暗証番号 (pin) のアロケーターの要件は、ストリーム AVStream によって提供されるバッファーの実際のサイズを決定します。

ただし、ピン留めだけでパスを入力するためのサンプル、ダウン ストリーム入力ピンの KSALLOCATOR で指定されたバッファー サイズ要件\_フレーム\_EX ([**KS\_フレーム\_項目**](https://msdn.microsoft.com/library/windows/hardware/ff567646).**PhysicalRange**) は使用されません。 メディアの種類が設定されているし、その内部構造を必要に応じて調整した後、ドライバーも入力フレーム サイズを確認する必要があります。

ドライバーは、入力フレーム サイズを与えることはできませんが、ピン留め、未処理のフレームの最大数 (KS\_フレーム\_項目 **。フレーム**) は、pin のアロケーターの要件に依存します。 ストリーミングのコンポーネントと少ない故障の間でスムーズなデータ フローは、ことをお勧めするエンコーダーとデコーダーの両方のフィルターには、入力し、出力ピンを未処理の 3 つのフレームの最小値をサポートします。

アロケーターのフレームの情報を提供することに加えて、 [ **KSPIN\_記述子\_EX** ](https://msdn.microsoft.com/library/windows/hardware/ff563534)デバイスの初期化時に、ドライバーの更新も関連[**KSALLOCATOR\_フレーム\_EX** ](https://msdn.microsoft.com/library/windows/hardware/ff560982)構造体。 この更新プログラムは、ベンダーから提供されたに暗証番号 (pin) の接続のメディアの種類に基づく必要が[ *AVStrMiniPinSetDataFormat* ](https://msdn.microsoft.com/library/windows/hardware/ff556355)コールバック ルーチン。

 

 




