---
title: DO_DEVICE_INITIALIZING フラグのクリア
description: DO_DEVICE_INITIALIZING フラグのクリア
ms.assetid: 1c1cca60-bb95-4a8d-9e17-4db54983bbb0
keywords:
- フィルターをアタッチ、フィルター ドライバー WDK ファイル システム
- ファイル システム フィルター ドライバー WDK、フィルターをアタッチします。
- ファイル システムまたはボリュームにフィルターをアタッチします。
- WDK のボリュームのファイル システム、フィルターをアタッチします。
- DO_DEVICE_INITIALIZING
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5bcd78c2ea07d6bd5550cada1c16b158ef062d75
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379000"
---
# <a name="clearing-the-dodeviceinitializing-flag"></a>オフ\_デバイス\_初期化フラグ


## <span id="ddk_clearing_the_do_device_initializing_flag_if"></span><span id="DDK_CLEARING_THE_DO_DEVICE_INITIALIZING_FLAG_IF"></span>


ファイル システムまたはボリュームをフィルター デバイス オブジェクトをアタッチした後を必ずオフにします\_デバイス\_フィルター デバイス オブジェクトの初期化フラグ。 (このフラグの詳細については、次を参照してください[**デバイス\_オブジェクト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_device_object)でカーネルの参照。)。これを使用して次のように、 **ClearFlag**マクロで定義されている*ntifs.h*:

```cpp
ClearFlag(NewDeviceObject->Flags, DO_DEVICE_INITIALIZING);
```

フィルターのデバイス オブジェクトが作成されると、 [ **IoCreateDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocreatedevice)設定、DO\_デバイス\_デバイス オブジェクトの初期化フラグ。 フィルターが正常に接続されると、このフラグをクリアする必要があります。 場合、このフラグをオフにすると、フィルター ドライバーにアタッチできるフィルター チェーンのために注意してください。 呼び出し[ **IoAttachDeviceToDeviceStackSafe** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-ioattachdevicetodevicestacksafe)は失敗します。

**注**   、操作をクリアする必要はありません\_デバイス\_のため、これは、自動的に I/O マネージャーによって、DriverEntry 内に作成したデバイス オブジェクトの初期化フラグ。 ただし、ドライバーを作成する他のすべてのデバイス オブジェクトでは、このフラグをオフにする必要があります。

 

 

 




