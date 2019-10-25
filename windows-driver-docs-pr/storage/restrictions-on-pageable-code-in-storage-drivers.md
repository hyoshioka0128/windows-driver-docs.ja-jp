---
title: ストレージ ドライバーでのページング可能コードの制約
description: ストレージ ドライバーでのページング可能コードの制約
ms.assetid: 1958f22f-5563-41e9-9c3f-dec8a4ac80c0
keywords:
- ストレージドライバー WDK、ページング可能コードの制限
- ページング可能コード制限 WDK ストレージ
- デッドロックの WDK ストレージ
- ページングパス WDK ストレージ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4c7709745645db21eedc8853e7e6068e10145478
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842691"
---
# <a name="restrictions-on-pageable-code-in-storage-drivers"></a>ストレージ ドライバーでのページング可能コードの制約


## <span id="ddk_restrictions_on_pageable_code_in_storage_drivers_kg"></span><span id="DDK_RESTRICTIONS_ON_PAGEABLE_CODE_IN_STORAGE_DRIVERS_KG"></span>


デッドロックを防ぐために、読み取り要求または書き込み要求を処理するために使用されるストレージドライバーには、ページング可能なコードが含まれている必要はありません。また、ページング可能なメモリにアクセスしようとする必要もありません。 これは、ドライバーの[**DispatchRead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンと[**DispatchWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンを &gt; パッシブ\_レベルの irql で呼び出すことができ、ページフォールトを処理するページングを行う i/o は、IRQL = APC\_レベルで行われるためです。

同様の規則は、特定の条件を満たした記憶域ドライバーのデバイス制御ディスパッチルーチン[**DispatchDeviceControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)に適用されます。 ストレージドライバーのデバイス制御ディスパッチルーチンには、ページング可能なコードを含めたり、ページング可能なメモリにアクセスしたりすることはできません。 ディスパッチルーチンは、任意の IRQLs で他のドライバーを対象とする IOCTL 要求を受信し、ドライバースタックに渡すことができる必要があります。 ドライバーは、要求の IRQL またはコンテキストを変更せずに、スタック内のすべての未処理の IOCTL 要求を渡す*必要があり*ます。

ただし、Microsoft では、すべての*ストレージ*ioctl 要求をパッシブ\_レベルで送信する必要があります。そのため、ディスパッチルーチン自体はページング可能ではありませんが、ページング可能なサブルーチンを呼び出してストレージ ioctl 要求を処理することができます。 これらのサブルーチンは、ページング可能なメモリにアクセスすることもできます。

[**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)、[**再初期化**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nc-ntddk-driver_reinitialize)、[**アンロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)など、i/o を行わず、IRQL = パッシブ\_レベルで実行されるルーチンも、ページング可能なコードを持つことができます。

ページングパスで記憶デバイスを管理するドライバーには、特別な考慮事項が適用されます。 ページングファイルに i/o 操作が含まれている場合、ドライバーは "ページングパス" にあります。 ストレージドライバーがページングパスにある場合、IRP\_MJ\_の[**DispatchPower**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンは、ページングを行うことができません。

既定では、カーネルモードドライバーのコードはページングできません。また、カーネルモードドライバーによって使用されるグローバルメモリもページングされません。 コードをページング可能にする方法の詳細については、「[ドライバーコードまたはデータをページング](https://docs.microsoft.com/windows-hardware/drivers/kernel/making-driver-code-or-data-pageable)できるようにする」を参照してください。

 

 




