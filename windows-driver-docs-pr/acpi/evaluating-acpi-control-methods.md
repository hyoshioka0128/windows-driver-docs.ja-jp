---
title: ACPI の制御メソッドを評価します。
description: ACPI の制御メソッドを評価します。
ms.assetid: 00cf7530-30e6-4ff2-8a26-1c5143413b56
keywords:
- ACPI の制御方法、WDK を評価します。
- ACPI デバイス WDK、コントロールのメソッドを評価します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6d235720a377df453cd50abda856e30de7f3c1c2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530642"
---
# <a name="evaluating-acpi-control-methods"></a>ACPI の制御メソッドを評価します。


Advanced Configuration and Power Interface (ACPI) の制御メソッドは、宣言し、クエリを実行して、システムのハードウェアを構成する操作を定義するソフトウェアです。 ACPI と互換性のあるシステムでは、最低限の制御メソッドを提供します。 制御メソッドは、ACPI ソース言語 (ASL) で記述された、ACPI 機械語 (AML) に、ASL コンパイラによってコンパイル、ACPI 名前空間にシステム ファームウェアから読み込まれる、および ACPI ドライバーによって解釈されるは。

カーネル モード デバイス ドライバーのカーネル モード ドライバー フレームワーク (KMDF) が読み込まれている要件に適合します。 ACPI 列挙されたデバイスのデバイス スタックで読み込まれるドライバー、ACPI ドライバーは常に値が、バス ドライバー作成し、PDO デバイス スタックでの動作をします。 この機能には、親デバイスの子孫である子オブジェクトでサポートされているコントロールのメソッドの評価が含まれています。

ドライバーは、次のいずれかを送信することによって制御メソッドを評価[ **IRP\_MJ\_デバイス\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff550744)デバイスへの要求。

-   [**IOCTL\_ACPI\_EVAL\_メソッド**](https://msdn.microsoft.com/library/windows/hardware/ff536148)

    この要求は、要求を送信するデバイスでサポートされているコントロールのメソッドを同期的に評価します。 この IOCTL を使用するには、デバイスのドライバーは、入力と出力のメソッド引数のバッファー、メソッド、および要求の完了を待機するイベント オブジェクトの名前を提供します。 メソッドは、要求を送信するデバイスの ACPI 名前空間で直接の子オブジェクトである必要があります。

-   [**IOCTL\_ACPI\_ASYNC\_EVAL\_メソッド**](https://msdn.microsoft.com/library/windows/hardware/ff536145)

    この要求は、非同期的に要求を送信するデバイスでサポートされているコントロールのメソッドを評価します。 デバイスは、メソッドの名前、入力と出力のメソッド引数バッファーを提供する場合は、この IOCTL では、ドライバーを使用して、 *IoCompletion*下位レベルのすべてのドライバーが要求を完了した後、I/O マネージャーを呼び出すルーチン。 メソッドは、要求を送信するデバイスの ACPI 名前空間で直接の子オブジェクトである必要があります。

-   [**IOCTL\_ACPI\_EVAL\_メソッド\_例**](https://msdn.microsoft.com/library/windows/hardware/ff536149)

    この要求が同期的に、デバイスまたはデバイスの子オブジェクトでサポートされているコントロールのメソッドを評価する、要求が送信されます。 この IOCTL を使用するには、デバイスのドライバーは、入力と出力のメソッド引数のバッファー、パスおよび要求の完了を待機するイベント オブジェクトと、デバイスの ACPI 名前空間管理メソッドの名前を提供します。

-   [**IOCTL\_ACPI\_ASYNC\_EVAL\_メソッド\_例**](https://msdn.microsoft.com/library/windows/hardware/ff536146)

    この要求は、デバイスまたはデバイスの子オブジェクトでサポートされているコントロールのメソッドを非同期的に評価する、要求が送信されます。 デバイスは、入力と出力のメソッド引数のバッファー、パスと、デバイスの ACPI 名前空間管理メソッドの名前を提供する場合は、この IOCTL では、ドライバーを使用して、 *IoCompletion* I/O マネージャーをすべて呼び出すルーチン下位レベルのドライバーは、要求が完了しました。

ACPI の制御メソッドを同期的に評価する方法の詳細については、[ACPI コントロールのメソッドを同期的評価](evaluating-acpi-control-methods-synchronously.md)を参照してください。 ACPI の制御メソッドを非同期に評価する方法の詳細については、次を参照してください[ **IOCTL\_ACPI\_ASYNC\_EVAL\_メソッド**](https://msdn.microsoft.com/library/windows/hardware/ff536145)と。[**IOCTL\_ACPI\_ASYNC\_EVAL\_メソッド\_EX**](https://msdn.microsoft.com/library/windows/hardware/ff536146)します。

デバイスの直接の子オブジェクトではないの制御方法を評価するデバイスのドライバーの場合、ドライバーは、デバイスの ACPI 名前空間内のメソッドの名前とパスを指定する必要があります。 デバイスの子オブジェクトの名前とパスを取得するには、Windows のサポート、 [ **IOCTL\_ACPI\_列挙\_子**](https://msdn.microsoft.com/library/windows/hardware/ff536147)要求する場合に、このデバイスのドライバー次の列挙を使用できます。

-   デバイスは、その直接の子デバイス。

-   デバイスは、すべての子デバイス。

-   デバイスなどの ACPI 名前空間に指定された名前の子オブジェクトは、具体的には、方法を制御します。

デバイスとデバイスの名前空間のメソッドを列挙する方法については、[列挙子のデバイスとコントロール メソッド](enumerating-child-devices-and-control-methods.md)を参照してください。

ドライバーは、コントロールのメソッドを評価するために使用できるシステム提供のマクロについては、[コントロール メソッド マクロ](control-method-macros.md)を参照してください。

ACPI デバイス、コントロールのメソッド、および名前空間の詳細については、、 [Advanced Configuration and Power Interface Specification](https://go.microsoft.com/fwlink/p/?linkid=866846)を参照してください。
