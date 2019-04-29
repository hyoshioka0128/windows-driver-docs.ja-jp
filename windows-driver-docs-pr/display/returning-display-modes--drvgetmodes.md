---
title: 表示モード DrvGetModes を返す
description: 表示モード DrvGetModes を返す
ms.assetid: 1010235a-0609-4380-8b83-7d8c649c2404
keywords:
- ディスプレイ ドライバー WDK Windows 2000 では、デスクトップ管理
- デスクトップ管理 WDK Windows 2000 の表示
- 表示モードの Windows 2000 の WDK の表示を返す
- DrvGetModes
- Windows 2000 の WDK のモードを表示します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 20ffe555a994a8b2dd479190f5475db89751da78
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63389984"
---
# <a name="returning-display-modes-drvgetmodes"></a>表示モードを返す: DrvGetModes


## <span id="ddk_returning_display_modes_drvgetmodes_gg"></span><span id="DDK_RETURNING_DISPLAY_MODES_DRVGETMODES_GG"></span>


ディスプレイ ドライバーがサポートする必要がありますも[ **DrvGetModes**](https://msdn.microsoft.com/library/windows/hardware/ff556233)します。 この関数により、GDI のポインターの配列に[ **DEVMODEW** ](https://msdn.microsoft.com/library/windows/hardware/ff552837)構造体。 構造体 (ピクセル単位、およびそのミリメートル) 内のディメンション、面の数、平面や色については、あたりのビット数など、サポートされるさまざまなモードの表示の属性を定義します。

ドライバーがメモリに使用できる表示モードを書き込みます順序と、 [ **DrvGetModes** ](https://msdn.microsoft.com/library/windows/hardware/ff556233)関数が呼び出される Windows が選択した最終的な表示モードの影響を与えることができます。 一般に、このアプリケーションでは、既定のモードを指定しない場合、システムは、ドライバーによって提供される一覧で最初の一致のモードを選択します。

たとえば、現在の表示モードがあります。

800x600x32bpp@60Hz DMDO\_既定 DMDFO\_センター

ドライバーが使用可能な表示モードの一覧を次のように指定します。

**します。** 600x800x32bpp@60Hz DMDO\_270 DMDFO\_STRETCH

**B とします。** 600x800x32bpp@60Hz DMDO\_90 DMDFO\_STRETCH

**C.** 600x800x32bpp@60Hz DMDO\_90 DMDFO\_センター

**D。** 600x800x32bpp@60Hz DMDO\_270 DMDFO\_センター

**ケース 1**

アプリケーションが、モニターを設定しようとしています場合600x800x32bpp@60Hz、が、DM\_DISPLAYORIENTATION および DM\_で DISPLAYFIXEDOUTPUT フラグが設定されていない、 **dmFields**のメンバー [ **。DEVMODEW**](https://msdn.microsoft.com/library/windows/hardware/ff552837)システムの向きを選択する必要があり、出力モードを修正しました。 この場合、システムが表示モードを選択 C 現在 DMDFO に一致する最初の表示モードである\_CENTER の設定。

**ケース 2**

アプリケーションが、モニターを設定しようとしています場合600x800x32bpp@60HzDMDFO\_STRETCH、システムの表示モードの A. は選択。

**ケース 3**

アプリケーションが、モニターを設定しようとしています場合600x800x32bpp@60HzDMDO\_270、システムは D. の表示モードを選択。

**ケース 4**

アプリケーションが、モニターを設定しようとしています。 場合600x800x32bpp@60HzDMDO\_既定では、許容と一致するものを、システムが失敗します。

これらの規則に 1 つの例外が適用されます。 システム シークの画面の向きに一致すると、方向が指定されていないと、現在のモードが一致することはできません、システムは、DMDO\_他の画面の向きを既定の優先順位。

たとえば、現在の表示モードがあります。

600x800x32bpp@60Hz DMDO\_90 DMDFO\_STRETCH

ドライバーが使用可能な表示モードの一覧を次のように指定します。

**します。** 800x600x32bpp@60Hz DMDO\_180 DMDFO\_センター

**B とします。** 800x600x32bpp@60Hz DMDO\_180 DMDFO\_STRETCH

**C.** 800x600x32bpp@60Hz DMDO\_既定 DMDFO\_センター

**D。** 800x600x32bpp@60Hz DMDO\_既定 DMDFO\_STRETCH

この場合、アプリケーションが、モニターを設定しようとしています800x600x32bpp@60Hz、D. の表示モードは、システムによって選択されます。

 

 





