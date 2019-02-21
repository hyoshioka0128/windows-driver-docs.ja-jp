---
title: フィルター処理を開始します。
description: フィルター処理を開始します。
ms.assetid: 79ae93bc-0a6d-412a-80ca-ec4f907fb814
keywords:
- I/O 操作の WDK ファイル システム ミニフィルターをフィルター処理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0323bc6d3906004828ad19b5563fd908abd29659
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529232"
---
# <a name="initiating-filtering"></a>フィルター処理を開始します。


## <span id="ddk_initiating_filtering_if"></span><span id="DDK_INITIATING_FILTERING_IF"></span>


呼び出した後[ **FltRegisterFilter**](https://msdn.microsoft.com/library/windows/hardware/ff544305)、ミニフィルター ドライバーの[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)ルーチンを呼び出す通常[ **FltStartFiltering** ](https://msdn.microsoft.com/library/windows/hardware/ff544569) I/O 操作をフィルター処理を開始します。

ミニフィルター ドライバーを呼び出す必要があります[ **FltStartFiltering** ](https://msdn.microsoft.com/library/windows/hardware/ff544569)からその[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)フィルター マネージャーに通知するルーチンをミニフィルター ドライバーを開始する準備がボリュームへのアタッチと、I/O 要求をフィルター処理します。 ミニフィルター ドライバーの呼び出し後**FltStartFiltering**、フィルター マネージャーは I/O 要求にアタッチするボリュームの通知を送ることの完全にアクティブなミニフィルター ドライバーとしてミニフィルター ドライバーを扱います。 ミニフィルター ドライバーは前であってもに、、これらの I/O 要求と通知を受信を開始する準備する必要があります**FltStartFiltering**を返します。

MiniSpy サンプル ドライバーで[ **FltStartFiltering** ](https://msdn.microsoft.com/library/windows/hardware/ff544569)の次のコード例に示すと呼びます。

```cpp
status = FltStartFiltering( MiniSpyData.FilterHandle );
if( !NT_SUCCESS( status )) {
  FltUnregisterFilter( MiniSpyData.FilterHandle );
}
```

場合に呼び出し[ **FltStartFiltering** ](https://msdn.microsoft.com/library/windows/hardware/ff544569)状態が返されません\_ミニフィルター ドライバーに呼び出す必要があります成功すると、 [ **FltUnregisterFilter**](https://msdn.microsoft.com/library/windows/hardware/ff544606)自体の登録を解除します。

 

 




