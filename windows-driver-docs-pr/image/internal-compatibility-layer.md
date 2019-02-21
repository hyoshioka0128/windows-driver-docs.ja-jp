---
title: 内部互換性レイヤー
description: 内部互換性レイヤー
ms.assetid: 6cfb3842-751e-4f4c-9fac-daba70245b81
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6d6d97c48d5501223d35caddc281b5cc740fafd2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528646"
---
# <a name="internal-compatibility-layer"></a>内部互換性レイヤー


Windows Vista で実行するドライバーを開発する際に互換性の 2 つの側面を考慮する必要があります。

-   Windows XP またはそれ以前のオペレーティング システムは、アプリケーションが Windows Vista のドライバーと通信する場合

-   Windows Vista アプリケーションを Windows XP ドライバーと通信するときに (つまり、*レガシ ドライバー*)

Windows Vista のアプリケーションが、Windows Vista ドライバーを通信する場合や、このような状況では、互換性が必要ないために、Windows XP のドライバーと Windows XP アプリケーションが通信するときなど、その他の状況を考慮する必要はありません。コンポーネント。

WIA では、すべての必要な変換を実行する内部互換性レイヤーを提供します。 そのため、Windows Vista で実行される Windows XP アプリケーションが Windows Vista のドライバーと通信できるようにして、Windows Vista のアプリケーションが Windows Vista で実行される Windows XP ドライバーと通信できます。

これには、互換性レイヤーのいくつかの制限があります。

-   Windows Vista の WIA アプリケーションを従来のドライバーのみが変換されます。

-   基本項目としてベッドとフィーダーを実装する Windows Vista スキャナー ドライバーのみ (WIA\_カテゴリ\_ベッドと WIA\_カテゴリ\_フィーダー) レガシの WIA アプリケーション用に変換されます。

 

 




