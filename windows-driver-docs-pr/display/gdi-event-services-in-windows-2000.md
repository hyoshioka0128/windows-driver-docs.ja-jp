---
title: Windows 2000 での GDI イベント サービス
description: Windows 2000 での GDI イベント サービス
ms.assetid: bf7f2127-cd3e-430c-99fd-62c824394a57
keywords:
- DirectX 8.0 リリース ノートには、Windows 2000 の WDK 表示 GDI イベント サービス
- GDI WDK Windows 2000 の表示、イベント
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 570ba9e5fa8c5d4c457915ec109d14226e58b3d7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63326188"
---
# <a name="gdi-event-services-in-windows-2000"></a>Windows 2000 での GDI イベント サービス


## <span id="ddk_gdi_event_services_in_windows_2000_gg"></span><span id="DDK_GDI_EVENT_SERVICES_IN_WINDOWS_2000_GG"></span>


[GDI イベント サービス](gdi-event-services.md)ディスプレイ ドライバーは、同期に使用できる GDI イベントに関連する関数のグループについて説明します。 Microsoft Windows XP で使用でき、後でのみとしては、これらのイベントに関連する関数が記載されている、それらのほとんどは Microsoft Windows 2000 では使用も。 これらのイベントに関連する関数のほとんどは Windows 2000 で使用できますはお勧めしませんが、ドライバーはこのような可能性があるため Windows 2000 信頼性の低い、ドライバーが Windows 2000 の実装で使用します。

Windows 2000 で利用できるイベントに関連する関数の Windows 2000 で同様に動作以外の Windows xp のように、 [ **EngWaitForSingleObject** ](https://msdn.microsoft.com/library/windows/hardware/ff565461)関数。 **EngWaitForSingleObject** Windows 2000 での実装には、Windows XP の実装を返すブール値ではなく、DWORD 値が返されます。 この DWORD 値には、次の値のいずれかを指定できます。

<span id="Zero"></span><span id="zero"></span><span id="ZERO"></span>0  
次の操作の 1 つ発生したことを示します。

-   待機が成功しました。 つまり、指定されたイベント オブジェクトは、シグナル状態に設定されました。 呼び出したスレッド**EngWaitForSingleObject**処理を再開することができます。

-   呼び出し元のスレッドへの無効なイベント オブジェクト ポインターを渡された、 *pEvent*パラメーターの**EngWaitForSingleObject**します。

<span id="Any_nonzero_value"></span><span id="any_nonzero_value"></span><span id="ANY_NONZERO_VALUE"></span>0 以外の値  
この値は、特定のエラー条件を示す NTSTATUS 状態値です。 たとえば、状態\_タイムアウトは、タイムアウトが発生したことを示します。

**注**   、 [ **EngClearEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff564190)と[ **EngReadStateEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff565001)関数では使用できませんWindows 2000 です。

 

 

 





