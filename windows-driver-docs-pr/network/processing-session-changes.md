---
title: セッション変更の処理
description: セッション変更の処理
ms.assetid: 6684b27e-d2ba-4305-bbd2-27543c9ec0cf
keywords:
- ユーザー操作 WDK ネイティブ 802.11 IHV 拡張 DLL
- セッションの変更 WDK ネイティブ 802.11 IHV 拡張 DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7ee43d8f4c908c250d1459513da592b14a0a4035
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843483"
---
# <a name="processing-session-changes"></a>セッション変更の処理




 

ユーザーがログインまたはログアウトしたときなど、ユーザーのセッションが状態を変更した場合、オペレーティングシステムは、 [*Dot11ExtIhvProcessSessionChange*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_process_session_change)関数を呼び出して、セッションの変更について IHV 拡張 DLL に通知します。 オペレーティングシステムは、セッションの変更の理由を*Ueventtype*パラメーターに渡します。

*Ueventtype*パラメーターが WTS\_SESSION\_LOGOFF に設定されている場合、ユーザーは現在のセッションからログオフしています。 この状況では、保留中のすべてのユーザーインターフェイス (UI) 要求は、IHV 拡張 DLL によって内部的にキャンセルされる必要があります。また、DLL は、保留中の UI 要求ごとに割り当てられたリソースを解放する必要があります。

 

 





