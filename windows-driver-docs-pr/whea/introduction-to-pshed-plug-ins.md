---
title: PSHED プラグインの概要
description: PSHED プラグインの概要
ms.assetid: 31c540ec-c1d0-48e3-9eab-b458a5213f7e
keywords:
- プラットフォーム固有のハードウェア エラー ドライバー プラグインをプラットフォーム固有のハードウェア エラー ドライバー プラグインについての WDK WHEA
- プラットフォーム固有のハードウェア エラー ドライバー プラグインについての PSHED プラグイン WDK WHEA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9f864db184a687a7128a8e2dda2865dfa6ca115e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548980"
---
# <a name="introduction-to-pshed-plug-ins"></a>PSHED プラグインの概要


プラットフォーム ベンダーは、プラットフォーム固有の機能を活用するよう PSHED にプラグインを提供することで、既定の PSHED 機能を補うことができます。 PSHED のプラグインは、特殊な Windows デバイス ドライバー、PSHED によって呼び出されるコールバック インターフェイスを実装します。 プラグインの PSHED では、補強したり、Microsoft によって提供される PSHED の既定の動作をオーバーライドします。

プラグインの PSHED として実装されている、 [Windows Driver Model](https://msdn.microsoft.com/library/windows/hardware/ff565698) (WDM) ドライバーは、システムの起動時に特定のハードウェア識別子が列挙されたときに、プラグ アンド プレイ (PnP) マネージャーによって読み込まれる。 プラットフォーム ベンダーは、PSHED プラグインの読み込みを開始するハードウェア識別子を指定します。 このハードウェア識別子を ACPI 名前空間にすることができますか、別のデバイスの名前空間を指定できます。

PSHED プラグインは、ユーザー モード アプリケーションまたはより高いレベルのドライバーによって開始されたすべての I/O 要求を処理しません。 そのため、そのプラグイン PSHED がドライバー ディスパッチ ルーチンを実装するためにのみ必要です (を参照してください[ **DRIVER_DISPATCH**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)) を処理する[IRP_MJ_PNP](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-pnp)と[IRP_MJ_POWER](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power) Irp します。 PSHED プラグインは、デバイス インターフェイスを登録またはそれらのデバイス オブジェクトのシンボリック リンクを作成する必要はありません。

次の 1 つ以上が参加するプラグイン PSHED[機能領域](functional-areas.md)ハードウェア エラーの処理に関連付けられています。

-   [エラー ソースの検出](error-source-discovery.md)

-   [エラー ソースの管理](error-source-control.md)

-   [エラー レコードの永続化](error-record-persistence.md)

-   [エラー情報の取得](error-information-retrieval.md)

-   [エラーからの回復](error-recovery.md)

-   [エラーの挿入](error-injection.md)

これらの機能領域ごとに、プラグイン PSHED、PSHED によって呼び出されるコールバック関数を実装します。 プラグイン PSHED が参加し、関連付けられているコールバック関数へのポインターを提供する機能領域を指定するときに、[登録](registering-a-pshed-plug-in.md)自体、PSHED で。 複数の PSHED プラグインは、同時に、PSHED で登録できます。 ただし、プラグインの 1 つ以上の登録済み PSHED では、特定の機能領域に含まれていることを指定する場合自身を登録する最後の 1 つのみは機能領域でその参加実際にします。

PSHED のプラグインは、ハードウェア プラットフォームのハードウェアのエラー レポートと回復機能をソフトウェア インターフェイスとしてのプラットフォーム ベンダーによって実装されるものです。 PSHED のプラグインはどのようなプライベート インターフェイスを使用して、プラットフォーム ファームウェアと対話できます。 またはメカニズムは、プラットフォーム ベンダーによって定義されます。 これにより、既存のファームウェアを使用して、ハードウェア エラーの処理を続行する、プラットフォーム ベンダーができます。 時間では、Microsoft は、ハードウェア エラー レポートと回復機能を標準化することが必要です。 その時点では、一般的なエラー処理およびレポート用の PSHED プラグインの必要性が低下することなど PSHED プラグインが標準のハードウェア エラーの処理に加えて追加の値を提供するベンダー固有の機能をサポートするため必要のみになります機能。

 

 




