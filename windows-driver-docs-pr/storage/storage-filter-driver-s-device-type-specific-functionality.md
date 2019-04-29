---
title: 記憶域フィルター ドライバーのデバイスの種類に固有な機能
description: 記憶域フィルター ドライバーのデバイスの種類に固有な機能
ms.assetid: ecc0d938-e931-46bd-a1e1-0e6da8e149a4
keywords:
- 記憶域フィルター ドライバー WDK、デバイスの種類に固有の機能
- フィルター ドライバー WDK ストレージ、デバイスの種類に固有の機能
- SFD WDK の記憶域、デバイスの種類に固有の機能
- デバイスの種類に固有の機能 WDK ストレージ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bf5973213406c3fc5c29934c535205538c3bce88
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331706"
---
# <a name="storage-filter-drivers-device-type-specific-functionality"></a>記憶域フィルター ドライバーのデバイスの種類に固有な機能


## <span id="ddk_storage_filter_drivers_device_type_specific_functionality_kg"></span><span id="DDK_STORAGE_FILTER_DRIVERS_DEVICE_TYPE_SPECIFIC_FUNCTIONALITY_KG"></span>


、そのデバイスの性質によっては、記憶域フィルター ドライバー (SFD) が次のデバイスの種類に固有の機能を担当可能性があります。

-   デバイスが非標準の形式でデータを処理する場合は、ドライバーを削減する転送要求を送信する前後にまたはデバイスに固有の書式にデータを変換します。

-   I/O 制御要求のポートでドライバーでサポートされる、ドライバーの定義済みの I/O 制御の要求またはパススルー要求をそのデバイスでは、およびそれら Irp を次の下位ドライバーに送信するために必要なとして使いなれた Irp の設定

-   そのデバイスに必要なクラスのドライバーが提供される Srb の変更

-   要求のタイムアウト値を確立します。

-   1 つまたは複数を指定して[ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)ルーチン、対応する記憶域クラス ドライバーなど、特定のエラー状況と特殊なを必要とするデバイス固有の要求の再試行を処理し、処理

一般に、SFD には、それらの要求をデバイスに固有の処理を必要とする記憶域クラス ドライバーとして同じ責任があります。 記憶域クラス ドライバーの必要な機能の詳細については、次を参照してください。[ストレージ クラス ドライバー](storage-class-drivers.md)します。

 

 




