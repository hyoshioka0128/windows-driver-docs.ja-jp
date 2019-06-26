---
title: ハイブリッド システム DDI
description: Windows 8.1 以降、これらのユーザー モードとカーネル モードの構造および表示デバイス ドライバー インターフェイス (DDI) の列挙体は更新ハイブリッド システム D3D10_DDI_RESOURCE_MISC_FLAGD3DDDI_RESOURCEFLAGS2D3DDDI_ でクロス アダプターのリソースを処理するにはWindows 8.1 では、新機能、SYNCHRONIZATIONOBJECT_FLAGSD3DKMDT_GDISURFACEDATAD3DKMDT_GDISURFACETYPEDXGK_DRIVERCAPSDXGK_VIDMMCAPSThis 関数がユーザー モードのディスプレイ ドライバー QueryDListForApplication1 によって実装されます。
ms.assetid: 8AABE677-2C2D-4CFD-AF22-06D65524A158
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ab47c69133bed7a19a67c88923f34fe3d7207e1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380200"
---
# <a name="hybrid-system-ddi"></a>ハイブリッド システム DDI


Windows 8.1 以降、これらのユーザー モードとカーネル モードの構造および表示デバイス ドライバー インターフェイス (DDI) の列挙体は更新を処理する[クロス アダプター リソース](using-cross-adapter-resources-in-a-hybrid-system.md)上、[ハイブリッド システム](using-cross-adapter-resources-in-a-hybrid-system.md):

-   [**D3D10\_DDI\_RESOURCE\_MISC\_FLAG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ne-d3d10umddi-d3d10_ddi_resource_misc_flag)
-   [**D3DDDI\_RESOURCEFLAGS2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dukmdt/ns-d3dukmdt-_d3dddi_resourceflags2)
-   [**D3DDDI\_SYNCHRONIZATIONOBJECT\_フラグ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dukmdt/ns-d3dukmdt-_d3dddi_synchronizationobject_flags)
-   [**D3DKMDT\_GDISURFACEDATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ns-d3dkmdt-_d3dkmdt_gdisurfacedata)
-   [**D3DKMDT\_GDISURFACETYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ne-d3dkmdt-_d3dkmdt_gdisurfacetype)
-   [**DXGK\_DRIVERCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_drivercaps)
-   [**DXGK\_VIDMMCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_vidmmcaps)

Windows 8.1 では、新機能は、この関数は、ユーザー モードのディスプレイ ドライバーによって実装されます。

-   [*QueryDListForApplication1*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_querydlistforapplication1)

設定して、この関数をエクスポートする DLL を登録する方法を次に示します。
## <a name="span-idsettingupthedlistdllspanspan-idsettingupthedlistdllspanspan-idsettingupthedlistdllspansetting-up-the-dlist-dll"></a><span id="Setting_up_the_dList_DLL"></span><span id="setting_up_the_dlist_dll"></span><span id="SETTING_UP_THE_DLIST_DLL"></span>DList DLL のセットアップ


A *dList*不連続の GPU で高パフォーマンスなレンダリングのクロス アダプター共有サーフェスを必要とするアプリケーションの一覧を示します。 独立した GPU インストール独立した小さな**dList**をエクスポートする DLL、 [ **QueryDListForApplication1** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_querydlistforapplication1)関数。 オペレーティング システム自体では、GPU でアプリケーションを実行する必要がありますを決定します。 マイクロソフトの Direct3D ランタイムが呼び出す代わりに、 **QueryDListForApplication1** Direct3D の初期化中に最大で 1 回です。

ドライバーは、プロセスが統合された GPU ではなく独立した GPU のパフォーマンスの強化が必要かどうかを判断するプロセスについての最新の一覧を照会する必要があります。

最適なパフォーマンスを DLL のサイズは 200 KB 未満にする必要があります、割り当てを最小限にならないように、およびから返すことができるよう、 [ **QueryDListForApplication1** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_querydlistforapplication1) 4 ミリ秒未満の関数。

## <a name="span-idregisteringthedlistdllspanspan-idregisteringthedlistdllspanspan-idregisteringthedlistdllspanregistering-the-dlist-dll"></a><span id="Registering_the_dList_DLL"></span><span id="registering_the_dlist_dll"></span><span id="REGISTERING_THE_DLIST_DLL"></span>DList DLL を登録します。


ユーザー モードのディスプレイ ドライバーは、わずかな名前を提供します**dList** INF ファイル、レジストリ キーの下で DLL **UserModeDListDriverName**と**UserModeDListDriverNameWow、** 。後者の下で、 **Wow64**レジストリ エントリ。 INF の例のコードを次に示します。

```inf
[Xxx_SoftwareDeviceSettings]
...
HKR,, UserModeDListDriverName,    %REG_MULTI_SZ%, dlistumd.dll
HKR,, UserModeDListDriverNameWow, %REG_MULTI_SZ%, dlistumdwow.dll
```
