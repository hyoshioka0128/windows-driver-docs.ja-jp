---
title: フレームワーク要求オブジェクトの再利用
description: フレームワーク要求オブジェクトの再利用
ms.assetid: 9e3090a9-62d0-48b3-9f3b-7171dc6d2766
keywords:
- 要求の処理の WDK KMDF、要求オブジェクトを再利用
- 要求オブジェクト WDK KMDF、再利用
- WDK KMDF をオブジェクトの要求を再利用
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 55daabf712c2bdb2249cc8c2195cf39088f176ac
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376248"
---
# <a name="reusing-framework-request-objects"></a>フレームワーク要求オブジェクトの再利用





パフォーマンスを向上させるのには、framework ベースのドライバーを作成し、再利用できる大量の I/O をターゲットとほぼ同じ非同期要求を送信は、要求ごとに新しい要求オブジェクトを作成する代わりにオブジェクトを要求します。 ドライバーは、要求が完了した後、要求オブジェクトを再利用できます。

ドライバーが呼び出すことによって、要求オブジェクトを作成してかどうか[ **WdfRequestCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcreate)または[ **WdfRequestCreateFromIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcreatefromirp)要求を再利用できます呼び出して[ **WdfRequestReuse**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestreuse)します。 ドライバーには、その I/O キューのフレームワークから受信した要求オブジェクトが再利用もできますが、受信した要求オブジェクトに含まれる IRP を変更することはできません。

説明されている失敗した場合の戻り値の発生状況を回避するように注意する場合は[ **WdfRequestReuse**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestreuse)、呼び出すことができます、ドライバー **WdfRequestReuse**内から、[ *CompletionRoutine* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nc-wdfrequest-evt_wdf_request_completion_routine)コールバック関数。 (、 *CompletionRoutine*コールバック関数が VOID の戻り値し、そのため、エラーを報告することはできません)。

お使いのドライバーの場合、 [ *CompletionRoutine* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nc-wdfrequest-evt_wdf_request_completion_routine)ドライバーに呼び出す必要がありますが再利用する要求オブジェクトのコールバック関数、 [ **WdfRequestSetCompletionRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestsetcompletionroutine)呼び出した後[ **WdfRequestReuse**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestreuse)します。

 

 





