---
title: ユーザー モードのハンドルを取得します。
description: ユーザー モードのハンドルを取得します。
ms.assetid: b241bf00-1adb-4ab0-a00e-e922bdc9eee5
keywords:
- カーネル モードのビデオ トランスポート WDK DirectDraw を描画するには、ユーザー モードの処理します。
- DirectDraw カーネル モードのビデオ トランスポート WDK Windows 2000 の表示、ユーザー モードの処理します。
- カーネル モードのビデオ トランスポート WDK DirectDraw、ユーザー モードの処理します。
- ビデオ トランスポートのカーネル モードの WDK DirectDraw、ユーザー モード処理
- ユーザー モード WDK DirectDraw を処理します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 018d2000150c8305a3673b483a7d120e25455ad3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548684"
---
# <a name="getting-the-user-mode-handles"></a>ユーザー モードのハンドルを取得します。


## <span id="ddk_getting_the_user_mode_handles_gg"></span><span id="DDK_GETTING_THE_USER_MODE_HANDLES_GG"></span>


次の手順では、ユーザー モード (リング 3) のハンドルを取得する方法を示します。

DirectDraw オブジェクトの DirectDraw ハンドルを取得します。

1. 呼び出す**QueryInterface (**<em>lpDD</em>、(& a)*IID\_IDirectDrawKernel*、(& a)<em>pNewInterface</em>**)** DirectDraw インターフェイス。

2. 呼び出す、 [ **IDirectDrawKernel::GetKernelHandle** ](https://msdn.microsoft.com/library/windows/hardware/ff567404)新しいインターフェイスのメソッド。

**IDirectDrawKernel::GetKernelHandle** DirectDraw オブジェクトのカーネル モードのハンドルを返します。 ハンドルを解放するを使用して、 [ **IDirectDrawKernel::ReleaseKernelHandle** ](https://msdn.microsoft.com/library/windows/hardware/ff567407)メソッド。

ユーザー モード コンポーネントを呼び出すことも、 [ **IDirectDrawKernel::GetCaps** ](https://msdn.microsoft.com/library/windows/hardware/ff567401) DirectDraw オブジェクトのカーネル モードの機能を取得します。

### <a name="span-idcodesamplespanspan-idcodesamplespancode-sample"></a><span id="code_sample"></span><span id="CODE_SAMPLE"></span>コード サンプル

```cpp
ddRVal = IDirectDraw_QueryInterface( lpDD, &IID_IDirectDrawKernel, &pDDK );
if( ( ddRVal == DD_OK ) && ( pDDK != NULL ) )
{
    dwDirectDrawHandle = 0;
    IDirectDrawKernel_GetKernelHandle( pDDK, dwDirectDrawHandle );
    if( dwDirectDrawHandle == 0 )
    {
        // error
    }
}
```

DirectDrawSurface ハンドルを取得します。

1. 呼び出す**QueryInterface (**<em>lpSurface</em>、(& a)*IID\_IDirectDrawSurfaceKernel*、(& a)<em>pDDSK</em> **)** DirectDrawSurface インターフェイス。

2. 呼び出す、 [ **IDirectDrawSurfaceKernel::GetKernelHandle** ](https://msdn.microsoft.com/library/windows/hardware/ff567411)新しいインターフェイスのメソッド。

**IDirectDrawSurfaceKernel::GetKernelHandle** DirectDrawSurface ドライバーのカーネル モードのハンドルを返します。 ハンドルを解放するを使用して、 [ **IDirectDrawSurfaceKernel::ReleaseKernelHandle** ](https://msdn.microsoft.com/library/windows/hardware/ff567413)メソッド。

### <a name="span-idcodesample2spanspan-idcodesample2spancode-sample"></a><span id="code_sample2"></span><span id="CODE_SAMPLE2"></span>コード サンプル

```cpp
ddRVal = IDirectDraw_QueryInterface( lpSurface,
             &IID_IDirectDrawSurfaceKernel, &pDDSK );
if( ( ddRVal == DD_OK ) && ( pDDK != NULL ) )
{
    dwSurfaceHandle = 0;
    IDirectDrawSurfaceKernel_GetKernelHandle( pDDSK, dwSurfaceHandle );
    if( dwSurfaceHandle == 0 )
    {
        // error
    }
}
```

 

 





