---
title: ストレージ ドライバーとデバイス オブジェクト
description: ストレージ ドライバーとデバイス オブジェクト
ms.assetid: dbadebe6-b2ae-4dc2-837b-5ca9634d45d0
keywords:
- ストレージ ドライバー WDK、デバイス オブジェクト
- デバイス オブジェクトの WDK ストレージ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 48e4230247c14a44c11683c70800785d5ce79b1f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376389"
---
# <a name="storage-drivers-and-device-objects"></a>ストレージ ドライバーとデバイス オブジェクト


## <span id="ddk_storage_drivers_and_device_objects_kg"></span><span id="DDK_STORAGE_DRIVERS_AND_DEVICE_OBJECTS_KG"></span>


記憶域デバイス スタックは、システム上の記憶域デバイスへの I/O の処理に関連するドライバーによって作成されたデバイス オブジェクトのツリーで構成されます。 このツリーのルートは、記憶域アダプターまたは記憶域スタックと統合されて、別のドライバー スタックの機能のデバイス オブジェクト (FDO) です。 このツリーのリーフは、ファイル システムとユーザー モード アプリケーションで使用するためのデバイス オブジェクトです。

PnP ドライバーや記憶域クラス、記憶域フィルター ドライバー自体に追加、AddDevice ルーチンで、ツリーを使用して、デバイス オブジェクトを作成するよう**IoCreateDevice**でデバイス スタックへの追加と**IoAttachDeviceToDeviceStack**初期化時、PnP マネージャーによってドライバーの AddDevice ルーチンに渡されるデバイス オブジェクトへのポインターを使用しています。 **IoAttachDeviceToDeviceStack**デバイス スタックの現在の先頭に新しいデバイス オブジェクトをアタッチします。

テープ miniclass、メディア チェンジャー miniclass、または SCSI ミニポート ドライバーは、デバイス オブジェクトを作成し、デバイス スタックをアタッチする必要はありません。 代わりに、システムが指定したテープのクラス、チェンジャー クラス、または SCSI ポート ドライバーに代わって miniclass/ミニポート デバイス オブジェクトを作成するために必要なデータを収集するドライバー ルーチンを呼び出す miniclass/ミニポート、これらのタスクを処理します。

記憶域ポート ドライバー ファイルの種類の物理デバイス オブジェクト (Pdo) を作成する\_デバイス\_大容量\_ストレージ。 クラスのディスク、CD-ROM クラス、tape クラスおよびチェンジャー クラス ドライバーは、作成ファイルの種類の Fdo\_デバイス\_ディスク、ファイル\_デバイス\_CD\_ROM]、[ファイル\_デバイス\_テープ、ファイルと\_デバイス\_チェンジャーそれぞれします。

PnP ドライバーのデザイン方法の詳細については、次を参照してください。、 [PnP ドライバー設計のガイドライン](https://docs.microsoft.com/windows-hardware/drivers/kernel/pnp-driver-design-guidelines)します。 PnP 関連について **Io * * * Xxx*ルーチンを参照してください、[プラグ アンド プレイ ルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)します。

 

 




