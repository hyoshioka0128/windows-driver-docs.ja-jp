---
title: ハイブリッドシステム DDI
description: Windows 8.1 以降では、これらのユーザーモードおよびカーネルモードの構造とディスプレイデバイスドライバーインターフェイス (DDI) の列挙が更新され、ハイブリッドシステム D3D10_DDI_RESOURCE_MISC_FLAGD3DDDI_RESOURCEFLAGS2D3DDDI_ 上のクロスアダプターリソースを処理できるようになりました。Windows 8.1 の新機能である SYNCHRONIZATIONOBJECT_FLAGSD3DKMDT_GDISURFACEDATAD3DKMDT_GDISURFACETYPEDXGK_DRIVERCAPSDXGK_VIDMMCAPSThis 関数は、ユーザーモード display driver QueryDListForApplication1 によって実装されています。
ms.assetid: 8AABE677-2C2D-4CFD-AF22-06D65524A158
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 700d4731bb251afd5db4a3600fe94fd94432060b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838894"
---
# <a name="hybrid-system-ddi"></a>ハイブリッドシステム DDI


Windows 8.1 以降では、ディスプレイデバイスドライバーインターフェイス (DDI) のこれらのユーザーモードとカーネルモードの構造と列挙が更新され、[ハイブリッドシステム](using-cross-adapter-resources-in-a-hybrid-system.md)上の[アダプター間のリソース](using-cross-adapter-resources-in-a-hybrid-system.md)が処理されます。

-   [**D3D10\_DDI\_リソース\_その他の\_フラグ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d10_ddi_resource_misc_flag)
-   [**D3DDDI\_RESOURCEFLAGS2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddi_resourceflags2)
-   [**D3DDDI\_同期オブジェクト\_フラグ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddi_synchronizationobject_flags)
-   [**D3DKMDT\_GDISURFACEDATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_gdisurfacedata)
-   [**D3DKMDT\_GDISURFACETYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_d3dkmdt_gdisurfacetype)
-   [**DXGK\_DRIVERCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_drivercaps)
-   [**DXGK\_VIDMMCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_vidmmcaps)

Windows 8.1 の新しい関数は、ユーザーモードの表示ドライバーによって実装されています。

-   [*QueryDListForApplication1*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_querydlistforapplication1)

この関数をエクスポートする DLL を設定および登録する方法を次に示します。
## <a name="span-idsetting_up_the_dlist_dllspanspan-idsetting_up_the_dlist_dllspanspan-idsetting_up_the_dlist_dllspansetting-up-the-dlist-dll"></a><span id="Setting_up_the_dList_DLL"></span><span id="setting_up_the_dlist_dll"></span><span id="SETTING_UP_THE_DLIST_DLL"></span>DList DLL の設定


*Dlist*は、独立した GPU で高パフォーマンスのレンダリングを行うために、クロスアダプター共有サーフェスを必要とするアプリケーションの一覧です。 個別の GPU によって、 [**QueryDListForApplication1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_querydlistforapplication1)関数をエクスポートする小さな**dlist** DLL が個別にインストールされます。 オペレーティングシステム自体は、アプリケーションを実行する GPU を決定しません。 代わりに、Direct3D の初期化中に、Microsoft Direct3D ランタイムによって**QueryDListForApplication1**が最大で1回呼び出されます。

ドライバーは、プロセスが統合 GPU ではなく個別の GPU のパフォーマンスを向上させる必要があるかどうかを判断するために、最新のプロセス情報の一覧を照会する必要があります。

最適なパフォーマンスを得るには、DLL のサイズが 200 KB 未満である必要があります。また、割り当てを最小限に抑える必要があり、4ミリ秒未満で[**QueryDListForApplication1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_querydlistforapplication1)関数から戻ることができる必要があります。

## <a name="span-idregistering_the_dlist_dllspanspan-idregistering_the_dlist_dllspanspan-idregistering_the_dlist_dllspanregistering-the-dlist-dll"></a><span id="Registering_the_dList_DLL"></span><span id="registering_the_dlist_dll"></span><span id="REGISTERING_THE_DLIST_DLL"></span>DList DLL を登録しています


ユーザーモードの表示ドライバーでは、レジストリキー **UserModeDListDriverName**と**UserModeDListDriverNameWow**の下にある INF ファイルに小さな**dlist** DLL の名前が指定され、その後、 **Wow64**レジストリエントリに含まれます。 次に、INF コード例を示します。

```inf
[Xxx_SoftwareDeviceSettings]
...
HKR,, UserModeDListDriverName,    %REG_MULTI_SZ%, dlistumd.dll
HKR,, UserModeDListDriverNameWow, %REG_MULTI_SZ%, dlistumdwow.dll
```
