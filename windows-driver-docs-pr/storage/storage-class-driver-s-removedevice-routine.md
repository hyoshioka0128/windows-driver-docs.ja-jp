---
title: 記憶域クラス ドライバーの RemoveDevice ルーチン
description: 記憶域クラス ドライバーの RemoveDevice ルーチン
ms.assetid: fbcbfbab-676a-43d3-aa63-0ea5e5f265d2
keywords:
- RemoveDevice
- クエリ-削除要求の WDK ストレージ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1bbe81c56d26e1de1e97380c8f353d552e424acc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845287"
---
# <a name="storage-class-drivers-removedevice-routine"></a>記憶域クラス ドライバーの RemoveDevice ルーチン


## <span id="ddk_storage_class_drivers_removedevice_routine_kg"></span><span id="DDK_STORAGE_CLASS_DRIVERS_REMOVEDEVICE_ROUTINE_KG"></span>


デバイスを削除しようとしているときに、PnP マネージャーはまず、PnP クエリ削除要求 (IRP\_MJ\_PNP と Irp\_を使用して、クラスドライバーの[**DispatchPnP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンを呼び出します。 [ **\_デバイスの削除\_\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-remove-device) ストレージクラスドライバーは、次のいずれかの場合にクエリ削除要求を失敗させる必要があります。

-   デバイスには、システムページングファイルまたは休止状態ファイルが含まれています。

-   ドライバーが長時間の操作を実行しています。この操作はキャンセルできません (テープの巻き戻しやフォーマットなど)。

-   デバイスへの未処理ハンドルがあります (が作成します)。

また、このようなデバイスを削除するとクラッシュダンプが無効になるため、デバイスにクラッシュダンプが要求された場合、ストレージクラスドライバーはクエリ削除要求に失敗することもあります。

ストレージクラスドライバーがクエリ削除要求に応答して STATUS\_SUCCESS を返した場合、PnP マネージャーは、PnP 削除要求 (IRP\_MJ\_PNP with Irp\_を使用して、クラスドライバーの*DispatchPnP*ルーチンを呼び出し[ **\_\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)) を削除します。 ストレージクラスドライバーの*DispatchPnP*ルーチンは、内部*removedevice*ルーチンを呼び出すか、同じ機能をインラインで実装します。

ストレージクラスドライバーの*Removedevice*ルーチンは、次の操作を行う必要があります。

-   ドライバーによって割り当てられたメモリやイベントなど、未解決のリソースを解放します。

-   ドライバーによって作成されたシンボリックリンクがある場合は削除します。

-   デバイスオブジェクト (FDO) を削除します。

-   要求を次の下位のドライバーに転送します。

記憶域クラスドライバーが起動時に PDOs を作成した場合 (パーティション分割されたメディアデバイスのパーティションを表す場合など)、PnP マネージャーが削除要求をストレージクラスドライバーに送信すると、このような PDOs は既に削除されています。

デバイスオブジェクトが削除された後でも、0以外の参照カウントがある場合、デバイスオブジェクトはその参照カウントが0になるまでシステム内に保持され、その後、デバイスオブジェクトは警告なしに消えます。 デバイスオブジェクトが削除された後、ストレージクラスドライバーはデバイスオブジェクトポインターを使用しないようにする必要があります。

削除要求の処理の詳細については、「[デバイスの削除](https://docs.microsoft.com/windows-hardware/drivers/kernel/removing-a-device)」を参照してください。

 

 




