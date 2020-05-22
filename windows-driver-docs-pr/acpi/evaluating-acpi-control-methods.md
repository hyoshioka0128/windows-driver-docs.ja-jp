---
title: ACPI 制御メソッドを評価する
description: ACPI 制御メソッドを評価する
ms.assetid: 00cf7530-30e6-4ff2-8a26-1c5143413b56
keywords:
- ACPI 制御方法 WDK、評価
- ACPI デバイス WDK、制御メソッドの評価
ms.date: 05/19/2020
ms.localizationpriority: medium
ms.openlocfilehash: 64e0c3ad53716d432919d5789b387e68262184be
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769372"
---
# <a name="evaluating-acpi-control-methods"></a>ACPI 制御メソッドを評価する

Advanced Configuration and Power Interface (ACPI) の制御方法は、システムハードウェアを照会および構成するための操作を宣言して定義するソフトウェアです。 ACPI 互換システムには、最小限の制御メソッドが用意されています。 コントロールメソッドは、acpi ソース言語 (ASL) で記述されており、ASL コンパイラによって acpi コンピューター言語 (AML) にコンパイルされ、システムファームウェアから ACPI 名前空間に読み込まれ、ACPI ドライバーによって解釈されます。

カーネルモードデバイスドライバーは、読み込まれるカーネルモードドライバーフレームワーク (KMDF) の要件に準拠しています。 ACPI で列挙されたデバイスのデバイススタックに読み込まれたドライバーの場合、ACPI ドライバーは常に、デバイススタックで PDO を作成および操作するバスドライバーです。 この機能には、親デバイスの子孫である子オブジェクトによってサポートされる制御メソッドの評価が含まれます。

ドライバーは、次のいずれかの[**IRP \_ MJ \_ デバイス \_ 制御**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)要求をデバイスに送信することによって、制御メソッドを評価します。

- [**IOCTL \_ ACPI \_ EVAL \_ メソッド**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ni-acpiioct-ioctl_acpi_eval_method)

    この要求は、要求が送信されたデバイスでサポートされている制御メソッドを同期的に評価します。 この IOCTL を使用するために、デバイスのドライバーは、入力および出力メソッドの引数バッファー、メソッドの名前、および要求の完了を待機するイベントオブジェクトを提供します。 メソッドは、要求を送信するデバイスの ACPI 名前空間の直下の子オブジェクトである必要があります。

- [**IOCTL \_ ACPI \_ 非同期 \_ EVAL \_ メソッド**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ni-acpiioct-ioctl_acpi_async_eval_method)

    この要求は、要求の送信先となるデバイスでサポートされているコントロールメソッドを非同期に評価します。 この IOCTL を使用するために、デバイスのドライバーは、入力および出力メソッドの引数バッファー、メソッドの名前、およびすべての下位レベルのドライバーが要求を完了した後に i/o マネージャーが呼び出す*Iocompletion*ルーチンを提供します。 メソッドは、要求を送信するデバイスの ACPI 名前空間の直下の子オブジェクトである必要があります。

- [**IOCTL \_ ACPI \_ EVAL \_ メソッド \_ EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ni-acpiioct-ioctl_acpi_eval_method_ex)

    この要求は、デバイスによってサポートされているコントロールメソッドまたは要求が送信されたデバイスの子子オブジェクトを同期的に評価します。 この IOCTL を使用するために、デバイスのドライバーは、入力および出力メソッドの引数バッファー、デバイスの ACPI 名前空間の制御メソッドのパスと名前、および要求の完了を待機するイベントオブジェクトを提供します。

- [**IOCTL \_ ACPI \_ 非同期 \_ EVAL \_ メソッド \_ EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ni-acpiioct-ioctl_acpi_async_eval_method_ex)

    この要求は、デバイスによってサポートされているコントロールメソッドまたは要求が送信されたデバイスの子子オブジェクトを非同期に評価します。 この IOCTL を使用するために、デバイスのドライバーは、入力および出力メソッドの引数バッファー、デバイスの ACPI 名前空間の制御メソッドのパスと名前、およびすべての下位レベルのドライバーが要求を完了した後に i/o マネージャーが呼び出す*Iocompletion*ルーチンを提供します。

ACPI コントロールメソッドを同期的に評価する方法の詳細については、「 [Acpi 制御メソッドを同期的に評価](evaluating-acpi-control-methods-synchronously.md)する」を参照してください。 ACPI コントロールメソッドを非同期的に評価する方法の詳細については、「 [**ioctl \_ acpi \_ 非同期 \_ eval \_ メソッド**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ni-acpiioct-ioctl_acpi_async_eval_method)」と「 [**ioctl \_ acpi \_ 非同期 \_ eval \_ メソッド \_ EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ni-acpiioct-ioctl_acpi_async_eval_method_ex)」を参照してください。

デバイスのドライバーが、デバイスの直接の子オブジェクトではないコントロールメソッドを評価する場合、ドライバーはデバイスの ACPI 名前空間のメソッドのパスと名前を指定する必要があります。 Windows では、デバイスの子オブジェクトのパスと名前を取得するために、 [**IOCTL \_ ACPI \_ ENUM \_ CHILDREN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ni-acpiioct-ioctl_acpi_enum_children)要求をサポートしています。これは、デバイスのドライバーが以下を列挙するために使用できます。

- デバイスとその直接の子デバイス。

- デバイスとその子デバイスすべて。

- 指定された名前の子オブジェクトを、デバイスの ACPI 名前空間に追加します (特に制御メソッドを含む)。

デバイスの名前空間のデバイスとメソッドを列挙する方法の詳細については、「[子デバイスの列挙と制御メソッド](enumerating-child-devices-and-control-methods.md)」を参照してください。

コントロールメソッドを評価するためにドライバーで使用できるシステム指定のマクロの詳細については、「[コントロールメソッドマクロ](control-method-macros.md)」を参照してください。

ACPI デバイス、制御メソッド、および名前空間の詳細については、「[高度な構成と電源インターフェイスの仕様](https://uefi.org/specifications)」を参照してください。
