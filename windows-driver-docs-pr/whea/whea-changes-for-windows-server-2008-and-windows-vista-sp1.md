---
title: Windows Server 2008 および Windows Vista SP1 での WHEA の変更点
description: Windows Server 2008 および Windows Vista SP1 での WHEA の変更点
ms.assetid: fd66ee01-e262-45c2-bced-549192b0eca3
keywords:
- Windows ハードウェアエラーアーキテクチャ WDK、Windows Server 2008 の変更
- Windows ハードウェアエラーアーキテクチャ WDK、Windows Vista SP1 の変更
- WHEA WDK、Windows Server 2008 の変更
- WHEA WDK、Windows Vista SP1 の変更
- Windows Server 2008 WDK WHEA
- Windows Server 2008 WDK WHEA、WHEA の変更
- Windows Vista SP1 WDK WHEA
- Windows Vista SP1 WDK WHEA、WHEA の変更
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4357d16df3afc9435cc1e67ebac2b6db110dda64
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845407"
---
# <a name="whea-changes-for-windows-server-2008-and-windows-vista-sp1"></a>Windows Server 2008 および Windows Vista SP1 での WHEA の変更点


Windows Server 2008 および Windows Vista SP1 以降では、Windows ハードウェアエラーアーキテクチャ (WHEA) に次の変更が加えられました。

-   ハードウェアプラットフォームのベンダーは、プラットフォーム固有の機能を使用するプラグインを提供することによって、既定の WHEA プラットフォーム固有のハードウェアエラードライバー (PSHED) 機能を補うことができます。 このプラグインは、特別な Windows デバイスドライバーであり、pshed 呼び出されるコールバックインターフェイスを実装しています。 このプラグインの目的は、Microsoft が提供する既定の動作を補強または上書きすることです。

    プラグインの詳細については、「[プラットフォーム固有のハードウェアエラードライバープラグイン](platform-specific-hardware-error-driver-plug-ins2.md)」を参照してください。

-   WHEA では、エラー[レコード](error-records.md)を不揮発性ストレージに格納できるようにする、エラーレコードの永続化メカニズムがサポートされています。 その結果、致命的なハードウェアエラー状態のためにオペレーティングシステムを再起動する必要がある場合、エラーレコードは保持されます。 このメカニズムは、システムの再起動時に、致命的なハードウェアエラー状態に関連するキャプチャされたエラーデータが失われないように、エラーレコードを保持します。

    エラーレコードの永続化の詳細については、「[エラーレコードの永続化メカニズム](error-record-persistence-mechanism.md)」を参照してください。

-   WHEA は、ハードウェアエラーが発生するたびに、Windows イベントトレーシング (ETW) イベントを発生させます。 Windows Server 2008 以降では、Windows Vista でサポートされているイベントとテンプレートとは、このハードウェアエラーイベントを説明する WHEA ハードウェアエラーイベントとデータテンプレートが異なります。

    WHEA での ETW のサポートの詳細については、「[ハードウェアエラーイベント](https://docs.microsoft.com/windows-hardware/drivers/ddi/_whea/)」を参照してください。

-   [Whea ハードウェアエラーイベント処理アプリケーション](whea-hardware-error-event-processing-applications.md)は、whea によってログに記録されたイベントを照会することによって、システムイベントログからハードウェアエラーイベントを取得できます。 ただし、Windows Server 2008 以降では、WHEA ハードウェアエラーイベントをログに記録するプロバイダーの名前が変更されています。 これらのアプリケーションは、新しいプロバイダーを通じてエラーイベントにアクセスする必要があります。 詳細については、「[ハードウェアエラーイベントのシステムイベントログのクエリ](querying-the-system-event-log-for-hardware-error-events.md)」を参照してください。

-   WHEA ハードウェアエラーイベント処理アプリケーションに加えて、windows Server 2008、Windows Vista SP1、およびそれ以降のバージョンの Windows では、 [whea 管理アプリケーション](whea-management-applications.md)がサポートされるようになりました。 ユーザーモードアプリケーションでは、WHEA によって提供される WMI インターフェイスを使用して、エラーソースの有効化または無効化や、テストのためのハードウェアエラーの挿入など、WHEA 管理操作を実行できます。

 

 




