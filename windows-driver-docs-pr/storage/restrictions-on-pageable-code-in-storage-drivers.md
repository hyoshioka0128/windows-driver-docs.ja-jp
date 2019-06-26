---
title: ストレージ ドライバーでのページング可能コードの制約
description: ストレージ ドライバーでのページング可能コードの制約
ms.assetid: 1958f22f-5563-41e9-9c3f-dec8a4ac80c0
keywords:
- ストレージ ドライバー WDK、ページング可能なコードの制限
- ページング可能なコードの制限の WDK ストレージ
- デッドロック WDK ストレージ
- ページング パス WDK ストレージ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3515a0b9e1a9f87df9679fd1dd1ad0430018aac4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373196"
---
# <a name="restrictions-on-pageable-code-in-storage-drivers"></a>ストレージ ドライバーでのページング可能コードの制約


## <span id="ddk_restrictions_on_pageable_code_in_storage_drivers_kg"></span><span id="DDK_RESTRICTIONS_ON_PAGEABLE_CODE_IN_STORAGE_DRIVERS_KG"></span>


デッドロックを防ぐためには、サービスに使用する記憶装置ドライバーの一部の読み取りまたは書き込み要求は、ページング可能なコードが必要でもページング可能なメモリにアクセスするまで試行する必要があります。 これは、ドライバーの[ **DispatchRead** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)と[ **DispatchWrite** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch) IRQL でルーチンを呼び出すことができます&gt;パッシブ\_レベル、および IRQL でページ フォールトの受け取り場所サービスを提供するページングで I/O APC を =\_レベル。

ストレージ ドライバーのデバイス管理のディスパッチ ルーチンに同様のルールを適用[ **DispatchDeviceControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)、特定の制限があります。 記憶装置ドライバーのデバイス制御ディスパッチ ルーチンには、ページング可能なコードまたはアクセス ページング可能なメモリが含まれていない必要があります。 ディスパッチ ルーチンは、任意の Irql で他のドライバーのためのものでは、ドライバー スタックを渡したり IOCTL 要求を受信できる必要があります。 ドライバー*する必要があります*IRQL または要求のコンテキストを変更することがなく、下位のスタックのすべての未処理の IOCTL 要求を渡します。

Microsoft では、する必要がすべて*ストレージ*IOCTL 要求はパッシブで提出する\_レベルで、ディスパッチ ルーチンは、それ自体ではありませんが、ページングを呼び出すことがストレージ IOCTL 要求を処理するサブルーチンをページング可能な。 これらのサブルーチンでは、ページング可能なメモリもアクセスできます。

などのルーチン[ **DriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)、 [**を再初期化**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nc-ntddk-driver_reinitialize)、および[**アンロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_unload)、I/O をしないし、IRQL で実行を = パッシブ\_レベルでは、ページング可能なコードはこともできます。

ページングのパスでの記憶域デバイスを管理するドライバーに特別な考慮事項が適用されます。 ドライバーが、「ページング パス」ページング ファイルの I/O 操作に含まれているかどうか。 ページングのパスが記憶装置ドライバーの場合、 [ **DispatchPower** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch) IRP の日常的な\_MJ\_POWER 要求をページングすることはできません。

既定では、カーネル モード ドライバー用のコードはページング可能なもがグローバル メモリをページング可能なカーネル モード ドライバーで使用します。 ページング可能なコードを作成する方法については、次を参照してください。[ドライバー コードの作成やページング可能なデータ](https://docs.microsoft.com/windows-hardware/drivers/kernel/making-driver-code-or-data-pageable)します。

 

 




