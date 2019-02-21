---
title: アクティビティの識別子を使用してください。
description: アクティビティの識別子を使用してください。
ms.assetid: 2B70953F-5192-4654-9506-6A84373D20B4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f180ccd37ac7c5d12adc3cb820f9da59fdc7a77f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537557"
---
# <a name="using-activity-identifiers"></a>アクティビティの識別子を使用してください。


フレームワーク バージョン 1.11 以降では、UMDF ドライバーは、設定し、アクティビティ識別子 (Id) を取得します。 アクティビティ Id では、複数の I/O 要求を関連付けることが許可されること Event Tracing for Windows (ETW) を使用してそれらを追跡できるようにトレースします。 このトピックでは、アクティビティ Id、ドライバーが使用して可能なシナリオについて説明します。

## <a name="associating-new-requests-with-an-existing-request"></a>新しい要求を既存の要求に関連付ける


ドライバーの I/O ディスパッチ コールバック関数では、複数のフレームワークに、受信要求の結果として I/O 要求を作成可能性があります。 ドライバーが元の要求アクティビティ ID を取得し、新しい要求で呼び出すことによって設定[ **WdfRequestRetrieveActivityId** ](https://msdn.microsoft.com/library/windows/hardware/dn265621)と[ **WdfRequestSetActivityId**](https://msdn.microsoft.com/library/windows/hardware/dn265622)します。

コード例では、次を参照してください。 [ **WdfRequestRetrieveActivityId**](https://msdn.microsoft.com/library/windows/hardware/dn265621)します。

## <a name="associating-new-requests-with-an-existing-thread"></a>新しい要求を既存のスレッドに関連付ける


ドライバーは、I/O のディスパッチ スレッド以外のスレッドまたは作業項目に新しい I/O 要求を作成可能性があります。 対応するすべての要求から、または I/O のディスパッチ スレッドに関連付けられているアクティビティ ID を使用して、このような要求のアクティビティ ID を設定できます。 ドライバーは、呼び出すことによって、現在のスレッドに関連付けられているアクティビティ ID を取得できます[ **EventActivityIdControl** ](https://msdn.microsoft.com/library/windows/desktop/aa363720)呼び出して[ **WdfRequestSetActivityId**](https://msdn.microsoft.com/library/windows/hardware/dn265622)新しい I/O 要求の識別子を設定します。

ドライバーは、I/O 要求を送信する Win32 API を呼び出す場合、元の要求からアクティビティ ID を取得し、スレッドに伝播することができます。 I/O マネージャーは、次の要求に対する応答で生成される、I/O 要求パケット (Irp) にスレッドに関連付けられているアクティビティ ID を適用します。

 

 





