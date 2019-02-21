---
title: フィルター モジュールの開始
description: フィルター モジュールの開始
ms.assetid: 493cb922-22bc-4845-b5a2-6f610559534d
keywords:
- フィルター モジュールの WDK ネットワーク、開始
- フィルター モジュールを開始
- フィルター ドライバー WDK ネットワークは、フィルター モジュールを開始
- NDIS フィルター ドライバー WDK、フィルター モジュールを開始
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4adf0795f8999e9da68b214528382538c8ba5cdc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532066"
---
# <a name="starting-a-filter-module"></a>フィルター モジュールの開始





NDIS フィルター ドライバーの呼び出しを一時停止中のフィルター モジュールを開始する[ *FilterSetModuleOptions* ](https://msdn.microsoft.com/library/windows/hardware/ff549970)関数、存在する場合の後に呼び出して、 [ *FilterRestart*](https://msdn.microsoft.com/library/windows/hardware/ff549962)関数。 フィルター モジュールが入力、*再起動*状態での実行の開始時、 *FilterRestart*関数。

ドライバーのエントリ ポイントが指定されている場合[ *FilterSetModuleOptions*](https://msdn.microsoft.com/library/windows/hardware/ff549970)ドライバーは、フィルター モジュールの部分的な特性を変更できます。 詳細については、次を参照してください。[データ バイパス モード](data-bypass-mode.md)します。

フィルター ドライバーの呼び出し時に[ *FilterRestart* ](https://msdn.microsoft.com/library/windows/hardware/ff549962)関数、NDIS 渡しますへのポインター、 [ **NDIS\_再起動\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff567255)構造体でのフィルター ドライバーを**RestartAttributes**のメンバー、 [ **NDIS\_フィルター\_再起動\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff565572)構造体。 フィルター ドライバーは、基になるドライバーで指定されている再起動属性を変更できます。 再起動の属性を変更する方法の詳細については、次を参照してください。 *FilterRestart*します。

**注**  NDIS 呼び出し[ *FilterSetModuleOptions* ](https://msdn.microsoft.com/library/windows/hardware/ff549970)すべて NDIS 呼び出される前に、スタック内のモジュールのフィルター、 [ *FilterRestart*](https://msdn.microsoft.com/library/windows/hardware/ff549962)スタック内の任意のフィルター モジュールの関数。

 

NDIS は、ドライバー スタックを再起動するプラグ アンド プレイ操作の一部としてフィルター モジュールを開始します。 ドライバー スタックの再起動の概要については、次を参照してください。[ドライバー スタックの再起動](restarting-a-driver-stack.md)します。

内にあるフィルター モジュールの代わり、*再起動*状態では、フィルター ドライバー。

-   通常の送信を再起動し、受信操作に必要なすべての操作を完了します。

    送信し、受信操作についての詳細についてを参照してください。[フィルター モジュールの送信と受信操作](filter-module-send-and-receive-operations.md)します。

-   読み取り、またはフィルター モジュールの構成可能なパラメーターを記述できます。

-   ネットワーク データの表示を受信できます。 コピーし、このようなデータをキューし、ドライバーを後で、関連することを示すことができます、ドライバーまたはデータを破棄できます。

-   開始する必要がありますすべての新しい受信表示します。

-   すべての新しい送信要求を拒否すべきその[ *FilterSendNetBufferLists* ](https://msdn.microsoft.com/library/windows/hardware/ff549966)関数を呼び出すことによってすぐに、 [ **NdisFSendNetBufferListsComplete**](https://msdn.microsoft.com/library/windows/hardware/ff562618)関数。 各完了の状態を設定する必要がある[NET\_バッファー\_一覧](net-buffer-list-structure.md)NDIS に\_状態\_一時停止します。

-   状態インジケーターを提供することができます、 [ **NdisFIndicateStatus** ](https://msdn.microsoft.com/library/windows/hardware/ff561824)関数。

    状態インジケーターの詳細については、次を参照してください。[フィルター モジュールの状態インジケーター](filter-module-status-indications.md)します。

-   OID の要求を処理する必要があります、 [ *FilterOidRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff549954)関数。

    OID 要求の詳細については、次を参照してください。[フィルター モジュールの OID 要求](filter-module-oid-requests.md)します。

-   新しい送信要求を開始する必要があります。

-   戻り値の新しい受信表示 NDIS をすぐに呼び出すことによって、 [ **NdisFReturnNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff562613)関数。 かどうか、必要に応じて、ドライバーをコピーできますなどに返す前にインジケーターを受信します。

-   設定を基になるドライバーに OID 要求を実行できるまたはクエリは、構成情報を更新します。

-   状態インジケーターを処理する必要があります、 [ *FilterStatus* ](https://msdn.microsoft.com/library/windows/hardware/ff549973)関数。

-   NDIS を指定する必要があります\_状態\_成功または失敗の状態。 NDIS と、フィルター モジュールが再起動しない場合は、デタッチし、NDIS 必須フィルターは、全体のドライバー スタックを終了します。

フィルター ドライバーは正常に送信が再起動し、受信操作を再起動操作を完了する必要があります。 フィルター ドライバー操作を完了できる再起動同期または非同期で NDIS を返すことによって\_状態\_成功または NDIS\_状態\_からそれぞれ PENDING [ *FilterRestart*](https://msdn.microsoft.com/library/windows/hardware/ff549962)します。

ドライバーは、NDIS を返す場合\_状態\_保留中、呼び出す必要があります、 [ **NdisFRestartComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff562610)再起動操作が完了した後に機能します。 この場合は、彼はドライバーは、再起動操作の最終的な状態を渡します**NdisFRestartComplete**します。

再起動操作が完了した後に、フィルター モジュールが、*を実行している*状態。 通常のドライバーの再開は、処理を送受信します。

NDIS が他のプラグ アンド プレイ操作を開始していないなどのアタッチ、デタッチ、またはフィルター ドライバーの中に、要求を一時停止、*再起動*状態。 フィルター ドライバーが、NDIS は一時停止要求を開始できる、*を実行している*状態。 フィルター モジュールを一時停止の詳細については、次を参照してください。[フィルター モジュールを一時停止](pausing-a-filter-module.md)します。

 

 





