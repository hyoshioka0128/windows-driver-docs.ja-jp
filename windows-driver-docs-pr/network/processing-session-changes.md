---
title: セッション変更の処理
description: セッション変更の処理
ms.assetid: 6684b27e-d2ba-4305-bbd2-27543c9ec0cf
keywords:
- ユーザーの介入 WDK ネイティブ 802.11 IHV 拡張 DLL
- セッションは、WDK の 802.11 IHV ・拡張機能のネイティブ DLL を変更します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 03b1a2476e9b3146db66fff01cf4bafdc34e29e8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385471"
---
# <a name="processing-session-changes"></a>セッション変更の処理




 

呼び出すことでの変更をユーザーのログオン時に、オペレーティング システムに通知セッションに関する IHV 拡張機能の DLL など、ユーザーのセッションに状態が変更された場合、 [ *Dot11ExtIhvProcessSessionChange* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_process_session_change)関数。 オペレーティング システムにセッションの変更の理由を渡す、 *uEventType*パラメーター。

場合、 *uEventType*パラメーター WTS を設定する\_セッション\_ログオフ、現在のセッションからユーザーがログオンします。 このような状況で保留中のユーザー インターフェイス (UI) のすべての要求は、IHV 拡張機能の DLL によって内部的にキャンセルする必要があり、DLL が保留中の UI 要求ごとに割り当てられたリソースを解放する必要があります。

 

 





