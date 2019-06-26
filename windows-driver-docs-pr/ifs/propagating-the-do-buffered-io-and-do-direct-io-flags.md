---
title: DO_BUFFERED_IO と DO_DIRECT_IO フラグの伝達
description: DO_BUFFERED_IO と DO_DIRECT_IO フラグの伝達
ms.assetid: a0cb4f1a-3c27-4608-a208-ffcf4113b722
keywords:
- フィルターをアタッチ、フィルター ドライバー WDK ファイル システム
- ファイル システム フィルター ドライバー WDK、フィルターをアタッチします。
- ファイル システムまたはボリュームにフィルターをアタッチします。
- WDK のボリュームのファイル システム、フィルターをアタッチします。
- DO_BUFFERED_IO
- DO_BUFFERED_IO フラグを伝達します。
- DO_DIRECT_IO
- DO_DIRECT_IO フラグを伝達します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cbeb0547871751cc628c1dcb6c038b7ffc8d81db
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385149"
---
# <a name="propagating-the-dobufferedio-and-dodirectio-flags"></a>メッセージを伝達する\_バッファーに格納された\_IO、および DO\_直接\_IO フラグ


## <span id="ddk_propagating_the_do_buffered_io_and_do_direct_io_flags_if"></span><span id="DDK_PROPAGATING_THE_DO_BUFFERED_IO_AND_DO_DIRECT_IO_FLAGS_IF"></span>


ファイル システムまたはボリュームをフィルター デバイス オブジェクトをアタッチした後は必ずを設定するかオフにします\_バッファーに格納された\_IO、および DO\_直接\_IO フラグの下のデバイスの値と一致するように、必要に応じてドライバー スタック上のオブジェクト。 (これらのフラグの詳細については、次を参照してください[メソッドにアクセスするデータ バッファーの](https://docs.microsoft.com/windows-hardware/drivers/kernel/methods-for-accessing-data-buffers)。)。この例は次に示します。

```cpp
if (FlagOn( DeviceObject->Flags, DO_BUFFERED_IO )) {
    SetFlag( myLegacyFilterDeviceObject->Flags, DO_BUFFERED_IO );
}
if (FlagOn( DeviceObject->Flags, DO_DIRECT_IO )) {
    SetFlag(myLegacyFilterDeviceObject->Flags, DO_DIRECT_IO );
}
```

上のコード スニペットで*デバイス オブジェクト*にデバイス オブジェクトへのポインターは、フィルター デバイス オブジェクトがアタッチされているだけです myLegacyFilter*デバイス オブジェクト*フィルター デバイス オブジェクトへのポインターです。自体。

 

 




