---
title: FILE_DEVICE_SECURE_OPEN フラグの伝達
description: FILE_DEVICE_SECURE_OPEN フラグの伝達
ms.assetid: cbc254ab-3ac6-44aa-bb16-16d701d5ada7
keywords:
- フィルタードライバー WDK ファイルシステム、フィルターのアタッチ
- ファイルシステムフィルタードライバー WDK、添付フィルター
- ファイルシステムまたはボリュームへのフィルターのアタッチ
- ボリューム WDK ファイルシステム、フィルターのアタッチ
- FILE_DEVICE_SECURE_OPEN
- FILE_DEVICE_SECURE_OPEN フラグを伝達しています
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 461d9dcd3394106f949699e8ff6d6871ed287aba
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841021"
---
# <a name="propagating-the-file_device_secure_open-flag"></a>ファイル\_デバイス\_セキュリティで保護された\_開くフラグを伝達する


## <span id="ddk_clearing_the_do_device_initializing_flag_if"></span><span id="DDK_CLEARING_THE_DO_DEVICE_INITIALIZING_FLAG_IF"></span>


フィルターデバイスオブジェクトをファイルシステムにアタッチした後 (ボリュームではない)、常に、ファイル\_\_デバイスに対して、必要に応じてフィルターデバイスオブジェクトの [セキュリティで保護された\_開く] フラグが設定されていることを確認してください。ドライバースタック。 (このフラグの詳細については、「カーネルアーキテクチャ設計ガイド」と「デバイス[ **\_オブジェクト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_object)」の「[デバイスの特性の指定](https://docs.microsoft.com/windows-hardware/drivers/kernel/specifying-device-characteristics)」を参照してください)。この例を次に示します。

```cpp
if (FlagOn( DeviceObject->Characteristics, FILE_DEVICE_SECURE_OPEN )) {
    SetFlag(myLegacyFilterDeviceObject->Characteristics, FILE_DEVICE_SECURE_OPEN );
}
```

上記のコードスニペットでは、 *DeviceObject*は、フィルターデバイスオブジェクトがアタッチされた直前のデバイスオブジェクトへのポインターです。myLegacyFilter *DeviceObject*は、フィルターデバイスオブジェクト自体へのポインターです。

 

 




