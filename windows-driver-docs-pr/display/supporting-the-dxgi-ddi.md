---
title: DXGI DDI のサポート
description: DXGI DDI のサポート
ms.assetid: 3a49d7cb-984f-4e4f-a549-5c0442e1c45a
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: 0f388df9532b103f0f740b878b3e987c45932a54
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825596"
---
# <a name="supporting-the-dxgi-ddi"></a>DXGI DDI のサポート


Microsoft DirectX Graphics Infrastructure (DXGI) device driver interface (DDI) をサポートするには、ユーザーモードの表示ドライバーに Dxgiddi ヘッダーファイルを含める必要があります。 Dxgiddi には、Dxgitype ヘッダーファイルも含まれています。このファイルには、アプリケーションレベルの DXGI コンストラクトと共有される定義が含まれています。 Dxgiddi は、いくつかのユーザーモード表示ドライバーのエントリポイントと、ドライバーがカーネルとの通信に使用できる DXGI コールバック関数 (ディスプレイミニポートドライバーを含む) を定義します。

Microsoft Direct3D ランタイムは、 [**D3D10DDIARG\_CREATEDEVICE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_createdevice)構造体の**dxgibaseddi**メンバーが指すの[ **\_ARGS 構造\_\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_base_args)内の dxgi DDI へのアクセスを提供します。[**CreateDevice (D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createdevice)関数。 ユーザーモード表示ドライバーは、DXGI 関数へのポインターを提供します。

ドライバーは、 **DXGI\_DDI のメンバー\_BASE\_ARGS** **が指す**構造体のメンバーを通じて、これらの関数を実装します。 ドライバーは、dxgi[コールバック関数テーブル](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)へのポインターを記録する必要があります。これは、 **\_ARGS\_\_** の**Pdxgibasecallbacks**メンバーが、後で使用するためにを指します。 ドライバーは、DXGI コールバック関数への個々のポインターを記録するのではなく、DXGI コールバック関数テーブルへのポインターを記録する必要があります。これは、Direct3D ランタイムは、の内部にスレッドが存在しない場合は常にコールバック関数のアドレスを変更できるためです。ユーザーモードの表示ドライバー。
ソフトウェア rasterizers には、さらに DXGI のユーザーモード表示ドライバー要件が存在します。 このようなユーザーモード表示ドライバー (具体的には、グラフィックスアダプター上の Direct3D バージョン 9 DDI 実装と共有されているハードウェアをサポートしていないドライバー) は、 **\_リダイレクトなし\_DXGI\_ステータス**を返す必要があります。[**CreateDevice (D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createdevice)関数の\_OK 値ではなく、値。 **Dxgi\_状態\_** 返されます。\_のリダイレクトは、共有リソースプレゼンテーションパスを使用してデスクトップウィンドウマネージャー (DWM) との通信を有効にする必要がないことを DXGI に示します。 共有リソースプレゼンテーションパスは、共有リソース関数 (つまり、 [**Createresource (D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createresource)および[**OPENRESOURCE (D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_openresource)関数を**D3D10\_DDI\_リソース\_で呼び出すときに作成され\_共有**フラグセット) が発生します。 ただし、バッファーが CPU だけで使用可能なスワップチェーンに関連する手法を使用する必要があります。 たとえば、DXGI は、共有リソースのプレゼンテーションパス以外の方法で、レンダリングされたデータをバックバッファーからデスクトップに移動する必要があります。 このような状況では、DXGI は実際には、DWM との通信ではなく、レンダリングされたデータを移動するために[**ドライバーの存在**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_base_functions)を呼び出します。

## <a name="direct3d-version-10-dxgi-functions"></a>Direct3D Version 10 DXGI 関数

ここでは、ユーザーモードで表示されるドライバー DLL が Microsoft Direct3D バージョン10ランタイムに提供する Microsoft DirectX グラフィックスインフラストラクチャ (DXGI) 関数について説明します。 ドライバーは、ユーザーモードの display driver の[CreateDevice (D3D10)](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createdevice)関数の呼び出しで、 [DXGI_DDI_BASE_FUNCTIONS](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_base_functions)構造体のメンバーを介して、DXGI 関数へのポインターを提供します。

|||
|:--|:--|
|BltDXGI|GetGammaCapsDXGI|
|% Dxgi|QueryResourceResidencyDXGI|
|ResolveSharedResourceDXGI|RotateResourceIdentitiesDXGI|
|SetDisplayModeDXGI|Setresourceの優先順位 Dxgi|


## <a name="direct3d-version-111-dxgi-functions"></a>Direct3D バージョン 11.1 DXGI 関数

このセクションでは、microsoft Direct3D バージョン11.1 ランタイム用に追加される、ユーザーモード表示ドライバーによって実装される Microsoft DirectX グラフィックスインフラストラクチャ (DXGI) の機能について説明します。 Direct3D 11.1 は Windows 8 で導入されました。 

ユーザーモードの display driver DLL は、 [OpenAdapter10_2](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_openadapter)関数をエクスポートし、ランタイムが CREATEDEVICE (D3D10) を呼び出すときに、 [D3D10_2DDI_ADAPTERFUNCS](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10_2ddi_adapterfuncs)構造体のメンバーを介してアダプター固有の関数へのポインターを提供します。

このドライバーは、ユーザーモードの表示ドライバーのアダプター固有の[CreateDevice (D3D10)](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createdevice)関数の呼び出しで、 [DXGI1_2_DDI_BASE_FUNCTIONS](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi1_2_ddi_base_functions)構造体のメンバーを介して、Direct3D バージョン 11.1 DXGI 関数へのポインターを提供します。

|||
|:--|:--|
|Blt1DXGI|OfferResourcesDXGI|
|ReclaimResourcesDXGI||

## <a name="direct3d-version-112-dxgi-functions"></a>Direct3D バージョン 11.2 DXGI 関数

このセクションのリファレンスページでは、microsoft Direct3D バージョン11.2 ランタイム用に追加された、ユーザーモード表示ドライバーによって実装される Microsoft DirectX グラフィックスインフラストラクチャ (DXGI) 関数について説明します。 Direct3D 11.2 は Windows 8.1 で導入されました。 

ユーザーモードの display driver DLL は、OpenAdapter10_2 関数をエクスポートし、ランタイムが CreateDevice (D3D10) を呼び出すときに、 [D3D10_2DDI_ADAPTERFUNCS](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10_2ddi_adapterfuncs)構造体のメンバーを介してアダプター固有の関数へのポインターを提供します。

このドライバーは、ユーザーモードの表示ドライバーのアダプター固有の[CreateDevice (D3D10)](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createdevice)関数の呼び出しで、 [DXGI1_3_DDI_BASE_FUNCTIONS](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi1_3_ddi_base_functions)構造体のメンバーを介して、Direct3D バージョン 11.2 DXGI 関数へのポインターを提供します。

|||
|:--|:--|
|[PFNDDXGIDDI_PRESENT_MULTIPLANE_OVERLAYCB](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/nc-dxgiddi-pfnddxgiddi_present_multiplane_overlaycb)|[PFNDDXGIDDI_PRESENTCB](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/nc-dxgiddi-pfnddxgiddi_presentcb)|
|[PFNDDXGIDDI_SUBMITPRESENTBLTTOHWQUEUECB](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/nc-dxgiddi-pfnddxgiddi_submitpresentblttohwqueuecb)|[PFNDDXGIDDI_SUBMITPRESENTTOHWQUEUECB](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/nc-dxgiddi-pfnddxgiddi_submitpresenttohwqueuecb)|

> [!NOTE]
> Direct3D 11.2 ランタイムによってサポートされるその他の DXGI 関数は、[ユーザーモードドライバーによって実装される Multiplane オーバーレイ関数](multiplane-overlay-support.md)のセクションに含まれています。

