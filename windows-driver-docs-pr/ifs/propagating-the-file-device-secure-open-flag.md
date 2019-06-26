---
title: FILE_DEVICE_SECURE_OPEN フラグの伝達
description: FILE_DEVICE_SECURE_OPEN フラグの伝達
ms.assetid: cbc254ab-3ac6-44aa-bb16-16d701d5ada7
keywords:
- フィルターをアタッチ、フィルター ドライバー WDK ファイル システム
- ファイル システム フィルター ドライバー WDK、フィルターをアタッチします。
- ファイル システムまたはボリュームにフィルターをアタッチします。
- WDK のボリュームのファイル システム、フィルターをアタッチします。
- FILE_DEVICE_SECURE_OPEN
- FILE_DEVICE_SECURE_OPEN フラグを伝達します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8e409628492ccb90cbefe6e049e531c06b6459eb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385157"
---
# <a name="propagating-the-filedevicesecureopen-flag"></a>ファイルを伝達する\_デバイス\_SECURE\_オープン フラグ


## <span id="ddk_clearing_the_do_device_initializing_flag_if"></span><span id="DDK_CLEARING_THE_DO_DEVICE_INITIALIZING_FLAG_IF"></span>


アタッチした後、フィルター デバイス オブジェクトをファイル システム (はないボリューム)、常に必ずファイルを設定する\_デバイス\_SECURE\_フィルター デバイス オブジェクトが次の下位の値に一致するように必要なオープン フラグデバイス ドライバー スタック オブジェクト。 (このフラグの詳細については、次を参照してください[デバイスの特性を指定する](https://docs.microsoft.com/windows-hardware/drivers/kernel/specifying-device-characteristics)カーネル アーキテクチャの設計ガイドと[**デバイス\_オブジェクト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_device_object)で、。カーネルの参照。)この例は次に示します。

```cpp
if (FlagOn( DeviceObject->Characteristics, FILE_DEVICE_SECURE_OPEN )) {
    SetFlag(myLegacyFilterDeviceObject->Characteristics, FILE_DEVICE_SECURE_OPEN );
}
```

上のコード スニペットで*デバイス オブジェクト*にデバイス オブジェクトへのポインターは、フィルター デバイス オブジェクトがアタッチされているだけです myLegacyFilter*デバイス オブジェクト*フィルター デバイス オブジェクトへのポインターです。自体。

 

 




