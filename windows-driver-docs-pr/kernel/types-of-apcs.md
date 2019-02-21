---
title: Apc の種類
description: Apc の種類
ms.assetid: 74ed953c-1b2a-40b9-9df3-16869b198b38
keywords:
- 非同期プロシージャ呼び出しの WDK カーネル
- Apc WDK カーネル
- ユーザーの Apc WDK カーネル
- 通常カーネル Apc WDK カーネル
- 特別なカーネル Apc WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 514f03879913030db26c5bfc094b394de2d9768e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535758"
---
# <a name="types-of-apcs"></a>Apc の種類


非同期プロシージャ コール (APC) は、非同期に実行される関数です。 Apc が遅延プロシージャ呼び出し (Dpc) と同じですが、Dpc とは異なり、Apc が特定のスレッドのコンテキスト内で実行します。 (ファイル システムとファイル システム フィルター ドライバー) 以外のドライバーを使用しないで Apc を直接、オペレーティング システムの他の部分には、Apc のしくみを認識する必要があります。

Windows オペレーティング システムでは、3 種類の Apc を使用します。

-   *ユーザーの Apc*ユーザー モードと現在のスレッドがステートでが場合にのみで厳密に実行します。 オペレーティング システムでは、ユーザー Apc を使用して、重複 I/O などのメカニズムを実装して、 **QueueUserApc** Win32 ルーチン。

-   *通常カーネル Apc* IRQL でカーネル モードで実行 = パッシブ\_レベル。 通常カーネル APC では、ユーザーの Apc を含む、すべてのユーザー モード コードを横取りします。 通常カーネル Apc は通常、ファイル システムおよびファイル システム フィルター ドライバーによって使用されます。

-   *特別なカーネル Apc* IRQL でカーネル モードで実行 = APC\_レベル。 ユーザー モード コードとカーネル モード コード IRQL でを実行する特別なカーネル APC に横取りされ = パッシブ\_ユーザー Apc と通常のカーネル Apc の両方を含むレベル。 オペレーティング システムでは、I/O 要求の完了などの操作を処理するために特別なカーネル Apc を使用します。

 

 




