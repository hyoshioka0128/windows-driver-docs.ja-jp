---
title: CD-ROM 専用アクセスモード
description: CD-ROM 専用アクセスモード
ms.assetid: 4432f6d6-e98c-4354-a7ba-b043a624f064
keywords:
- CD-ROM ドライバー WDK ストレージ
- 記憶域 CD-ROM ドライバー WDK
- 排他アクセスモード WDK CD-ROM
- IOCTL_CDROM_EXCLUSIVE_ACCESS
- CDROM_EXCLUSIVE_LOCK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 481511f34a27c5fd4e72bd5b7c65aea4b2ea453b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841634"
---
# <a name="cd-rom-exclusive-access-mode"></a>CD-ROM 専用アクセスモード


CD-ROM*専用アクセス*メカニズム (*排他アクセスモード*とも呼ばれます) を使用すると、アプリケーションおよびシステムコンポーネントは cd-rom デバイスへの排他アクセスを取得できます。 CD-ROM デバイスへの排他的アクセスを必要とするアプリケーションには、次の例が含まれます。

<span id="Optical_media-authoring_applications"></span><span id="optical_media-authoring_applications"></span><span id="OPTICAL_MEDIA-AUTHORING_APPLICATIONS"></span>光学式メディア-アプリケーションの作成  
一部の光学作成ソフトウェアでは、他のアプリケーションを中断することなく、データを書き込むために CD-ROM デバイスに排他的にアクセスする必要があります。 そうしないと、データが誤って書き込まれ、データが破損する可能性があります。

<span id="Firmware_update_utilities"></span><span id="firmware_update_utilities"></span><span id="FIRMWARE_UPDATE_UTILITIES"></span>ファームウェア更新ユーティリティ  
多くの CD-ROM デバイスの製造元は、ファームウェア更新ユーティリティを提供しています。 ファームウェアの更新中にアプリケーションがデバイスにコマンドを送信すると、デバイスが使用できなくなる可能性があります。

排他的アクセスメカニズムを使用しない場合、この2種類のアプリケーションに排他アクセス権を付与する唯一の方法は、他のアプリケーションやコンポーネントからの i/o 要求を失敗させるカスタムフィルタードライバーをインストールすることです。この方法ではシステムがたり. フィルタードライバーを使用して、CD-ROM デバイスへの排他アクセスを取得しないでください。

排他的アクセスメカニズムを使用するには、アプリケーションは、ROM [ **\_cd-rom\_排他\_アクセス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_exclusive_access)要求を、パッシブ\_レベルの IRQL で cd-rom クラスドライバーに送信する必要があります。 呼び出し元がこの要求を行うときに、呼び出し元は、CDROM の**Callername**メンバー [ **\_排他\_ロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ns-ntddcdrm-_cdrom_exclusive_lock)に識別文字列を提供する必要があります。 クラスドライバーは、この文字列を使用して、排他アクセスを持つアプリケーションを識別します。

アプリケーションは、デバイスのロックを試行する前に、デバイスの現在の状態を照会する必要があります。 デバイスが既にロックされている場合、クラスドライバーはデバイスの現在の所有者の識別文字列を返します。 デバイスをロックする前に、呼び出し元は、デバイスを読み取り/書き込みアクセスモードで開く必要があります。 そのため、呼び出し元には、書き込みアクセスモードで CD-ROM デバイスを開くための管理者特権またはアクセス許可が必要です。

排他アクセスを要求する呼び出し元は、ファイルシステムドライバーに作成要求を送信するだけで CD-ROM デバイスを開けないようにする必要があります。これは、CD-ROM クラスドライバーが要求を受信する保証がないためです。 代わりに、アプリケーションは**Setupdi**_Xxx_ルーチンを使用して、システム内のすべての cd-rom デバイスのインターフェイスを列挙し、適切なデバイスインターフェイスを開く必要があります。

呼び出し元が、アクセスモードが0に設定されたドライブ文字または*CdRom0*のような名前を使用してデバイスを開くと、ファイルシステムドライバーは、cd-rom クラスドライバーに作成要求を渡すことが保証されます。 ただし、このような保証は依然として十分ではありません。これは、アプリケーションがこのプロシージャによって取得するハンドルによって、デバイスへの読み取り/書き込みアクセスが呼び出し元に付与されないためです。

排他アクセスモードには、次の特性があります。

-   排他アクセスロックの所有者だけがデバイスにアクセスできます。

-   システムは、他のアプリケーションからのアクセスの要求に失敗します。

-   システムは、通常の方法でプラグアンドプレイ (PnP) と電源 i/o 要求パケット (Irp) を処理します。

-   デバイスのメディア変更通知が無効になっています。

-   システムは、ロックされている間にデバイスを開く要求を失敗させます。

-   [**IOCTL\_STORAGE\_QUERY\_PROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_query_property)要求を送信するその他のアプリケーションは、ロックされている間、デバイスからキャッシュされた情報を受け取ります。 具体的には、 [**STORAGE\_QUERY\_TYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ne-ntddstor-_storage_query_type)が**PropertyExistsQuery**の場合、IOCTL は、デバイスがロックされていない場合と同様に動作します。 また、 **storage\_QUERY\_TYPE**が**Propertystandardquery**で、 [**storage\_プロパティ\_ID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ne-ntddstor-storage_property_id)が**storagedeviceproperty**または**storagedeviceproperty**の場合、IOCTL はを返します。CD-ROM クラスドライバーにキャッシュされている情報。 **ストレージ\_クエリ\_種類**および**ストレージ\_プロパティ\_ID**の他の組み合わせでは、IOCTL が失敗し、状態値の状態が "\_アクセス\_拒否" になります。

-   \_IOCTL\_CDROM に送信するその他のアプリケーションは、CD-ROM クラスドライバーに[ **\_照会\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_get_inquiry_data)要求を取得し、ロックされている間、およびロックが解除されたときに、デバイスからキャッシュされた情報を受け取ります。

次のいずれかが発生すると、システムによって CD-ROM デバイスへの排他アクセスが削除されます。

-   排他アクセスロックの所有者は、cd-rom に排他的な[ **\_アクセス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_exclusive_access)要求を送信します。これは、Cd-rom の**RequestType**メンバーを使用して、 [ **\_排他\_アクセス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ns-ntddcdrm-_cdrom_exclusive_access)をに**設定して、\_\_ExclusiveAccessUnlockDevice**。

-   排他アクセスロックの所有者は、デバイスハンドルを閉じます。

-   排他アクセスロックを所有するアプリケーションは終了します。

デバイスで排他アクセスロックを削除した後、CD-ROM クラスドライバーは次の操作を実行します。

-   デバイスでメディア変更通知を有効にします。

-   デバイスの拡張子に DO\_VERIFY\_ボリュームフラグを設定し、システムによってデバイスのファイルシステムが再マウントされるようにします。

-   デバイスのマルチメディア機能を強制的に更新します。

 

 




