---
title: フレームワーク要求オブジェクトの再利用
description: フレームワーク要求オブジェクトの再利用
ms.assetid: 9e3090a9-62d0-48b3-9f3b-7171dc6d2766
keywords:
- WDK KMDF の要求の処理、要求オブジェクトの再利用
- 要求オブジェクト WDK KMDF、再利用
- 要求オブジェクトの再利用 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 498cf85da837e32a0cc752a1b70f5522bf6e2fac
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842208"
---
# <a name="reusing-framework-request-objects"></a>フレームワーク要求オブジェクトの再利用





パフォーマンスを向上させるために、ほぼ同一の非同期要求を作成して i/o ターゲットに送信するフレームワークベースのドライバーは、要求ごとに新しい要求オブジェクトを作成する代わりに、要求オブジェクトを再利用できます。 要求が完了すると、ドライバーは要求オブジェクトを再利用できます。

ドライバーが[**Wdfrequestcreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcreate)または[**Wdfrequestcreatefromirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcreatefromirp)を呼び出して要求オブジェクトを作成した場合、 [**WdfRequestReuse**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestreuse)を呼び出すことによって要求を再利用できます。 また、ドライバーは、その i/o キューのフレームワークから受信した要求オブジェクトを再利用することもできますが、受信した要求オブジェクトに含まれる IRP を変更することはできません。

[**WdfRequestReuse**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestreuse)で説明されている失敗した戻り値の原因となる状況を避けるために、ドライバーは、実行可能[*ルーチン*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nc-wdfrequest-evt_wdf_request_completion_routine)のコールバック関数内から**WdfRequestReuse**を呼び出すことができます。 (*補完ルーチン*のコールバック関数には VOID の戻り値があるため、エラーを報告することはできません)。

ドライバーが、再利用する要求オブジェクトに対して完了[*ルーチン*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nc-wdfrequest-evt_wdf_request_completion_routine)のコールバック関数を提供している場合、ドライバーは[**WdfRequestReuse**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestreuse)を呼び出した後に[**wdfrequestset ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsetcompletionroutine)を呼び出す必要があります。

 

 





