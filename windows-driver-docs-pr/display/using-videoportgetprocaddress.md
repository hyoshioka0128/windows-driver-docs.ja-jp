---
title: VideoPortGetProcAddress の使用
description: VideoPortGetProcAddress の使用
ms.assetid: 48dace7e-7ba3-48bf-9788-469ff42f6fe3
keywords:
- ビデオミニポートドライバー WDK Windows 2000、複数の Windows バージョン、VideoPortGetProcAddress
- VideoPortGetProcAddress
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c90318c70415fe2eddea702cfa9fcf5b4598d5fb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829240"
---
# <a name="using-videoportgetprocaddress"></a>VideoPortGetProcAddress の使用


## <span id="ddk_using_videoportgetprocaddress_gg"></span><span id="DDK_USING_VIDEOPORTGETPROCADDRESS_GG"></span>


ある NT ベースのオペレーティングシステムのバージョンで開発されたビデオミニポートドライバーは、新しいオペレーティングシステムのバージョンに固有の機能をミニポートドライバーが使用しない限り、以前のバージョンのオペレーティングシステムでも読み込むことができます。

ビデオミニポートドライバーが読み込まれると 、VIDEO [ **\_PORT\_CONFIG\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/ns-video-_video_port_config_info)構造体の VideoPortGetProcAddress メンバーには、ビデオポートドライバーによってエクスポート[**されるコールバックルーチンのアドレスが含まれます。VideoPortGetProcAddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_port_get_proc_address)。 ミニポートドライバーは、このコールバックルーチンを使用して、 *videoprt*からエクスポートされたビデオポート関数のアドレスを見つけることができます。 ミニポートドライバーには、関数のアドレスがあると、このアドレスを使用して関数を呼び出すことができます。 これを次のコード例に示します。

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

*VideoPortGetProcAddress*コールバックルーチンを通じて呼び出しが実行された後、 *Pvpfunction*が**NULL**であるか、または**VideoPortCreateSecondaryDisplay**関数のアドレスを含んでいます。 *Pvpfunction*が**NULL**の場合、ビデオポートドライバーは、検索しようとしている関数をエクスポートしません。また、ミニポートドライバーは、この関数を使用しないようにする必要があります。 *Pvpfunction*が**NULL**でない場合は、前の例に示すように、このポインターを使用して**VideoPortCreateSecondaryDisplay**を呼び出すことができます。

 

 





