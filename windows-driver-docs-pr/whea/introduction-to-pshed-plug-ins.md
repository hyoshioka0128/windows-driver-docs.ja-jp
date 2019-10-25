---
title: PSHED プラグインの概要
description: PSHED プラグインの概要
ms.assetid: 31c540ec-c1d0-48e3-9eab-b458a5213f7e
keywords:
- プラットフォーム固有のハードウェアエラードライバープラグイン WDK WHEA、プラットフォーム固有のハードウェアエラードライバープラグインについて
- 自己のプラグイン WDK WHEA、プラットフォーム固有のハードウェアエラードライバープラグインについて
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ee857070490c7c2888bea13bd1eab17b58a1e117
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844397"
---
# <a name="introduction-to-pshed-plug-ins"></a>PSHED プラグインの概要


プラットフォームベンダーは、プラットフォーム固有の機能を利用するプラグインを提供することで、既定の機能を補完できます。 このプラグインは、特別な用途を持つ Windows デバイスドライバーであり、pshed 呼び出されるコールバックインターフェイスを実装しています。 このプラグインの目的は、Microsoft が提供する既定の動作を拡張または上書きすることです。

システムの起動時に特定のハードウェア識別子が列挙されると、プラグアンドプレイ (PnP) マネージャーによって読み込まれる[Windows Driver Model](https://docs.microsoft.com/windows-hardware/drivers/kernel/windows-driver-model) (WDM) デバイスドライバーとして実装されます。 プラットフォームベンダは、PSHED プラグインの読み込みを開始するハードウェア識別子を指定します。 このハードウェア識別子は、ACPI 名前空間内にある場合も、別のデバイスの名前空間にある場合もあります。

ユーザーモードアプリケーションまたは上位レベルのドライバーによって開始された i/o 要求は、プラグインによって処理されません。 そのため、 [IRP_MJ_PNP](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-pnp)と[IRP_MJ_POWER](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power)の irp を処理するには、ドライバーディスパッチルーチン ( [**DRIVER_DISPATCH**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)を参照) を実装する必要があります。 プラグインでは、デバイスインターフェイスを登録したり、デバイスオブジェクトのシンボリックリンクを作成したりする必要はありません。

このプラグインは、ハードウェアエラーの処理に関連する次の[機能領域](functional-areas.md)の1つまたは複数に関与します。

-   [エラーソースの検出](error-source-discovery.md)

-   [ソース管理のエラー](error-source-control.md)

-   [エラーレコードの永続化](error-record-persistence.md)

-   [エラー情報の取得](error-information-retrieval.md)

-   [エラー回復](error-recovery.md)

-   [エラー挿入](error-injection.md)

これらの各機能領域では、pshed プラグインによって呼び出されるコールバック関数が実装されています。 プラグインは、それが参加する機能領域を指定し、関連付けら[れている](registering-a-pshed-plug-in.md)コールバック関数へのポインターを提供します。 複数のプラグインを同時に登録することができます。 ただし、複数の登録済みの PSHED プラグインが特定の機能領域に参加することを指定した場合、最後に登録されたプラグインだけが、実際にはその機能領域に参加します。

このプラグインは、ハードウェアプラットフォームのハードウェアエラー報告と回復機能へのソフトウェアインターフェイスとしてプラットフォームベンダーによって実装されることを目的としています。 プラットフォームベンダーによって定義されているプライベートインターフェイスまたはメカニズムを使用して、プラットフォームファームウェアとのインターフェイスを提供できます。 これにより、プラットフォームベンダーは、ハードウェアエラー処理に既存のファームウェアを引き続き使用できます。 Microsoft では、より多くのハードウェアエラー報告と復旧機能が標準化されることを期待しています。 その時点で、一般的なエラー処理とレポートのためのプラグインが必要になるため、標準のハードウェアエラー処理を超える追加の価値を提供するベンダー固有の機能をサポートするためにのみ、プラグインが必要になります。機.

 

 




