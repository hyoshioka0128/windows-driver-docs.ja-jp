---
title: ACPI デバイス機能ドライバーの操作
description: ACPI デバイス機能ドライバーの操作
ms.assetid: 56c63373-5094-4ae5-a7b0-56d61e3fa9b1
keywords:
- ACPI デバイス WDK、関数のドライバーの操作
- 関数のベンダーから提供されたドライバー WDK ACPI
- ドライバー WDK ACPI、操作を関数します。
- WDM 関数ドライバー WDK ACPI、操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f837b1126b5cf520b8c38d3df88a6a0feaa581ef
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355833"
---
# <a name="operation-of-an-acpi-device-function-driver"></a>ACPI デバイス機能ドライバーの操作





このセクションでは、デバイスの ACPI 関数のベンダーから提供されたドライバーの汎用的な操作について説明します。

デバイスの ACPI 関数ドライバーとは、WDM ドライバーでは、次のことです。

-   」の説明に従って、WDM 関数ドライバーの最小要件に準拠している[Windows Driver Model](https://docs.microsoft.com/windows-hardware/drivers/kernel/windows-driver-model)します。 これには、ドライバーのエントリ ポイント、ディスパッチ ルーチン、プラグ アンド プレイ、電源管理、および Windows Management Instrumentation (WMI) が含まれます。 この基本的な機能は、汎用の操作を Windows のドライバーと ACPI デバイスに固有の操作を実装するためのフレームワークが必要です。

-   関数のドライバーと ACPI BIOS との間の通信インターフェイスは、デバイスの操作の領域をサポートしています。

    詳細については、次を参照してください。[サポート、営業地域](supporting-an-operation-region.md)します。

-   ベンダー定義を必要に応じて、サポート*デバイス インターフェイス*と*Ioctl*デバイスを操作するその他のドライバーやユーザー モード アプリケーションが使用されます。

    詳細については、次を参照してください。 [Vendor-Defined ACPI デバイス インターフェイスを提供する](providing-a-vendor-defined-acpi-device-interface.md)します。

 

 




