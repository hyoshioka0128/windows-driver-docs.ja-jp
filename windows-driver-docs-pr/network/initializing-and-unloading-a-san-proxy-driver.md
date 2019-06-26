---
title: SAN プロキシ ドライバーの初期化とアンロード
description: SAN プロキシ ドライバーの初期化とアンロード
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
ms.openlocfilehash: 1d1de55ee9a03c279135575e049ac39f72be2029
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381279"
---
# <a name="initializing-and-unloading-a-san-proxy-driver"></a>SAN プロキシ ドライバーの初期化とアンロード





作成とデバイスの初期化に加えてオブジェクト ドライバー オブジェクトのプロキシ ドライバーの**DriverEntry**ルーチンは、ドライバーの管理下にある Nic の追加または削除はときに通知を登録できます。 詳細については、次を参照してください。 [SAN NIC の通知を登録する](registering-for-san-nic-notifications.md)します。

プロキシ ドライバーの SAN サービス プロバイダーは、プロキシ ドライバー、I/O 制御要求を送信する場合**DriverEntry**指定する必要があります、*エントリ ポイント*デバイス制御できるようにします。 プロバイダーは、ドライバーの Nic に割り当てられた IP アドレスの一覧を取得する要求可能性がありますなどができます。 この要求のエントリ ポイントは、 [ **IRP\_MJ\_デバイス\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)ドライバーの Nic に割り当てられた IP アドレスのリストを返すルーチンをディスパッチします。 詳細については、次を参照してください。 [SAN サービス プロバイダーの実装の Ioctl](implementing-ioctls-for-a-san-service-provider.md)します。

**DriverEntry**ルーチンは、プロキシ ドライバーをアンロードするルーチンのエントリ ポイントを指定する必要があります。 このアンロード ルーチンで作成されたデバイスを削除します**DriverEntry**します。

 

 





