---
title: SPB (Simple Peripheral Bus)
description: SoC integrated 回線は、単純な低-pin-数、広範に使用を行い、低電力シリアルがプラットフォームの周辺機器に接続するために相互接続します。
ms.assetid: E85BDD36-7ECE-47DB-A770-E28DA8383BA2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5df6feb0afeb28f71b737e9600d527a680947aa5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353954"
---
# <a name="simple-peripheral-bus-spb"></a>SPB (Simple Peripheral Bus)


プラットフォームの周辺機器に接続するための単純なチップ (SoC) integrated 回線する広範な使用上のシステム、低の暗証番号 (pin) を搭載し、低電力シリアルが相互接続します。 例には、I²C、SPI Uart などがあります。 SoC ベースのプラットフォームでは、Windows が単純な周辺機器 sp バス (B) のハードウェアには、一般的な抽象化に示し、この抽象化には、Advanced Configuration and Power Interface (ACPI) 名前空間からの新しいサポートが必要です。

## <a name="spb-controller-devices"></a>SPB コント ローラー デバイス


ハードウェア ベンダーが割り当てた ID と共に名前空間で識別される SPB のコント ローラー デバイス (\_HID) と、使用されるリソースのセット (\_CRS)。

### <a name="spb-namespace-objects"></a>SPB 名前空間のオブジェクト

SPB コント ローラー、および、それらに接続するための周辺機器は、ACPI に列挙されます。 シリアル バス接続リソースの記述子を使用して、それらの間の接続を説明します。 詳細については、の 6.4.3.8、「接続記述子」セクションを参照してください。、 [ACPI 5.0 仕様](https://uefi.org/specifications)します。

### <a name="spb-resource-descriptors"></a>SPB リソース記述子

GPIO 接続の場合と同様に、SPB 接続が、オペレーティング システムによって新しいリソースの記述子を使用して、使用のデバイスについて説明します。 ジェネリック シリアル バス リソース記述子は I²C 接続、SPI 接続、および UART 接続を宣言するために使用し、は、将来他シリアル バスの種類をサポートするために拡張できます。

これらの記述子のリソース テンプレートのマクロは、「19.5.55、に記載されて"I2CSerialBus (I2C シリアル バス接続リソース記述子マクロ)"、の、 [ACPI 5.0 仕様](https://uefi.org/specifications)します。

### <a name="genericserialbus-opregions"></a>GenericSerialBus OpRegions

GPIO と同様に、ACPI 5.0 定義、OpRegion SPB コント ローラー、GenericSerialBus (ACPI 5.0 仕様のセクション 5.5.2.4.5) を使用します。 GenericSerialBus OpRegions は SPBs 通信バスであるために、SPB ターゲット デバイスへのアクセスのさまざまなプロトコルをサポートしています。 詳細については、の 5.5.2.4.5.3、the GenericSerialBus プロトコル"を使用して"のセクションを参照してください。、 [ACPI 5.0 仕様](https://uefi.org/specifications)します。

多くの場合、SPBs でそのデバイスのオペレーティング システムのドライバーを使用した SPB のターゲット デバイスへのアクセスを共有する ASL コントロールのメソッドの必要があります。 これらのアクセスの同期を確実には、ACPI 5.0 は、デバイスのロック ミュー テックスを定義します (\_DLM) オブジェクト。 詳細については、の 5.7.5」セクションを参照してください、 [ACPI 5.0 仕様](https://uefi.org/specifications)します。

 

 




