---
title: PnP カスタム通知の使用
description: PnP カスタム通知の使用
ms.assetid: de5562f8-07a8-4f4e-ac49-58c789bd9fde
keywords:
- WDK PnP、カスタムの通知
- カスタム通知 PnP WDK
- 通知 WDK PnP、ターゲット デバイスの変更
- ターゲット デバイスの変更通知 PnP WDK
- EventCategoryTargetDeviceChange 通知
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 44ae6795262b4600251fa2e78dae896385a85404
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354218"
---
# <a name="using-pnp-custom-notification"></a>PnP カスタム通知の使用





ドライバーは、デバイスでのカスタム イベントの通知をターゲット デバイスの変更通知のメカニズムを使用できます。

カスタム イベントを定義するプログラマは、次の操作を行う必要があります。

1.  カスタム イベントの新しい GUID を定義します。

    GUID を生成**Uuidgen**または**Guidgen** (Microsoft Windows SDK に含まれている)。 適切なヘッダー ファイルとドキュメントには、GUID を発行します。

2.  カスタム イベントをトリガーするコードを記述します。

    カーネル モード ドライバー呼び出し[ **IoReportTargetDeviceChange** ](https://msdn.microsoft.com/library/windows/hardware/ff549625)カスタム GUID と、デバイスの PDO へのポインター。 カスタム イベントは、カーネル モードからのみトリガーできます。

ドライバーのライターでは、次のようにプロシージャを使用したカスタム通知を使用します。

1.  ドライバー (またはアプリケーション) は、カスタム イベントの通知を登録します。

    カーネル モード ドライバー呼び出し[ **IoRegisterPlugPlayNotification** ](https://msdn.microsoft.com/library/windows/hardware/ff549526)とレジスタの**EventCategoryTargetDeviceChange**デバイスにします。

    ユーザー モードでは、アプリケーションは、登録を使用して**RegisterDeviceNotification**します。 詳細については、Windows SDK を参照してください。

2.  カーネル モード コンポーネントは、カスタム イベントをトリガーします。

3.  PnP マネージャーでは、デバイスに登録されている通知ルーチンを呼び出します。

    PnP マネージャーでは、登録済みのユーザー モードにコールバック ルーチンを呼び出して、カーネル モードにコールバック ルーチンを呼び出します。

4.  ユーザー モードの通知が完了したら、カーネル モード ドライバーの通知コールバック routine(s) はカスタム イベントに応答します。

    参照してください[PnP 通知コールバック ルーチンを記述するためのガイドライン](guidelines-for-writing-pnp-notification-callback-routines.md)通知コールバック ルーチンの一般的なガイドラインです。 これらのガイドラインに加えカスタム通知のコールバック ルーチンをする必要がありますからコールバック ルーチン スレッド内のデバイスを識別するハンドルを開けません。

 

 




