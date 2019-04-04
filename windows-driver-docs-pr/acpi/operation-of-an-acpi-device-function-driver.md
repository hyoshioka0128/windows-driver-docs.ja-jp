---
title: ACPI 関数デバイスの操作
description: ACPI 関数デバイスの操作
ms.assetid: 56c63373-5094-4ae5-a7b0-56d61e3fa9b1
keywords:
- ACPI デバイス WDK、関数のドライバーの操作
- 関数のベンダーから提供されたドライバー WDK ACPI
- ドライバー WDK ACPI、操作を関数します。
- WDM 関数ドライバー WDK ACPI、操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7d5b3a525ae6d76504249758a0bf8ec1a0ac127f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557334"
---
# <a name="operation-of-an-acpi-device-function-driver"></a>ACPI 関数デバイスの操作





このセクションでは、デバイスの ACPI 関数のベンダーから提供されたドライバーの汎用的な操作について説明します。

デバイスの ACPI 関数ドライバーとは、WDM ドライバーでは、次のことです。

-   」の説明に従って、WDM 関数ドライバーの最小要件に準拠している[Windows Driver Model](https://msdn.microsoft.com/library/windows/hardware/ff565698)します。 これには、ドライバーのエントリ ポイント、ディスパッチ ルーチン、プラグ アンド プレイ、電源管理、および Windows Management Instrumentation (WMI) が含まれます。 この基本的な機能は、汎用の操作を Windows のドライバーと ACPI デバイスに固有の操作を実装するためのフレームワークが必要です。

-   関数のドライバーと ACPI BIOS との間の通信インターフェイスは、デバイスの操作の領域をサポートしています。

    詳細については、[サポート、営業地域](supporting-an-operation-region.md)を参照してください。

-   ベンダー定義を必要に応じて、サポート*デバイス インターフェイス*と*Ioctl*デバイスを操作するその他のドライバーやユーザー モード アプリケーションが使用されます。

    詳細については、[Vendor-Defined ACPI デバイス インターフェイスを提供する](providing-a-vendor-defined-acpi-device-interface.md)を参照してください。

 

 




