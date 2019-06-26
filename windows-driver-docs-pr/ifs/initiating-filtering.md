---
title: フィルタリングの開始
description: フィルタリングの開始
ms.assetid: 79ae93bc-0a6d-412a-80ca-ec4f907fb814
keywords:
- I/O 操作の WDK ファイル システム ミニフィルターをフィルター処理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 90083473c6739f62168313d09df8a50b6189d2dd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381742"
---
# <a name="initiating-filtering"></a>フィルタリングの開始


## <span id="ddk_initiating_filtering_if"></span><span id="DDK_INITIATING_FILTERING_IF"></span>


呼び出した後[ **FltRegisterFilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltregisterfilter)、ミニフィルター ドライバーの[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)ルーチンを呼び出す通常[ **FltStartFiltering** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltstartfiltering) I/O 操作をフィルター処理を開始します。

ミニフィルター ドライバーを呼び出す必要があります[ **FltStartFiltering** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltstartfiltering)からその[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)フィルター マネージャーに通知するルーチンをミニフィルター ドライバーを開始する準備がボリュームへのアタッチと、I/O 要求をフィルター処理します。 ミニフィルター ドライバーの呼び出し後**FltStartFiltering**、フィルター マネージャーは I/O 要求にアタッチするボリュームの通知を送ることの完全にアクティブなミニフィルター ドライバーとしてミニフィルター ドライバーを扱います。 ミニフィルター ドライバーは前であってもに、、これらの I/O 要求と通知を受信を開始する準備する必要があります**FltStartFiltering**を返します。

MiniSpy サンプル ドライバーで[ **FltStartFiltering** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltstartfiltering)の次のコード例に示すと呼びます。

```cpp
status = FltStartFiltering( MiniSpyData.FilterHandle );
if( !NT_SUCCESS( status )) {
  FltUnregisterFilter( MiniSpyData.FilterHandle );
}
```

場合に呼び出し[ **FltStartFiltering** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltstartfiltering)状態が返されません\_ミニフィルター ドライバーに呼び出す必要があります成功すると、 [ **FltUnregisterFilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltunregisterfilter)自体の登録を解除します。

 

 




