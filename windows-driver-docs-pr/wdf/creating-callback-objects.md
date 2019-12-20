---
title: コールバック オブジェクトの作成
description: コールバック オブジェクトの作成
ms.assetid: bbae1458-911f-4a48-8bf2-0997e8f98826
keywords:
- コールバックオブジェクト WDK UMDF
- コールバックオブジェクト WDK UMDF、作成
- ユーザーモードドライバーフレームワーク WDK、オブジェクト
- ユーザーモードドライバー WDK UMDF、オブジェクト
- UMDF オブジェクト WDK、コールバックオブジェクト
- フレームワークオブジェクト WDK UMDF、コールバックオブジェクト
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 13634974b988c7c981f503e040825c9d3e5097c0
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210180"
---
# <a name="creating-callback-objects"></a>コールバック オブジェクトの作成


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

UMDF ドライバーでは、コンテキストデータとインターフェイスメソッドで構成される*コールバックオブジェクト*を作成できます。 このフレームワークは、ドライバーのコールバックインターフェイスメソッドを介して、ドライバーのコールバックオブジェクトにアクセスします。

次の図は、ドライバーによって実装されたコールバックオブジェクトが[フレームワークオブジェクト](framework-objects.md)にどのように対応するかを示しています。

![フレームワークオブジェクトとベンダー提供のコールバックオブジェクト](images/correspond.gif)

UMDF ドライバーでは、次のようないくつかの種類のコールバックオブジェクトを作成できます。

-   ドライバーコールバックオブジェクト

    このフレームワークは、ドライバーのコールバックオブジェクトを使用してドライバーを初期化し、新しいデバイスの到着をドライバーに通知します。

-   デバイスコールバックオブジェクト

    ドライバーはデバイスコールバックオブジェクトを使用してデバイスコンテキストを格納し、ファイルオブジェクトとプラグアンドプレイ (PnP) イベントおよび電源管理 (PM) イベントのクリーンアップと終了を処理します。

-   キューコールバックオブジェクト

    ドライバーは、キューコールバックオブジェクトを使用して i/o を処理します。

次の図は、UMDF ドライバーがデバイスコールバックオブジェクトを作成する方法を示しています。

![umdf デバイスコールバックオブジェクトを作成するための呼び出しシーケンス](images/callback.gif)

次のトピックには、コールバックオブジェクトの作成方法を示すコード例が含まれています。

-   [コールバックオブジェクトの作成の例](creating-callback-objects-example.md)

-   [コールバックオブジェクトの定義の例](defining-callback-objects-example.md)

-   [コールバックインターフェイスの関連付けの例](associating-callback-interfaces-example.md)

 

 





