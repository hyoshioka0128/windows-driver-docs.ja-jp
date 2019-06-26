---
title: CD-ROM 排他アクセス モード
description: CD-ROM 排他アクセス モード
ms.assetid: 4432f6d6-e98c-4354-a7ba-b043a624f064
keywords:
- CD-ROM ドライバー WDK ストレージ
- CD-ROM のストレージ ドライバー WDK
- WDK の CD-ROM の排他アクセス モード
- IOCTL_CDROM_EXCLUSIVE_ACCESS
- CDROM_EXCLUSIVE_LOCK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2d0bb6dea4075890839ed5fb7da243e52f8eb3ab
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368339"
---
# <a name="cd-rom-exclusive-access-mode"></a>CD-ROM 排他アクセス モード


CD-ROM*排他アクセス*メカニズム (とも呼ばれます*排他アクセス モード*) CD-ROM デバイスへの排他アクセスを取得するには、アプリケーションおよびシステム コンポーネントを使用します。 CD-ROM デバイスへの排他アクセスを必要とするアプリケーションには、次の例が含まれます。

<span id="Optical_media-authoring_applications"></span><span id="optical_media-authoring_applications"></span><span id="OPTICAL_MEDIA-AUTHORING_APPLICATIONS"></span>光学式メディア作成アプリケーション  
いくつかの光学式作成ソフトウェアには、他のアプリケーションから中断なくデータを書き込む CD-ROM デバイスへの排他アクセスが必要です。 それ以外の場合、データが書き込まれます正しく、データ破損の原因します。

<span id="Firmware_update_utilities"></span><span id="firmware_update_utilities"></span><span id="FIRMWARE_UPDATE_UTILITIES"></span>ファームウェア更新ユーティリティ  
多くの製造元の CD-ROM デバイスのファームウェア更新プログラムのユーティリティを提供します。 アプリケーションでは、ファームウェアの更新中に、デバイスにコマンドを送信する場合ことは、デバイス使用できなくなります。

排他アクセス メカニズムがなければこれら 2 種類のアプリケーション排他アクセスを提供するベンダーの唯一の方法は、その他のアプリケーションやコンポーネントからの I/O 要求が失敗したカスタム フィルター ドライバーをインストールすることは、この方法によりシステム不安定になります。 CD-ROM デバイスへの排他アクセスを取得するのには、フィルター ドライバーを使用する必要があります。

排他アクセス メカニズムを使用するアプリケーションを送信する必要があります、 [ **IOCTL\_CDROM\_排他\_アクセス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_exclusive_access)パッシブに CD-ROM クラス ドライバーへの要求\_IRQL レベル。 呼び出し元がこの要求を行うと、呼び出し元がで識別文字列を提供する必要があります、 **CallerName**のメンバー [ **CDROM\_排他\_ロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddcdrm/ns-ntddcdrm-_cdrom_exclusive_lock). クラス ドライバーは、排他アクセス権を持つアプリケーションを識別するためにこの文字列を使用します。

アプリケーションは、ロックを試行する前に、デバイスの現在の状態を照会する必要があります。 デバイスが既にロックされている場合、クラス ドライバーは、デバイスの現在の所有者の識別文字列を返します。 デバイスをロックする前に、呼び出し元開く必要があります、読み取り/書き込みアクセス モード。 そのため、呼び出し元は、管理者特権または書き込みのアクセス モードで CD-ROM デバイスを開くアクセス許可が必要です。

CD-ROM クラス ドライバーが、要求を受信することの保証がないために、排他アクセスを要求する呼び出し元が、作成要求をファイル システム ドライバーに送信するだけで CD-ROM デバイスを開きますされません。 代わりに、アプリケーションが使用する必要があります、**SetupDi * * * Xxx*ルーチンをシステム内のすべての CD-ROM デバイス用のインターフェイスを列挙し、適切なデバイスのインターフェイスを開きます。

呼び出し元がドライブ文字を使用してデバイスを表示またはなどのツール名*CdRom0* CD-ROM クラス ドライバーを作成する要求を渡すを 0 に設定されるアクセス モード、ファイル システム ドライバーが保証されます。 この手順によって、アプリケーションを取得するハンドルを与えない、呼び出し元の読み取り/書き込みアクセスをデバイスにあるために、この保証が不十分です。

排他アクセス モードでは、次の特徴があります。

-   排他ロックの所有者のみがデバイスにアクセスできます。

-   システムでは、他のアプリケーションからのアクセスの要求が失敗します。

-   システム プロセス プラグ アンド プレイ (PnP) と power I/O は、通常の方法でパケット (Irp) を要求します。

-   デバイスのメディアの変更通知は無効です。

-   システムでは、ロックされているデバイスのオープン要求が失敗します。

-   送信する他のアプリケーション、 [ **IOCTL\_ストレージ\_クエリ\_プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_query_property) CD-ROM クラス ドライバーへの要求からキャッシュされた情報が表示されます、デバイスがロックされています。 具体的には場合、 [**ストレージ\_クエリ\_型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ne-ntddstor-_storage_query_type)は**PropertyExistsQuery**IOCTL、デバイスの場合は動作は同じになりますロックされていません。 また場合、**ストレージ\_クエリ\_型**は**PropertyStandardQuery**と[**ストレージ\_プロパティ\_ID** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ne-ntddstor-storage_property_id)は**StorageDeviceProperty**または**StorageAdapterProperty**IOCTL が CD-ROM クラス ドライバーにキャッシュされている情報を返します。 他の組み合わせの**ストレージ\_クエリ\_型**と**ストレージ\_プロパティ\_ID**、ステータスステータス値を持つ、IOCTLが失敗しました。\_アクセス\_が拒否されました。

-   送信する他のアプリケーション、 [ **IOCTL\_CDROM\_取得\_照会\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_get_inquiry_data) CD-ROM クラス ドライバーへの要求には、キャッシュされた情報が表示されます。中にデバイスがロックされているし、もできないことがロックされています。

システムでは、次のいずれかが発生した場合、CD-ROM デバイスへの排他アクセスが削除されます。

-   排他ロックの所有者に送信、 [ **IOCTL\_CDROM\_排他\_アクセス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_exclusive_access)と CD-ROM クラス ドライバーへの要求、 **RequestType**のメンバー [ **CDROM\_排他\_アクセス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddcdrm/ns-ntddcdrm-_cdrom_exclusive_access)設定**ExclusiveAccessUnlockDevice**します。

-   排他ロックの所有者では、デバイス ハンドルを閉じます。

-   排他アクセスのロックを所有するアプリケーションを終了します。

デバイスに対する排他アクセスのロックを削除した後には、CD-ROM クラス ドライバーは次の操作を行います。

-   デバイスのメディアの変更通知を有効にします。

-   設定は\_を確認してください\_ボリュームは、システムが、デバイスのファイル システムを再マウントするため、デバイスの拡張機能のフラグします。

-   デバイスのマルチ メディア機能の更新を強制します。

 

 




