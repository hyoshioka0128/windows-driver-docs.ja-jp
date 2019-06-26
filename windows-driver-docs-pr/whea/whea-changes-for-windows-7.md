---
title: Windows 7 での WHEA の変更点
description: Windows 7 での WHEA の変更点
ms.assetid: d92c2be0-732b-4fcd-b517-5cb9eccf962b
keywords:
- Windows ハードウェア エラー アーキテクチャ WDK、Windows 7 の変更
- WHEA WDK、Windows 7 の変更
- Windows 7 の WDK WHEA
- Windows 7 の WDK WHEA、WHEA の変更
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2b556a934f98db12869340f06d83ae0b46621abc
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387143"
---
# <a name="whea-changes-for-windows-7"></a>Windows 7 での WHEA の変更点


Windows 7 以降で、次の変更が加えられました Windows ハードウェア エラー アーキテクチャ (WHEA) します。

-   新しいエラー レコードの形式 ([**WHEA\_エラー\_パケット\_V2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_whea_error_packet_v2)) Windows 7 および Windows の以降のバージョンでハードウェア エラーを報告するために使用します。 以前のエラー レコードの形式 ([WHEA\_エラー\_パケット](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff560465(v=vs.85))) に変更されました[ **WHEA\_エラー\_パケット\_V1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_whea_error_packet_v1)、Windows Server 2008 および Windows Vista SP1 でのハードウェア エラーをレポートにのみ使用されます。

    以降で、Windows 7 Windows Driver Kit (WDK)、WHEA\_エラー\_パケットは、ビルド ターゲットによって参照か、WHEA マクロ\_エラー\_パケット\_V1 または WHEA\_エラー\_パケット\_V2 構造体。

    この変更の詳細については、次を参照してください。 [WHEA\_エラー\_パケット](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff560465(v=vs.85))します。

-   さまざまな Windows ハードウェア エラー アーキテクチャ (WHEA) データ型は、Windows 7 Windows Driver Kit (WDK) で名前変更されています。 これらの変更の詳細については、次を参照してください。 [WHEA データ型の名前を変更](renamed-whea-data-types.md)します。

-   WHEA では、エラー修正コード (ECC) メモリを予測的な障害の分析 (PFA) をサポートします。 PFA、を通じて WHEA は以前のエラーが発生している 1 つまたは複数の ECC メモリ ページを監視できます。 多くのエラーが発生したときに、WHEA はオフライン状態に、メモリ ページが表示しようとします。

    A[プラットフォーム固有のハードウェア エラー ドライバー (PSHED) プラグイン](platform-specific-hardware-error-driver-plug-ins2.md)ECC メモリ PFA 自体を実行することによって、WHEA の PFA サポートを拡張できます。 これにより、プラグインする必要がありますのタイミングを判断をオフライン状態に、メモリ ページを表示します。

-   WHEA エラー固有のハードウェアの他のエラーが定義されています。 これらのエラーの詳細については、次を参照してください。 [WHEA ハードウェア エラー イベント (Windows Server 2008、Windows Vista SP1 以降)](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff560537(v=vs.85))します。

 

 




