---
title: 初期化と SAN プロキシ ドライバーをアンロード
description: 初期化と SAN プロキシ ドライバーをアンロード
ms.assetid: 1c602f7d-a1c2-429a-a297-4290a7cbfd9f
keywords:
- プロキシ ドライバー WDK San、初期化しています
- SAN プロキシ ドライバー WDK、初期化しています
- プロキシ ドライバー WDK San、アンロード
- SAN プロキシ ドライバー WDK、アンロード
- アンロード ドライバー
- SAN プロキシ ドライバーを初期化しています
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d5774e5e9aef58fdc2589e9d91621d967f373d5a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551283"
---
# <a name="initializing-and-unloading-a-san-proxy-driver"></a>初期化と SAN プロキシ ドライバーをアンロード





作成とデバイスの初期化に加えてオブジェクト ドライバー オブジェクトのプロキシ ドライバーの**DriverEntry**ルーチンは、ドライバーの管理下にある Nic の追加または削除はときに通知を登録できます。 詳細については、次を参照してください。 [SAN NIC の通知を登録する](registering-for-san-nic-notifications.md)します。

プロキシ ドライバーの SAN サービス プロバイダーは、プロキシ ドライバー、I/O 制御要求を送信する場合**DriverEntry**指定する必要があります、*エントリ ポイント*デバイス制御できるようにします。 プロバイダーは、ドライバーの Nic に割り当てられた IP アドレスの一覧を取得する要求可能性がありますなどができます。 この要求のエントリ ポイントは、 [ **IRP\_MJ\_デバイス\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff550744)ドライバーの Nic に割り当てられた IP アドレスのリストを返すルーチンをディスパッチします。 詳細については、次を参照してください。 [SAN サービス プロバイダーの実装の Ioctl](implementing-ioctls-for-a-san-service-provider.md)します。

**DriverEntry**ルーチンは、プロキシ ドライバーをアンロードするルーチンのエントリ ポイントを指定する必要があります。 このアンロード ルーチンで作成されたデバイスを削除します**DriverEntry**します。

 

 





