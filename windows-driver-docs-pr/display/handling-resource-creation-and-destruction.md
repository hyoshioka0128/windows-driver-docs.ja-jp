---
title: リソースの作成および破棄の処理
description: リソースの作成および破棄の処理
ms.assetid: d443bdc3-1c5a-4372-9e6a-b8a4d21499b9
keywords:
- リソース作成の WDK 表示
- リソース破棄の WDK 表示
- リソースの破棄 WDK 表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cd8df9e3466305c02a0a9a94055b3299f3983eb7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838901"
---
# <a name="handling-resource-creation-and-destruction"></a>リソースの作成および破棄の処理


Microsoft DirectX graphics カーネルサブシステムがリソースの有効期間を適切に追跡し、オペレーティングシステムのメモリリークを回避できるようにするには、ユーザーモードの表示ドライバーがリソースを適切に作成および破棄する必要があります。

Microsoft Direct3D ランタイムは、ユーザーモードのリソースを作成するために、次のユーザーモードの display driver 関数を呼び出します。

-   [**Createresource**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource)新しい共有リソースまたは共有されていないリソースを作成します。

-   [**Openresource**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_openresource)は、既存の共有リソースのビューを開きます。

どちらの呼び出しでも、Direct3D ランタイムは、ユーザーモードの表示ドライバーがランタイムにコールバックするために使用する一意の*ユーザーモードランタイムリソースハンドル*を渡します。 *Createresource*または*openresource*が正常に返された場合、ユーザーモード表示ドライバーは、リソースを表す一意のユーザーモードハンドルを返します。 このハンドルは、*ユーザーモードドライバーリソースハンドル*です。 ランタイムは、後続のドライバー呼び出しでユーザーモードドライバーリソースハンドルを使用します。

1対1の対応は、ユーザーモードのランタイムリソースハンドルとユーザーモードドライバーリソースハンドルの間に存在します。 Direct3D ランタイムとユーザーモードのディスプレイドライバーは、 [**D3DDDIARG\_CREATERESOURCE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddiarg_createresource)と[**D3DDDIARG\_Openresource**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_openresource)の**hresource**メンバーを介して、ユーザーモードのランタイムとドライバーのリソースハンドルを交換します。構成.

ユーザーモード表示ドライバーが Direct3D ランタイムの[**Pfnallocatecb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_allocatecb)関数を呼び出してユーザーモードリソースの割り当てを作成する場合、ドライバーは、D3DDDICB の**hresource**メンバーにあるユーザーモードのランタイムリソースハンドルを指定する必要があります。このリソースハンドルは、 *pData*パラメーターが指す構造体[ **\_割り当て**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddicb_allocate)ます。 Direct3D ランタイムは、リソースへの一意のカーネルモードハンドルを生成し、\_D3DDDICB の**Hkmresource**メンバー内のユーザーモードの表示ドライバーに渡します。 ユーザーモードの表示ドライバーは、後で使用するディスプレイミニポートドライバーをコマンドストリームに挿入できます。

**メモ**   ユーザーモードのリソースハンドルは、ユーザーモードのリソースの作成ごとに常に一意ですが、カーネルモードのリソースハンドルは必ずしも一意ではありません。 Direct3D ランタイムがユーザーモードの表示ドライバーの[**openresource**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_openresource)関数を呼び出して、既存の共有リソースへのビューを開くと、ランタイムは D3DDDIARG の**hkmresource**メンバー内にあるリソースのカーネルモードハンドルを渡し[ **\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_openresource) *Presource*パラメーターが指す openresource 構造体。 ランタイムは、ランタイムがユーザーモードの display ドライバーの[**Createresource**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource)関数を呼び出した後に、このカーネルモードハンドルを以前に作成しました。

 

*Createresource*または*openresource*で作成されたユーザーモードリソースを破棄するために、Direct3D ランタイムは、ユーザーモードの表示ドライバーの[**Destroyresource**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_destroyresource)関数の呼び出しで*hresource*パラメーターにユーザーモードドライバーリソースハンドルを渡します。 カーネルモードのリソースハンドルと、ユーザーモードのリソースに関連付けられているすべての割り当てを解放するために、ユーザーモードの表示ドライバーは、 [ **\_D3DDDICB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddicb_deallocate)の**hresource**メンバー内のユーザーモードのランタイムリソースハンドルを渡します。このリソースハンドルは、 [*Pfndeallocatecb*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_deallocatecb)関数への呼び出しで、 *pData*パラメーターが指す構造体です。

ユーザーモードのディスプレイドライバーによってリソースが作成および破棄される場合は、次の点を考慮してください。

-   ユーザーモード表示ドライバーが共有リソースへの応答として作成する割り当ての場合 (つまり、D3DDDIARG の**Flags**メンバーに**sharedresource**ビットフィールドフラグが設定された[**createresource**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource)呼び出しへの応答) [ **\_CREATERESOURCE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddiarg_createresource))。ドライバーは、D3DDDICB の**hresource**メンバーに対して**NULL**以外の値を割り当てる必要があります。[**割り当て\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddicb_allocate)です。

-   共有されていないリソースへの応答としてユーザーモード表示ドライバーによって作成される割り当ての場合、ドライバーは、D3DDDICB\_割り当ての**Hresource**メンバーに**NULL**以外の値を割り当てる必要はありません。 ドライバーが**Hresource**に**NULL**を割り当てる場合、割り当ては特定のリソース (およびカーネルモードのリソースハンドル) ではなく、デバイスに関連付けられます。 ただし、割り当てがリソースに実際に関係している場合、ドライバーは割り当てをそのリソースに関連付けます。
    カーネルモードのリソースハンドルは、ユーザーモードの表示ドライバーで D3DDDICB の**Hresource**メンバーが設定されている場合にのみ作成されます。これは、 [**D3DDDIARG\_createresource**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddiarg_createresource)構造体の**Hresource**メンバーから、 [**createresource**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource)への呼び出しで受信したドライバーが、ユーザーモードのランタイムリソースハンドルに割り当て\_ます **。  **

     

-   共有されていないユーザーモードリソースを破棄するために[**Destroyresource**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_destroyresource)が呼び出されると、ユーザーモード表示ドライバーは、 [ **\_D3DDDICB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddicb_deallocate)の**Hresource**メンバーと共に[*pfndeallocatecb*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_deallocatecb)を呼び出すことができます。この場合、ドライバーがリソースに割り当てられていない場合にのみ、割り当てが**NULL**に設定されます。 ユーザーモードでリソースに関連付けられている割り当てを表示する場合、ドライバーは\_D3DDDICB の**Hresource**メンバーを**NULL**以外の値に設定して、 **Pfndeallocatecb**を呼び出す必要があります。それ以外の場合は、メモリリークが発生します。

 

 





