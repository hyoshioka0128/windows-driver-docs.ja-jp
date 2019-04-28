---
title: WIA DDI インターフェイス
description: WIA DDI インターフェイス
ms.assetid: 738a87e2-9c74-4215-85dc-ec793f10ce05
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d322ccde483705f32bac6354274f8be6fe762af8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367009"
---
# <a name="wia-ddi-interfaces"></a>WIA DDI インターフェイス





WIA デバイス ドライバー インターフェイス (DDI) は、次のインターフェイスおよび WIA ミニドライバーの開発者に関数は指定します。

-   [COM インターフェイスの IWiaMiniDrv](iwiaminidrv-com-interface.md)、ようにミニドライバーに通信方法を提供します。 これらのメソッドは、WIA サービスと、ミニドライバーの間のすべての通信のエントリ ポイントです。 これらのメソッドは、デバイスを制御、WIA サービスを有効にします。

-   [WIA ドライバー サービス ライブラリ](wia-driver-services-library.md)(**wias * * * Xxx*関数)、WIA ミニドライバーのヘルパー関数を提供します。 これらの関数を使用して、、それ以外の場合があるカスタム関数を記述する多くの一般的なタスクを実行することができます。

-   [WIA ユーティリティ ライブラリ](wia-utility-library.md)、提供する追加のヘルパー関数と 3 つのクラス、WIA ミニドライバーを使用できます。

-   [IWiaMiniDrvCallBack COM インターフェイス](iwiaminidrvcallback-com-interface.md)、WIA ミニドライバー コールバックのデータ転送時に使用するためのコールバック メソッドを提供します。

-   [IWiaDrvItem COM インターフェイス](iwiadrvitem-com-interface.md)のデバイスのツリーを維持するために、ミニドライバーのメソッドを提供します**IWiaDrvItem**オブジェクト。

-   [ユーザー インターフェイスの拡張機能](user-interface-extensions.md)、されません既定 WIA のユーザー インターフェイスを介して利用できるデバイスの機能を提供するベンダーを有効にします。

-   [IWiaLog COM インターフェイス](iwialog-com-interface.md)メソッドと診断のログ ファイルにメッセージを記録する WIA ミニドライバーを有効にするマクロを提供します。

 

 




