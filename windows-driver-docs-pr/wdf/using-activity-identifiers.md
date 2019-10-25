---
title: アクティビティ識別子の使用
description: アクティビティ識別子の使用
ms.assetid: 2B70953F-5192-4654-9506-6A84373D20B4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b248653eb6f7375bc55d6f8d931c6f0db2eb4e4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843102"
---
# <a name="using-activity-identifiers"></a>アクティビティ識別子の使用


Framework バージョン1.11 以降では、UMDF ドライバーはアクティビティ識別子 (IDs) を設定および取得できます。 アクティビティ Id を使用すると、複数の i/o 要求を関連付けることができます。これにより、Windows イベントトレーシング (ETW) トレースを使用して追跡できるようになります。 このトピックでは、ドライバーがアクティビティ Id を使用する可能性があるいくつかのシナリオについて説明します。

## <a name="associating-new-requests-with-an-existing-request"></a>新しい要求を既存の要求に関連付ける


ドライバーの i/o ディスパッチコールバック関数では、受信要求の結果として複数のフレームワーク i/o 要求を作成する場合があります。 ドライバーは元の要求からアクティビティ ID を取得し、 [**WdfRequestRetrieveActivityId**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveactivityid)および[**Wdfrequestsetactivityid**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsetactivityid)を呼び出すことによって、新しい要求でそれを設定します。

コード例については、「 [**WdfRequestRetrieveActivityId**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveactivityid)」を参照してください。

## <a name="associating-new-requests-with-an-existing-thread"></a>新しい要求を既存のスレッドに関連付ける


ドライバーは、i/o ディスパッチスレッドまたは作業項目以外のスレッドで、新しい i/o 要求を作成する場合があります。 このような要求のアクティビティ ID は、対応する要求から設定することも、i/o ディスパッチスレッドに関連付けられているアクティビティ ID を使用して設定することもできます。 現在のスレッドに関連付けられているアクティビティ ID を取得するには、 [**Eventactivityidcontrol**](https://docs.microsoft.com/windows/desktop/api/evntprov/nf-evntprov-eventactivityidcontrol)を呼び出してから、 [**Wdfrequestsetactivityid**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsetactivityid)を呼び出して、新しい i/o 要求ごとに識別子を設定します。

ドライバーは、i/o 要求を送信するために Win32 API を呼び出した場合、元の要求からアクティビティ ID を取得し、それをスレッドに伝達することができます。 次に、i/o マネージャーは、スレッドに関連付けられているアクティビティ ID を、要求に対する応答として生成する i/o 要求パケット (Irp) に適用します。

 

 





