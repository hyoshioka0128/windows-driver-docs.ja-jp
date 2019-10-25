---
title: DO_DEVICE_INITIALIZING フラグのクリア
description: DO_DEVICE_INITIALIZING フラグのクリア
ms.assetid: 1c1cca60-bb95-4a8d-9e17-4db54983bbb0
keywords:
- フィルタードライバー WDK ファイルシステム、フィルターのアタッチ
- ファイルシステムフィルタードライバー WDK、添付フィルター
- ファイルシステムまたはボリュームへのフィルターのアタッチ
- ボリューム WDK ファイルシステム、フィルターのアタッチ
- DO_DEVICE_INITIALIZING
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: acb85c2c7a922dd0e06ac8b6ef363a7a29183c03
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841473"
---
# <a name="clearing-the-do_device_initializing-flag"></a>DO\_デバイス\_初期化フラグをクリアしています


## <span id="ddk_clearing_the_do_device_initializing_flag_if"></span><span id="DDK_CLEARING_THE_DO_DEVICE_INITIALIZING_FLAG_IF"></span>


フィルターデバイスオブジェクトをファイルシステムまたはボリュームにアタッチした後は、常に、フィルターデバイスオブジェクトの [初期化] フラグをオフにして、[デバイスの\_\_を初期化する] を選択します。 (このフラグの詳細については、「カーネルリファレンス」の「 [**DEVICE\_オブジェクト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_object)」を参照してください)。これは、 *ntifs*で定義されている**clearflag**マクロを使用して、次のように実行できます。

```cpp
ClearFlag(NewDeviceObject->Flags, DO_DEVICE_INITIALIZING);
```

フィルターデバイスオブジェクトが作成されると、 [**IoCreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice)はデバイスオブジェクトの初期化フラグ\_DO\_デバイスを設定します。 フィルターが正常にアタッチされたら、このフラグをクリアする必要があります。 このフラグがオフになっていない場合は、 [**Ioattachdevicetodevicestacksafe**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioattachdevicetodevicestacksafe)の呼び出しが失敗するため、これ以上フィルタードライバーをフィルターチェーンにアタッチすることはできません。

**注意**   driverentry で作成されたデバイスオブジェクトに対して、DO\_デバイス\_初期化フラグをクリアする必要はありません。これは、i/o マネージャーによって自動的に行われるためです。 ただし、ドライバーは、作成する他のすべてのデバイスオブジェクトでこのフラグをクリアする必要があります。

 

 

 




