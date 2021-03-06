---
title: ACPI 設計ガイド
description: このセクションでは、デバイス ドライバーと Advanced Configuration and Power Interface (ACPI) デバイスのインターフェイス方法について説明します。 ACPI デバイスは、Advanced Configuration and Power Interface (ACPI) 仕様で定義されています。
ms.assetid: 294f4b43-2b3e-4afa-8fa8-74a6719131c7
ms.date: 01/24/2018
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.openlocfilehash: 103ede5b9929de69855e4c530240dcc5ef13f48b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328819"
---
# <a name="acpi-design-guide"></a>ACPI 設計ガイド


このセクションでは、デバイス ドライバーと Advanced Configuration and Power Interface (ACPI) デバイスのインターフェイス方法について説明します。 ACPI デバイスは、[Advanced Configuration and Power Interface (ACPI) 仕様](https://go.microsoft.com/fwlink/p/?linkid=866846)で定義されています。

## <a name="in-this-section"></a>このセクションの内容


| セクション | 説明 |
| --- | --- |
| [ACPI デバイスのサポート](supporting-acpi-devices.md) | Windows Driver Model (WDM) 関数ドライバーを使用して ACPI デバイスの機能を強化する方法について説明します。 |
| [ACPI 制御メソッドの評価](evaluating-acpi-control-methods.md) | [Kernel-Mode Driver Framework (KMDF)](https://docs.microsoft.com/windows-hardware/drivers/kernel)、[User-Mode Driver Framework (UMDF)](https://docs.microsoft.com/windows-hardware/drivers/wdf/getting-started-with-umdf-version-2)、または [Windows Driver Model (WDM)](https://docs.microsoft.com/windows-hardware/drivers/kernel/windows-driver-model) の要件に準拠するデバイス ドライバーで、ACPI 制御メソッドを評価する方法について説明します。 |
| [_OSI を使用して ACPI で Windows バージョンを識別する方法](winacpi-osi.md) | ホスト オペレーティング システムの識別に使用される ACPI ソース言語 (ASL) のオペレーティング システム インターフェイス レベル (\_OSI) メソッドについて説明します。 |


## <a name="related-sctions"></a>関連するセクション

-   [ACPI DDI リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_acpi)

 



