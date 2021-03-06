---
title: 記憶域クラス ドライバーの AddDevice ルーチン
description: 記憶域クラス ドライバーの AddDevice ルーチン
ms.assetid: ff07ae84-2748-44b4-88c6-e67f1d4c9268
keywords:
- AddDevice ルーチン WDK ストレージ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4326cd34a62c8c71d226837bd15bd141ede99752
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376893"
---
# <a name="storage-class-drivers-adddevice-routine"></a>記憶域クラス ドライバーの AddDevice ルーチン


## <span id="ddk_storage_class_drivers_adddevice_routine_kg"></span><span id="DDK_STORAGE_CLASS_DRIVERS_ADDDEVICE_ROUTINE_KG"></span>


PnP マネージャーには、記憶域クラス ドライバーの[ **AddDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)ルーチンは、ドライバーによって制御されるデバイスを検出した場合。 記憶域クラス ドライバーの*AddDevice*ルーチン。

-   」の説明に従って、デバイスを要求[記憶域クラス ドライバー ClaimDevice ルーチン](storage-class-driver-s-claimdevice-routine.md)、ドライバーは、デバイスを要求できない場合は、ステータスを返しますまたは、\_成功します。

-   ドライバーが正常にデバイスを要求する場合は、デバイス オブジェクト (FDO) を作成します。

-   アプリケーションおよびその他のシステム デバイス使用してデバイスのインターフェイスを登録します。 クラス ドライバーは、PnP 開始要求を受け取ったときにこのようなインターフェイスを使用します。

-   」の説明に従って開始要求を処理するためにデバイス オブジェクトを準備します[、AddDevice ルーチンを記述](https://docs.microsoft.com/windows-hardware/drivers/kernel/writing-an-adddevice-routine)します。

-   デバイス スタックを呼び出すことによって、デバイス オブジェクトをアタッチします[ **IoAttachDeviceToDeviceStack** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioattachdevicetodevicestack)入力 PDO を使用します。

-   デバイスは、既知の電源状態で起動する場合は、呼び出し[ **PoSetPowerState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-posetpowerstate)します。

-   実行をクリアします\_デバイス\_新しいデバイス オブジェクトの初期化フラグ。

ストレージ クラス ドライバーによって返されたポインターを格納する**IoAttachDeviceToDeviceStack**新しく要求されたデバイスを表す独自デバイス オブジェクト (FDO) の拡張機能でデバイスと*すべてでこのポインターを使用する必要がありますクラス ドライバーは、次の下位ドライバーに送信する後続の要求*します。 ドライバーは、デバイス拡張機能の後に入力 PDO へのポインターを格納するも**IoAttachDeviceToDeviceStack** 、ドライバーは PnP への呼び出しでのみ入力 PDO へのポインターを使用する必要がありますを返します **Io * * * Xxx*パラメーターとしてこのようなポインターを使用するルーチン。

詳細については、次を参照してください。 [、AddDevice ルーチンを記述](https://docs.microsoft.com/windows-hardware/drivers/kernel/writing-an-adddevice-routine)します。

 

 




