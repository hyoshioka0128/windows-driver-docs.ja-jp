---
title: グラフィックス ドライバー関数内の浮動小数点演算
description: グラフィックス ドライバー関数内の浮動小数点演算
ms.assetid: 5f85dc0b-27c1-4fee-9a0a-cb52d5f2dae7
keywords:
- GDI WDK Windows 2000 の表示、浮動小数点演算
- グラフィックス ドライバー WDK Windows 2000 の表示、浮動小数点演算
- WDK GDI、浮動小数点演算の描画
- 浮動小数点演算 WDK GDI
- FPU WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 46ea99e3f760b67aeef21a21517d4eb3ca8779b7
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57348971"
---
# <a name="floating-point-operations-in-graphics-driver-functions"></a>グラフィックス ドライバー関数内の浮動小数点演算


## <span id="ddk_floating_point_operations_in_graphics_driver_functions_gg"></span><span id="DDK_FLOATING_POINT_OPERATIONS_IN_GRAPHICS_DRIVER_FUNCTIONS_GG"></span>


呼び出しでそのコードを前する必要があります、グラフィックス ドライバー関数は浮動小数点ユニット (FPU) を使用するコードが含まれる場合[ **EngSaveFloatingPointState** ](https://msdn.microsoft.com/library/windows/hardware/ff565010)への呼び出し後に[ **EngRestoreFloatingPointState**](https://msdn.microsoft.com/library/windows/hardware/ff565006)します。 グラフィック ドライバー機能の一覧は、[グラフィックス ドライバー関数](graphics-driver-functions.md)を参照してください。

FPU を使用できる場合は、浮動小数点変数に値を割り当てるか、浮動小数点数に関連する計算を実行するコードで使用されます。 たとえば、次のコード行の各 FPU を使用します。

```cpp
double myDouble = 5;
int myInt = 5 * 4.3;
int myInt = 50 * cos(2);
```

作成すると、 [ **DrvAlphaBlend** ](https://msdn.microsoft.com/library/windows/hardware/ff556176) FPU を使用する関数。 次の例では、浮動小数点状態を復元および保存を行う方法を示します。

```cpp
#define DRIVER_TAG // Put your driver tag here, for example 'zyxD'

BOOL DrvAlphaBlend(...)
{
   ...
   ULONG result;
 double floatVal;
   VOID* pBuf;
   ULONG bufSize;

 // Determine the size of the required buffer.
   bufSize = EngSaveFloatingPointState(NULL, 0);

 if(bufSize > 0)
   {
 // Allocate a zeroed buffer in the nonpaged pool.
      pBuf = EngAllocMem(
         FL_NONPAGED_MEMORY|FL_ZERO_MEMORY, bufSize, DRIVER_TAG);

 if(pBuf != NULL)
      {
 // The buffer was allocated successfully.
 // Save the floating-point state.
         result = EngSaveFloatingPointState(pBuf, bufSize);

 if(TRUE == result)
         {
 // The floating-point state was saved successfully.
 // Use the FPU.
            floatVal = 0.8;
            ...
            EngRestoreFloatingPointState(pBuffer);
         }

         EngFreeMem(pBuf);
      }
   }
   ...
}
```

GDI はドライバーへの呼び出しの浮動小数点状態を自動的に保存します。 [ **DrvEscape** ](https://msdn.microsoft.com/library/windows/hardware/ff556217)関数エスケープが OPENGL\_CMD、OPENGL\_GETINFO、または MCDFUNCS します。 FPU を使用するような場合、 *DrvEscape*呼び出さず関数**EngSaveFloatingPointState**と**EngRestoreFloatingPointState**します。

浮動小数点演算を実行するほとんどの DirectDraw、Direct3D のコールバック関数は、保存し、浮動小数点状態を復元する必要がありますもします。 詳細については、[DirectDraw で浮動小数点演算の実行](performing-floating-point-operations-in-directdraw.md)と[Direct3D の浮動小数点演算の実行](performing-floating-point-operations-in-direct3d.md)を参照してください。

GDI によって提供される浮動小数点のサービスについては、[GDI 浮動小数点サービス](gdi-floating-point-services.md)を参照してください。

 

 





