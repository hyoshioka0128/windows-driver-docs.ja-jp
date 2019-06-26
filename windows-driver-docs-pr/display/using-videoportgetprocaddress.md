---
title: VideoPortGetProcAddress の使用
description: VideoPortGetProcAddress の使用
ms.assetid: 48dace7e-7ba3-48bf-9788-469ff42f6fe3
keywords:
- ビデオのミニポート ドライバー WDK Windows 2000 では、複数の Windows バージョン VideoPortGetProcAddress
- VideoPortGetProcAddress
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 707c39b096c8faa1d88c610310f86de5224ca8c1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373562"
---
# <a name="using-videoportgetprocaddress"></a>VideoPortGetProcAddress の使用


## <span id="ddk_using_videoportgetprocaddress_gg"></span><span id="DDK_USING_VIDEOPORTGETPROCADDRESS_GG"></span>


ビデオのミニポート ドライバーは、ミニポート ドライバーが新しいオペレーティング システムのバージョンに固有の機能を使用しない限り、NT ベースのオペレーティング システムのバージョンの読み込みおよびそれ以前のオペレーティング システムのバージョンで実行できる 1 つの開発。

ビデオのミニポート ドライバーが読み込まれるときに、 **VideoPortGetProcAddress**のメンバー、 [**ビデオ\_ポート\_CONFIG\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/ns-video-_video_port_config_info)構造体には、ビデオ ポート ドライバーをエクスポートするコールバック ルーチンのアドレスが含まれています。 [ **VideoPortGetProcAddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_port_get_proc_address)します。 ミニポート ドライバーは、このコールバック ルーチンを使用してからエクスポートされたビデオ ポート関数のアドレスを検索する*videoprt.sys*します。 ミニポート ドライバーは、関数のアドレスがある後、は、関数の呼び出しにこのアドレスを使用できます。 これは、次のコード例に示します。

```cpp
  // Useful typedef for a function pointer type
  //   that points to a function with same argument types
  //   as VideoPortCreateSecondaryDisplay
typedef VP_STATUS ( *pFunc(PVOID, PVOID *, ULONG));

  // Declare a pointer to a function
pFunc pVPFunction;

  // Declare a pointer to a VIDEO_PORT_CONFIG_INFO struct
PVIDEO_PORT_CONFIG_INFO pConfigInfo;

  // Call through VideoPortGetProcAddress callback
  //   to get address of VideoPortCreateSecondaryDisplay
pVPFunction = (pFunc)
  ( *(pConfigInfo->VideoPortGetProcAddress)(
                        pDeviceExt, 
                       "VideoPortCreateSecondaryDisplay")
  );
if (NULL == pVPFunction) {
  // Video port does not export the function
  ...
}
else {
  Status = pVPFunction(DevExtension, 
                      &SecondDevExtension,
                       VIDEO_DUALVIEW_REMOVABLE);
} 
```

呼び出した後、 *VideoPortGetProcAddress*コールバック ルーチンが実行すると、 *pVPFunction*いずれかが**NULL**のアドレスを格納または、 **VideoPortCreateSecondaryDisplay**関数。 場合*pVPFunction*は**NULL**ミニポート ドライバーは使用しないで、ビデオ ポート ドライバーでは、検索しようとして、関数はエクスポートされません。 場合*pVPFunction*ない**NULL**、このポインターを使用して、呼び出すことができます**VideoPortCreateSecondaryDisplay**前の例で示すようにします。

 

 





