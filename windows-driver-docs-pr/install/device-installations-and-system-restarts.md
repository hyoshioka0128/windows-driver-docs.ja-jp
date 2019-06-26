---
title: デバイスのインストールとシステムの再起動
description: デバイスのインストールとシステムの再起動
ms.assetid: c09d2150-60ae-4912-86f5-6489c818853e
keywords:
- デバイスのインストール WDK、再起動
- デバイス WDK をインストールするには、再起動します。
- デバイス セットアップ WDK デバイス インストールの再起動
- WDK のデバイスのインストールを再起動します。
- デバイスのインストール中に再起動を開始します。
- デバイスのインストール中に再起動します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 45d5458a980367da11a30c05e4a7fec116894080
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387137"
---
# <a name="device-installations-and-system-restarts"></a>デバイスのインストールとシステムの再起動





デバイスのインストールする必要があります強制しない限り、システムの再起動を絶対に必要です。 次の状況を唯一のものであるシステムの再起動が必要にする必要があります。

<a href="" id="installing-or-removing-a-non-plug-and-play-device--"></a>インストールまたはプラグ アンド プレイ デバイスを削除します。   
これらの以前のデバイスのユーザー通常必要がありますシステムをシャット ダウン、物理的に追加またはデバイスを削除する前にします。 電源戻った後、システムが起動します。

**注**  デバイスのセットアップ ファイルは、前に、またはハードウェアを接続した後に、ユーザーが、ドライバーをインストールするかどうかに関係なく、システムの再起動を開始しないでください。

 

<a href="" id="updating-a-driver-for-a-system-boot-device--"></a>システムのブート デバイス用のドライバーを更新しています。   
システムのページング、休止状態、またはクラッシュ ダンプ ファイルに、デバイスが保持できる可能性がある場合、ドライバーがサービスする必要があります[ **IRP_MN_DEVICE_USAGE_NOTIFICATION** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-device-usage-notification)要求。 システムは、これらのファイル、ディスク上のいずれかを配置する前に、この要求を送信します。 その後する必要があります失敗した場合は、ドライバーは、要求を成功[ **IRP_MN_QUERY_REMOVE_DEVICE** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-remove-device)要求。 デバイスのドライバーには、IRP_MN_QUERY_REMOVE_DEVICE 要求が失敗した場合、ユーザーに、システムの再起動が求められます。

**注**  デバイスのセットアップ ファイルがシステムの再起動を開始する必要があります。

 

<a href="" id="installing-a-non-wdm-filter-driver-"></a>非 WDM フィルター ドライバーをインストールします。  
フィルター ドライバーを非 WDM ドライバー スタックに追加する場合、システムを再起動する必要があります。 この場合、ドライバーのインストーラーや共同インストーラー システムの再起動を要求する必要があります (を参照してください[開始中にデバイス インストールのシステム再起動](initiating-system-restarts-during-device-installations.md))。

**注**   WDM ドライバー スタックへのフィルター ドライバーの追加は、システムの再起動を基になるデバイスがシステムのブート デバイスでない限り、します。

 

セクションには、次のトピックが含まれています。

[デバイスのインストール中にシステムの再起動を避ける](avoiding-system-restarts-during-device-installations.md)

[デバイスのインストール中の再起動のシステムを開始します。](initiating-system-restarts-during-device-installations.md)

 

 





