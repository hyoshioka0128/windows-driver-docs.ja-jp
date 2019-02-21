---
title: セッションの変更の処理
description: セッションの変更の処理
ms.assetid: 6684b27e-d2ba-4305-bbd2-27543c9ec0cf
keywords:
- ユーザーの介入 WDK ネイティブ 802.11 IHV 拡張 DLL
- セッションは、WDK の 802.11 IHV ・拡張機能のネイティブ DLL を変更します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3e36bb394335eb14927582fd982bb3daac556cc3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550990"
---
# <a name="processing-session-changes"></a>セッションの変更の処理




 

呼び出すことでの変更をユーザーのログオン時に、オペレーティング システムに通知セッションに関する IHV 拡張機能の DLL など、ユーザーのセッションに状態が変更された場合、 [ *Dot11ExtIhvProcessSessionChange* ](https://msdn.microsoft.com/library/windows/hardware/ff547501)関数。 オペレーティング システムにセッションの変更の理由を渡す、 *uEventType*パラメーター。

場合、 *uEventType*パラメーター WTS を設定する\_セッション\_ログオフ、現在のセッションからユーザーがログオンします。 このような状況で保留中のユーザー インターフェイス (UI) のすべての要求は、IHV 拡張機能の DLL によって内部的にキャンセルする必要があり、DLL が保留中の UI 要求ごとに割り当てられたリソースを解放する必要があります。

 

 





