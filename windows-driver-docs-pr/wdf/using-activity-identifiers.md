---
title: アクティビティ識別子の使用
description: アクティビティ識別子の使用
ms.assetid: 2B70953F-5192-4654-9506-6A84373D20B4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 09ca53f29d2e8e761ac7851f8695f4d4249806fb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372281"
---
# <a name="using-activity-identifiers"></a>アクティビティ識別子の使用


フレームワーク バージョン 1.11 以降では、UMDF ドライバーは、設定し、アクティビティ識別子 (Id) を取得します。 アクティビティ Id では、複数の I/O 要求を関連付けることが許可されること Event Tracing for Windows (ETW) を使用してそれらを追跡できるようにトレースします。 このトピックでは、アクティビティ Id、ドライバーが使用して可能なシナリオについて説明します。

## <a name="associating-new-requests-with-an-existing-request"></a>新しい要求を既存の要求に関連付ける


ドライバーの I/O ディスパッチ コールバック関数では、複数のフレームワークに、受信要求の結果として I/O 要求を作成可能性があります。 ドライバーが元の要求アクティビティ ID を取得し、新しい要求で呼び出すことによって設定[ **WdfRequestRetrieveActivityId** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveactivityid)と[ **WdfRequestSetActivityId**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestsetactivityid)します。

コード例では、次を参照してください。 [ **WdfRequestRetrieveActivityId**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveactivityid)します。

## <a name="associating-new-requests-with-an-existing-thread"></a>新しい要求を既存のスレッドに関連付ける


ドライバーは、I/O のディスパッチ スレッド以外のスレッドまたは作業項目に新しい I/O 要求を作成可能性があります。 対応するすべての要求から、または I/O のディスパッチ スレッドに関連付けられているアクティビティ ID を使用して、このような要求のアクティビティ ID を設定できます。 ドライバーは、呼び出すことによって、現在のスレッドに関連付けられているアクティビティ ID を取得できます[ **EventActivityIdControl** ](https://docs.microsoft.com/windows/desktop/api/evntprov/nf-evntprov-eventactivityidcontrol)呼び出して[ **WdfRequestSetActivityId**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestsetactivityid)新しい I/O 要求の識別子を設定します。

ドライバーは、I/O 要求を送信する Win32 API を呼び出す場合、元の要求からアクティビティ ID を取得し、スレッドに伝播することができます。 I/O マネージャーは、次の要求に対する応答で生成される、I/O 要求パケット (Irp) にスレッドに関連付けられているアクティビティ ID を適用します。

 

 





