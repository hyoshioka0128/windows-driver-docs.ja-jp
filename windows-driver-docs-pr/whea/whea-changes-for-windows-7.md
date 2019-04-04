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
ms.openlocfilehash: 213e7015a20186da329760fac190eb3949789a2b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571684"
---
# <a name="whea-changes-for-windows-7"></a>Windows 7 での WHEA の変更点


Windows 7 以降で、次の変更が加えられました Windows ハードウェア エラー アーキテクチャ (WHEA) します。

-   新しいエラー レコードの形式 ([**WHEA\_エラー\_パケット\_V2**](https://msdn.microsoft.com/library/windows/hardware/ff560480)) Windows 7 および Windows の以降のバージョンでハードウェア エラーを報告するために使用します。 以前のエラー レコードの形式 ([WHEA\_エラー\_パケット](https://msdn.microsoft.com/library/windows/hardware/ff560465)) に変更されました[ **WHEA\_エラー\_パケット\_V1**](https://msdn.microsoft.com/library/windows/hardware/ff560476)、Windows Server 2008 および Windows Vista SP1 でのハードウェア エラーをレポートにのみ使用されます。

    以降で、Windows 7 Windows Driver Kit (WDK)、WHEA\_エラー\_パケットは、ビルド ターゲットによって参照か、WHEA マクロ\_エラー\_パケット\_V1 または WHEA\_エラー\_パケット\_V2 構造体。

    この変更の詳細については、[WHEA\_エラー\_パケット](https://msdn.microsoft.com/library/windows/hardware/ff560465)を参照してください。

-   さまざまな Windows ハードウェア エラー アーキテクチャ (WHEA) データ型は、Windows 7 Windows Driver Kit (WDK) で名前変更されています。 これらの変更の詳細については、[WHEA データ型の名前を変更](renamed-whea-data-types.md)を参照してください。

-   WHEA では、エラー修正コード (ECC) メモリを予測的な障害の分析 (PFA) をサポートします。 PFA、を通じて WHEA は以前のエラーが発生している 1 つまたは複数の ECC メモリ ページを監視できます。 多くのエラーが発生したときに、WHEA はオフライン状態に、メモリ ページが表示しようとします。

    A[プラットフォーム固有のハードウェア エラー ドライバー (PSHED) プラグイン](platform-specific-hardware-error-driver-plug-ins2.md)ECC メモリ PFA 自体を実行することによって、WHEA の PFA サポートを拡張できます。 これにより、プラグインする必要がありますのタイミングを判断をオフライン状態に、メモリ ページを表示します。

-   WHEA エラー固有のハードウェアの他のエラーが定義されています。 これらのエラーの詳細については、[WHEA ハードウェア エラー イベント (Windows Server 2008、Windows Vista SP1 以降)](https://msdn.microsoft.com/library/windows/hardware/ff560537)を参照してください。

 

 




