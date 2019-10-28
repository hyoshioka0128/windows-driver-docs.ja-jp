---
title: Windows 7 での WHEA の変更点
description: Windows 7 での WHEA の変更点
ms.assetid: d92c2be0-732b-4fcd-b517-5cb9eccf962b
keywords:
- Windows ハードウェアエラーアーキテクチャ WDK、Windows 7 の変更
- WHEA WDK、Windows 7 の変更
- Windows 7 WDK WHEA
- Windows 7 WDK WHEA、WHEA の変更
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 57e38c7bbed34a379b6d1d42acbb64ce178c8f9d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843281"
---
# <a name="whea-changes-for-windows-7"></a>Windows 7 での WHEA の変更点


Windows 7 以降では、Windows ハードウェアエラーアーキテクチャ (WHEA) に対して次の変更が加えられました。

-   Windows 7 以降のバージョンの Windows でハードウェアエラーを報告するために、新しいエラーレコード形式 ([**WHEA\_エラー\_パケット\_V2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_whea_error_packet_v2)) が使用されています。 前のエラーレコード形式 ([whea\_エラー\_パケット](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff560465(v=vs.85))) が[**whea\_エラー\_パケット\_V1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_whea_error_packet_v1)に変更され、Windows Server 2008 および windows Vista SP1 でハードウェアエラーを報告するためにのみ使用されています。

    Windows 7 Windows Driver Kit (WDK)、WHEA\_エラー\_パケットはマクロです。これは、ビルドターゲットに応じて、WHEA\_エラー\_パケット\_V1 または WHEA\_エラー\_パケット @no__t_ を参照しています。7_ V2 構造体。

    この変更の詳細については、「 [WHEA\_エラー\_パケット](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff560465(v=vs.85))」を参照してください。

-   Windows 7 Windows Driver Kit (WDK) では、さまざまな Windows ハードウェアエラーアーキテクチャ (WHEA) のデータ型の名前が変更されています。 これらの変更の詳細については、「 [WHEA データ型の名前変更](renamed-whea-data-types.md)」を参照してください。

-   WHEA では、エラー修正コード (ECC) メモリの予測エラー分析 (PFA) がサポートされています。 PFA を通じて、WHEA は、以前のエラーが発生した1つまたは複数の ECC メモリページを監視できます。 発生したエラーが多すぎると、WHEA はメモリページをオフライン状態にしようとします。

    [プラットフォーム固有のハードウェアエラードライバー (pshed) プラグイン](platform-specific-hardware-error-driver-plug-ins2.md)は、ECC メモリで pshed 自体を実行することで、WHEA の pshed サポートを拡張できます。 このようにして、プラグインは、メモリページをオフライン状態にするタイミングを決定する必要があります。

-   追加の WHEA エラー固有のハードウェアエラーが定義されています。 これらのエラーの詳細については、「 [WHEA ハードウェアエラーイベント (Windows Server 2008、Windows VISTA SP1 以降)](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff560537(v=vs.85))」を参照してください。

 

 




