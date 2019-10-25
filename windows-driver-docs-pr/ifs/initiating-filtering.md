---
title: フィルタリングの開始
description: フィルタリングの開始
ms.assetid: 79ae93bc-0a6d-412a-80ca-ec4f907fb814
keywords:
- i/o 操作のフィルター選択 WDK ファイルシステムミニフィルター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 694f1110442735cd1468010eb55136a86f2fa01b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841198"
---
# <a name="initiating-filtering"></a>フィルタリングの開始


## <span id="ddk_initiating_filtering_if"></span><span id="DDK_INITIATING_FILTERING_IF"></span>


[**Fltregisterfilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltregisterfilter)を呼び出した後、ミニフィルタードライバーの[**driverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)ルーチンは通常[**fltregisterfilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltstartfiltering)を呼び出して、i/o 操作のフィルター処理を開始します。

すべてのミニフィルタードライバーは、 [**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)ルーチンから[**Fltstartfiltering**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltstartfiltering)を呼び出して、フィルタマネージャーに対して、ミニフィルタードライバーがボリュームへのアタッチと i/o 要求のフィルター処理を開始する準備ができていることを通知する必要があります。 ミニフィルタドライバが**Fltstartfiltering**を呼び出した後、フィルタマネージャはミニフィルタドライバを完全にアクティブなミニフィルタドライバとして扱い、i/o 要求およびアタッチするボリュームの通知を表示します。 **Fltstartfiltering**が返される前に、ミニフィルタードライバーは、これらの i/o 要求と通知の受信を開始できるように準備する必要があります。

MiniSpy サンプルドライバーでは、次のコード例に示すように[**Fltstartfiltering**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltstartfiltering)が呼び出されます。

```cpp
status = FltStartFiltering( MiniSpyData.FilterHandle );
if( !NT_SUCCESS( status )) {
  FltUnregisterFilter( MiniSpyData.FilterHandle );
}
```

[**Fltstartfiltering**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltstartfiltering)を呼び出すとステータス\_SUCCESS が返されない場合、ミニフィルタードライバーは[**Fltstartfiltering**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltunregisterfilter)を呼び出して自身の登録を解除する必要があります。

 

 




