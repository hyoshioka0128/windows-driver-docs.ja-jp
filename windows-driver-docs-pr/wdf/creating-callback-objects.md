---
title: コールバック オブジェクトの作成
description: コールバック オブジェクトの作成
ms.assetid: bbae1458-911f-4a48-8bf2-0997e8f98826
keywords:
- コールバック オブジェクト WDK UMDF
- コールバック オブジェクトを作成する、WDK UMDF
- ユーザー モード ドライバー フレームワーク WDK のオブジェクト
- ユーザー モード ドライバー WDK UMDF、オブジェクト
- UMDF オブジェクト WDK、コールバック オブジェクト
- フレームワークは、WDK UMDF、コールバック オブジェクトをオブジェクトします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 18cf7083d053a77f280e5d3377342878fc962527
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358589"
---
# <a name="creating-callback-objects"></a>コールバック オブジェクトの作成


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

UMDF ドライバーを作成できます*コールバック オブジェクト*コンテキストのデータとインターフェイスのメソッドで構成されます。 フレームワークでは、ドライバーのコールバック インターフェイスのメソッドによって、ドライバーのコールバック オブジェクトにアクセスします。

次の図に、ドライバーの実装方法のコールバック オブジェクトに対応して[framework オブジェクト](framework-objects.md)します。

![framework のオブジェクトとコールバックのベンダーから提供されたオブジェクト](images/correspond.gif)

UMDF ドライバーでは、コールバック オブジェクトに、次のいくつかの種類を作成できます。

-   ドライバーのコールバック オブジェクト

    フレームワークでは、ドライバーのコールバック オブジェクトを使用して、ドライバーを初期化し、新しいデバイスの到着をドライバーに通知します。

-   デバイスのコールバック オブジェクト

    ドライバーは、デバイス コンテキストを格納して、クリーンアップとファイル オブジェクトとプラグ アンド プレイ (PnP) と電源管理 (PM) のイベントの終了を処理するために、デバイス コールバック オブジェクトを使用します。

-   コールバック オブジェクトのキュー

    ドライバーは、プロセスの i/o キューのコールバック オブジェクトを使用します。

次の図は、UMDF ドライバーが、デバイス コールバック オブジェクトを作成する方法を示します。

![umdf デバイス コールバック オブジェクトを作成するための呼び出しシーケンス](images/callback.gif)

次のトピックには、コールバック オブジェクトを作成する方法を示すコード例が含まれます。

-   [コールバック オブジェクトの例を作成します。](creating-callback-objects-example.md)

-   [コールバック オブジェクトの例を定義します。](defining-callback-objects-example.md)

-   [関連付けられたコールバック インターフェイスの例](associating-callback-interfaces-example.md)

 

 





