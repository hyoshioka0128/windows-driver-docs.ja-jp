---
title: Windows Server 2008 および Windows Vista SP1 での WHEA の変更点
description: Windows Server 2008 および Windows Vista SP1 での WHEA の変更点
ms.assetid: fd66ee01-e262-45c2-bced-549192b0eca3
keywords:
- Windows ハードウェア エラー アーキテクチャ WDK、Windows Server 2008 の変更
- Windows ハードウェア エラー アーキテクチャ WDK、Windows Vista SP1 の変更
- WHEA WDK、Windows Server 2008 の変更
- WHEA WDK、Windows Vista SP1 の変更
- Windows Server 2008 の WDK WHEA
- Windows Server 2008 の WDK WHEA、WHEA を変更します。
- Windows Vista SP1 の WDK WHEA
- Windows Vista SP1 WDK WHEA、WHEA の変更
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6486b0cf15fc125364549f162e9f60216a05138e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579553"
---
# <a name="whea-changes-for-windows-server-2008-and-windows-vista-sp1"></a>Windows Server 2008 および Windows Vista SP1 での WHEA の変更点


Windows Server 2008 および Windows Vista SP1 以降、次の変更が行われた Windows ハードウェア エラー アーキテクチャ (WHEA) に。

-   ハードウェア プラットフォーム ベンダーは、プラットフォーム固有の機能を使用するよう PSHED にプラグインを提供することで既定 WHEA プラットフォーム固有のハードウェア エラー ドライバー (PSHED) 機能を補うことができます。 PSHED のプラグインは、特殊な Windows デバイス ドライバー、PSHED によって呼び出されるコールバック インターフェイスを実装します。 プラグインの PSHED では、補強したり、Microsoft によって提供される PSHED の既定の動作をオーバーライドします。

    PSHED プラグインの詳細については、次を参照してください。[プラットフォームに固有のハードウェア エラー ドライバー プラグイン](platform-specific-hardware-error-driver-plug-ins2.md)します。

-   WHEA できるエラー レコードの永続化メカニズムをサポートしている[エラー レコード](error-records.md)不揮発性ストレージに格納されます。 その結果、ハードウェアの致命的なエラー条件のため、オペレーティング システムを再起動する必要がありますとエラー レコードが保持されます。 このメカニズムでは、システムが再起動したときに、ハードウェアの致命的なエラー条件に関連するエラーをキャプチャしたデータのいずれもが失われるように、エラー レコードが保持されます。

    エラー レコードの永続化の詳細については、次を参照してください。[エラー レコードの永続化メカニズム](error-record-persistence-mechanism.md)します。

-   WHEA では、ハードウェア エラーが発生したときに、Event Tracing for Windows (ETW) イベントを生成します。 Windows Server 2008 以降、WHEA ハードウェアのエラー イベントとそのハードウェアのエラー イベントを記述するデータ テンプレートは、イベントと Windows Vista でサポートされているテンプレートによって異なります。

    WHEA で ETW のサポートの詳細については、次を参照してください。[ハードウェア エラー イベント](https://msdn.microsoft.com/library/windows/hardware/ff559387)します。

-   [WHEA ハードウェア エラーのイベント処理アプリケーション](whea-hardware-error-event-processing-applications.md)WHEA によってログに記録されたイベントをクエリすることによって、システム イベント ログからハードウェアのエラー イベントを取得できます。 ただし、Windows Server 2008 以降では、WHEA ハードウェア エラーのイベント ログに記録するプロバイダーの名前が変更されました。 これらのアプリケーションは、新しいプロバイダーによってエラー イベントにアクセスする必要があります。 詳細については、次を参照してください。[のハードウェア エラー イベント、システム イベント ログを照会](querying-the-system-event-log-for-hardware-error-events.md)します。

-   WHEA のハードウェア エラーのイベントだけでなく、アプリケーションの処理[WHEA 管理アプリケーション](whea-management-applications.md)は、Windows Server 2008、Windows Vista SP1 と以降のバージョンの Windows ではサポートされています。 WHEA によって提供される WMI インターフェイス、ユーザー モード アプリケーションは、有効化またはエラーのソースを無効にしてテスト目的でハードウェア エラーを挿入するなど、WHEA 管理操作を実行できます。

 

 




