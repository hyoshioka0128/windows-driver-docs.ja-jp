---
title: DXGI DDI をサポートしています。
description: DXGI DDI をサポートしています。
ms.assetid: 3a49d7cb-984f-4e4f-a549-5c0442e1c45a
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9accff4e1d95f836bd937c0328216a471da998ef
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559803"
---
# <a name="supporting-the-dxgi-ddi"></a>DXGI DDI をサポートしています。


Microsoft DirectX Graphics Infrastructure (DXGI) のデバイス ドライバー インターフェイス (DDI) をサポートするために、ユーザー モードのディスプレイ ドライバーが Dxgiddi.h ヘッダー ファイルを含める必要があります。 Dxgiddi.h は、アプリケーション レベルと共有されている定義を含む Dxgitype.h ヘッダー ファイルも含まれています。 DXGI を構築します。 Dxgiddi.h では、いくつかのユーザー モード ディスプレイ ドライバーのエントリ ポイントと、ドライバーは、カーネル (ディスプレイのミニポート ドライバーを含む) との通信に使用できる DXGI コールバック関数を定義します。

マイクロソフトの Direct3D ランタイムで DXGI DDI へのアクセスを提供する、 [ **DXGI\_DDI\_ベース\_ARGS** ](https://msdn.microsoft.com/library/windows/hardware/ff557485)構造体、 **DXGIBaseDDI**のメンバー、 [ **D3D10DDIARG\_CREATEDEVICE** ](https://msdn.microsoft.com/library/windows/hardware/ff541664)への呼び出しで指す構造体、 [ **CreateDevice(D3D10)**](https://msdn.microsoft.com/library/windows/hardware/ff540635)関数。 ユーザー モードのディスプレイ ドライバーは、DXGI 関数へのポインターを提供します。

ドライバーは、これらの関数、構造体のメンバーを実装する、 **pDXGIDDIBaseFunctionsXxx**のメンバー **DXGI\_DDI\_ベース\_ARGS**をポイントします。 ドライバーへのポインターを記録する必要があります、 [DXGI コールバック関数のテーブル](https://msdn.microsoft.com/library/windows/hardware/ff552877)を**pDXGIBaseCallbacks**のメンバー **DXGI\_DDI\_ベース\_ARGS**後で使用するを指しています。 ドライバーは、DXGI のコールバック関数のテーブルへのポインターを記録ではなく内でスレッドがないときに、Direct3D ランタイムは、コールバック関数のアドレスを変更できるため、DXGI のコールバック関数には、個々 のポインターを記録しますユーザー モードのディスプレイ ドライバー。
さらに DXGI ユーザー モード ディスプレイ ドライバー要件では、ソフトウェア rasterizers 存在します。 このようなユーザー モードのディスプレイ ドライバー (具体的には、すべてのドライバーはグラフィックス アダプターの Direct3D のバージョン 9 DDI 実装と共有されているサポート ハードウェアはなく) 返す必要があります、 **DXGI\_状態\_ありません\_リダイレクト**S ではなく値\_[ok] の値からその[ **CreateDevice(D3D10)** ](https://msdn.microsoft.com/library/windows/hardware/ff540635)関数。 返す**DXGI\_状態\_いいえ\_リダイレクト**使用するようにしない効果的なコミュニケーションの共有リソースのプレゼンテーション パス デスクトップ ウィンドウ マネージャー (DWM) で DXGI することを示します。 共有リソースの表示パスが作成された共有リソースの関数呼び出し (つまり、 [ **CreateResource(D3D10)** ](https://msdn.microsoft.com/library/windows/hardware/ff540691)と[ **OpenResource(D3D10)**](https://msdn.microsoft.com/library/windows/hardware/ff568612)関数、 **D3D10\_DDI\_リソース\_その他\_SHARED**フラグを設定) が発生します。 ただし、DXGI は手法がバッファーは、CPU にのみ使用可能なスワップに関連する代わりに使用する必要があります。 たとえば、DXGI から移動する表示されたデータ バック バッファーをデスクトップに共有リソースのプレゼンテーション パス以外の方法でします。 この場合、DXGI 実際に呼び出す、ドライバーの[ **PresentDXGI** ](https://msdn.microsoft.com/library/windows/hardware/ff569179) DWM との通信を有効ではなく、表示されたデータを移動する関数。

## <a name="direct3d-version-10-dxgi-functions"></a>Direct3D のバージョン 10 DXGI 関数

このセクションでは、ユーザー モードは、direct3d10 Microsoft バージョンのランタイムに DLL を提供するドライバーを表示する Microsoft DirectX Graphics Infrastructure (DXGI) 関数について説明します。 ドライバーのメンバーを使用して DXGI 関数へのポインターを提供する、 [DXGI_DDI_BASE_FUNCTIONS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi_ddi_base_functions)ユーザー モードのディスプレイ ドライバーの呼び出しで構造[CreateDevice(D3D10)](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createdevice)関数。

|||
|:--|:--|
|BltDXGI|GetGammaCapsDXGI|
|PresentDXGI|QueryResourceResidencyDXGI|
|ResolveSharedResourceDXGI|RotateResourceIdentitiesDXGI|
|SetDisplayModeDXGI|SetResourcePriorityDXGI|


## <a name="direct3d-version-111-dxgi-functions"></a>Direct3D のバージョン 11.1 DXGI 関数

このセクションでは、マイクロソフトの Direct3D バージョン 11.1 ランタイムに追加されるユーザー モード ディスプレイ ドライバーによって実装される、Microsoft DirectX Graphics Infrastructure (DXGI) 関数について説明します。 Direct3D 11.1 は、Windows 8 で導入されました。 

ユーザー モードのディスプレイ ドライバー DLL のエクスポート、 [OpenAdapter10_2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_openadapter)関数し、アダプター固有の関数のメンバーへのポインターを提供、 [D3D10_2DDI_ADAPTERFUNCS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ns-d3d10umddi-d3d10_2ddi_adapterfuncs)構造体ときに、ランタイムは CreateDevice(D3D10) を呼び出します。

Direct3D のバージョン 11.1 DXGI 関数のメンバーへのポインターを提供するドライバー、 [DXGI1_2_DDI_BASE_FUNCTIONS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi1_2_ddi_base_functions)ユーザー モードのディスプレイ ドライバーへの呼び出しで構造体のアダプター固有[CreateDevice (D3D10)](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createdevice)関数。

|||
|:--|:--|
|Blt1DXGI|OfferResourcesDXGI|
|ReclaimResourcesDXGI||

## <a name="direct3d-version-112-dxgi-functions"></a>Direct3D のバージョン 11.2 DXGI 関数

このセクションでは、リファレンスのページには、マイクロソフトの Direct3D バージョン 11.2 のランタイムに追加されるユーザー モード ディスプレイ ドライバーによって実装される、Microsoft DirectX Graphics Infrastructure (DXGI) 関数について説明します。 Direct3D 11.2 は、Windows 8.1 で導入されました。 

ユーザー モードのディスプレイ ドライバー DLL が OpenAdapter10_2 関数をエクスポートし、アダプター固有の関数のメンバーへのポインターを提供、 [D3D10_2DDI_ADAPTERFUNCS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ns-d3d10umddi-d3d10_2ddi_adapterfuncs)ランタイムが呼び出す CreateDevice(D3D10) と構造体します。

ドライバーのメンバーを Direct3D のバージョン 11.2 DXGI 関数へのポインターを提供する、 [DXGI1_3_DDI_BASE_FUNCTIONS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi1_3_ddi_base_functions)ユーザー モードのディスプレイ ドライバーへの呼び出しで構造体のアダプター固有[CreateDevice (D3D10)](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createdevice)関数。

|||
|:--|:--|
|[PFNDDXGIDDI_PRESENT_MULTIPLANE_OVERLAYCB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/nc-dxgiddi-pfnddxgiddi_present_multiplane_overlaycb)|[PFNDDXGIDDI_PRESENTCB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/nc-dxgiddi-pfnddxgiddi_presentcb)|
|[PFNDDXGIDDI_SUBMITPRESENTBLTTOHWQUEUECB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/nc-dxgiddi-pfnddxgiddi_submitpresentblttohwqueuecb)|[PFNDDXGIDDI_SUBMITPRESENTTOHWQUEUECB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/nc-dxgiddi-pfnddxgiddi_submitpresenttohwqueuecb)|

> [!NOTE]
> このセクションでは、Direct3D 11.2 のランタイムでサポートされている追加の DXGI 関数が含まれている[Multiplane ユーザー モード ドライバーによって実装される関数のオーバーレイ](multiplane-overlay-support.md)します。

