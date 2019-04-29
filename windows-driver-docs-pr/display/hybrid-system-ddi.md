---
title: ハイブリッド システム DDI
description: Windows 8.1 以降、これらのユーザー モードとカーネル モードの構造および表示デバイス ドライバー インターフェイス (DDI) の列挙体は更新ハイブリッド システム D3D10_DDI_RESOURCE_MISC_FLAGD3DDDI_RESOURCEFLAGS2D3DDDI_ でクロス アダプターのリソースを処理するにはWindows 8.1 では、新機能、SYNCHRONIZATIONOBJECT_FLAGSD3DKMDT_GDISURFACEDATAD3DKMDT_GDISURFACETYPEDXGK_DRIVERCAPSDXGK_VIDMMCAPSThis 関数がユーザー モードのディスプレイ ドライバー QueryDListForApplication1 によって実装されます。
ms.assetid: 8AABE677-2C2D-4CFD-AF22-06D65524A158
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a56451bb377831d6b41f45f35f029426f5a57961
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383724"
---
# <a name="hybrid-system-ddi"></a>ハイブリッド システム DDI


Windows 8.1 以降、これらのユーザー モードとカーネル モードの構造および表示デバイス ドライバー インターフェイス (DDI) の列挙体は更新を処理する[クロス アダプター リソース](using-cross-adapter-resources-in-a-hybrid-system.md)上、[ハイブリッド システム](using-cross-adapter-resources-in-a-hybrid-system.md):

-   [**D3D10\_DDI\_RESOURCE\_MISC\_FLAG**](https://msdn.microsoft.com/library/windows/hardware/ff542004)
-   [**D3DDDI\_RESOURCEFLAGS2**](https://msdn.microsoft.com/library/windows/hardware/hh439286)
-   [**D3DDDI\_SYNCHRONIZATIONOBJECT\_フラグ**](https://msdn.microsoft.com/library/windows/hardware/ff544662)
-   [**D3DKMDT\_GDISURFACEDATA**](https://msdn.microsoft.com/library/windows/hardware/ff546021)
-   [**D3DKMDT\_GDISURFACETYPE**](https://msdn.microsoft.com/library/windows/hardware/ff546039)
-   [**DXGK\_DRIVERCAPS**](https://msdn.microsoft.com/library/windows/hardware/ff561062)
-   [**DXGK\_VIDMMCAPS**](https://msdn.microsoft.com/library/windows/hardware/ff562072)

Windows 8.1 では、新機能は、この関数は、ユーザー モードのディスプレイ ドライバーによって実装されます。

-   [*QueryDListForApplication1*](https://msdn.microsoft.com/library/windows/hardware/dn270597)

設定して、この関数をエクスポートする DLL を登録する方法を次に示します。
## <a name="span-idsettingupthedlistdllspanspan-idsettingupthedlistdllspanspan-idsettingupthedlistdllspansetting-up-the-dlist-dll"></a><span id="Setting_up_the_dList_DLL"></span><span id="setting_up_the_dlist_dll"></span><span id="SETTING_UP_THE_DLIST_DLL"></span>DList DLL のセットアップ


A *dList*不連続の GPU で高パフォーマンスなレンダリングのクロス アダプター共有サーフェスを必要とするアプリケーションの一覧を示します。 独立した GPU インストール独立した小さな**dList**をエクスポートする DLL、 [ **QueryDListForApplication1** ](https://msdn.microsoft.com/library/windows/hardware/dn270597)関数。 オペレーティング システム自体では、GPU でアプリケーションを実行する必要がありますを決定します。 マイクロソフトの Direct3D ランタイムが呼び出す代わりに、 **QueryDListForApplication1** Direct3D の初期化中に最大で 1 回です。

ドライバーは、プロセスが統合された GPU ではなく独立した GPU のパフォーマンスの強化が必要かどうかを判断するプロセスについての最新の一覧を照会する必要があります。

最適なパフォーマンスを DLL のサイズは 200 KB 未満にする必要があります、割り当てを最小限にならないように、およびから返すことができるよう、 [ **QueryDListForApplication1** ](https://msdn.microsoft.com/library/windows/hardware/dn270597) 4 ミリ秒未満の関数。

## <a name="span-idregisteringthedlistdllspanspan-idregisteringthedlistdllspanspan-idregisteringthedlistdllspanregistering-the-dlist-dll"></a><span id="Registering_the_dList_DLL"></span><span id="registering_the_dlist_dll"></span><span id="REGISTERING_THE_DLIST_DLL"></span>DList DLL を登録します。


ユーザー モードのディスプレイ ドライバーは、わずかな名前を提供します**dList** INF ファイル、レジストリ キーの下で DLL **UserModeDListDriverName**と**UserModeDListDriverNameWow、**。後者の下で、 **Wow64**レジストリ エントリ。 INF の例のコードを次に示します。

```inf
[Xxx_SoftwareDeviceSettings]
...
HKR,, UserModeDListDriverName,    %REG_MULTI_SZ%, dlistumd.dll
HKR,, UserModeDListDriverNameWow, %REG_MULTI_SZ%, dlistumdwow.dll
```
