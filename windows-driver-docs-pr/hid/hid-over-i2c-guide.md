---
title: I2C での HID の概要
description: Windows 8 の場合、Microsoft では、デバイスが統合回線 (I ² C) バスを介して通信できるようにする新しい HID ミニポートドライバーを作成しました。
ms.assetid: E8A056C0-B10F-48E2-B8E3-67B00AAC87D8
keywords:
- HID ミニポートドライバー
- 統合された回線
- I2C バス
- HIDI2C.sys
- 単純な周辺機器バス
- SPB
- GPIO
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: af265af5a99022b0472d5429f5c2e35d49c3c84d
ms.sourcegitcommit: fec48fa5342d9cd4cd5ccc16aaa06e7c3d730112
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2019
ms.locfileid: "69565622"
---
# <a name="introduction-to-hid-over-i2c"></a>I2C での HID の概要


Windows 8 の場合、Microsoft では、デバイスが統合回線 (I ² C) バスを介して通信できるようにする新しい HID ミニポートドライバーを作成しました。

新しい HID ミニポートソリューションは、USB および Bluetooth 以外の HID プロトコルを拡張して、I ² C デバイスをサポートします。 I ² C は、単純かつ効率的なプロトコルで、電話および埋め込みプラットフォームで10年以上にわたって使用されています。 このプロトコルは、HIDI2C という名前の組み込みの KMDF ドライバーによって Windows 8 でサポートされています。

このように、受信トレイドライバーでは、"I ² C" を使用して、デバイスを windows 上ですばやく実行できるようになりました。ドライバーを作成する必要はありません。

複数の ACPI リソースがあるシステムで正しい動作を確保するために、次の2つのリソースが最初に表示される必要があります。

-   HID I ² C 接続
-   デバイスの割り込み

これらのリソースを定義した後は、他の種類の追加の ACPI リソースが必要になる可能性があります。

*重要な注意事項:*

-   現在、HID I ² C ドライバーは、単純な周辺機器バス (SPB) と GPIO をサポートする SoC システムを対象としています。 今後、Microsoft はこのドライバーを SoC 以外のシステムでサポートする場合があります。
-   HID I ² C ドライバーは、すべての HID クライアントをサポートするように最適化されています。
-   HID I ² C ドライバーを使用すると、デバイスとシステム製造元は、キーボード、タッチパッド向け、タッチスクリーン、センサーなどの一般的なデバイスの種類をサポートするために開発する必要のあるドライバーの合計数を減らすことができます。
-   HID I ² C ドライバーは、Windows のすべてのクライアント Sku で使用でき、WinPE に含まれています。

 

 




