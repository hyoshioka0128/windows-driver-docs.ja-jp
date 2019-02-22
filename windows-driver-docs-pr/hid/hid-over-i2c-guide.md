---
title: HID I2C 経由で
description: Windows 8 では、Microsoft は、Inter-Integrated 回線 (I²C) バス経由で通信するためにデバイスを許可する新しい HID ミニポート ドライバーを作成します。
ms.assetid: E8A056C0-B10F-48E2-B8E3-67B00AAC87D8
keywords:
- HID のミニポート ドライバー
- 回線の間の統合
- I2C バス
- HIDI2C.sys
- シンプルな周辺機器のバス
- SPB
- GPIO
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 06a6a6e5869eb5c95eff5bb6f5449e31d07ac975
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557691"
---
# <a name="hid-over-i2c"></a>HID I2C 経由で


Windows 8 では、Microsoft は、Inter-Integrated 回線 (I²C) バス経由で通信するためにデバイスを許可する新しい HID ミニポート ドライバーを作成します。

新しい HID ミニポート ソリューションでは、USB と Bluetooth、I²C デバイスをサポートする以外に、HID プロトコルを拡張します。 I²C は単純ですが、効率的なプロトコルであるため、電話と埋め込みのプラットフォームで 10 年以上に使用されました。 このプロトコルは、Windows 8 で HIDI2C.sys という名前のインボックス KMDF ドライバーでサポートされます。

I²C HID 経由で受信トレイのドライバーでこの結合されたサポートにより、ハードウェア メーカーが自分のデバイス ドライバーを作成する必要もありません、windows で迅速に実行を取得します。

ACPI の複数のリソースを持つシステムで正しく動作するには、次の 2 つのリソースを最初に表示する必要があります。

-   HID I²C 接続
-   デバイスの割り込み

これらのリソースを定義したら、その他の型の ACPI の他のリソースに従います。

*重要な注意事項:*

-   今日では、HID I²C ドライバーは、単純な周辺機器バス (SPB) と GPIO をサポートする SoC システムを対象とします。 将来的には、Microsoft では、SoC 以外のシステムでこのドライバーをサポートする場合があります。
-   HID I²C ドライバーは HID のすべてのクライアントをサポートするために最適化されています。
-   HID I²C ドライバーを使用すると、デバイスと、キーボード、タッチパッドのような一般的なデバイスの種類をサポートするために開発する必要があるドライバーの合計数を減らすシステム製造元タッチ画面やセンサー。
-   HID I²C ドライバーは、すべてクライアント Sku の Windows で使用可能な WinPE に含まれています。

 

 




