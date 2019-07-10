---
title: Direct3D バージョン 10 ランタイムおよびドライバー ハンドル
description: Direct3D バージョン 10 ランタイムおよびドライバー ハンドル
ms.assetid: 1e50afe1-7103-45c4-8f58-a08d51423b22
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6a3a1ebcc751ba8eb64412f5ba89564e192bab2e
ms.sourcegitcommit: fee68bc5f92292281ecf1ee88155de45dfd841f5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/10/2019
ms.locfileid: "67716871"
---
# <a name="direct3d-version-10-runtime-and-driver-handles"></a>Direct3D バージョン 10 ランタイムおよびドライバー ハンドル


Direct3D のバージョン 10 とドライバーのランタイム ハンドルは、同じ有効期間を共有します。 Direct3D のランタイムを作成する型の関数呼び出しの間でオブジェクトの有効期間を指定します (たとえば、 [ **CreateResource(D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createresource)) 破棄型関数の呼び出し (たとえば、 [ **DestroyResource(D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_destroyresource))。 ランタイムは、ランタイム ハンドルの値だけでなく、ドライバー ハンドル値を提供します。 これらのハンドルは、操作対象のオブジェクトを識別する厳密な型でラップされているポインター基本的にです。 リソースのランタイムとドライバーの処理の例を次に示します。

```cpp
// Strongly typed handle to identify a resource object to the driver: 
typedef struct D3D10DDI_HRESOURCE
{
    void* pDrvPrivate; // Pointer to memory location as large as the driver requested.
} D3D10DDI_HRESOURCE;

// Strongly typed handle to identify a resource object to the runtime:
typedef struct D3D10DDI_HRTRESOURCE
{
    void* handle;
} D3D10DDI_HRTRESOURCE;
```

レンダリング デバイス オブジェクトとその子オブジェクトのすべてのドライバー ハンドルには、次の 2 つのパスの作成メカニズムが行われます。

1.  ランタイム ドライバー ハンドルのポインターの値を確認するのにはまず、 _CalcPrivate_**ObjType**_サイズ_関数 (たとえば、 [ **CalcPrivateResourceSize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_calcprivateresourcesize)関数)。 ランタイムはこの呼び出しで、作成パラメーターに渡します (たとえばへのポインター、 [ **D3D10DDIARG\_CREATERESOURCE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_createresource)構造)。 ランタイムにもへの呼び出しで作成パラメーターに渡す、_作成_**ObjType**関数。

    呼び出し中に何も割り当てに一般的には、ユーザー モードのディスプレイ ドライバーが不要_CalcPrivate_**ObjType**_サイズ_します。 ただし、ドライバーは、障害が発生したり、他の種類のエラー状態を示す必要があります、ドライバーを返すサイズ\_ハンドル作成されないようにする T (-1)。 ランタイムは戻ります E\_呼び出し元アプリケーションに OUTOFMEMORY エラー条件。

    少なくとも、ドライバーを返す必要があります**sizeof (** void\* **)** への呼び出しから_CalcPrivate_**ObjType** _サイズ_します。

2.  ランタイムは、ランタイムを呼び出し、ユーザー モードのディスプレイ ドライバーによって、サイズが必要なを満たすために十分な領域を割り当てることができる場合、_作成_**ObjType**関数 (たとえば、 [ **CreateResource(D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createresource)) ドライバーのハンドルの新しい一意の値と共に、同じ作成パラメーターを使用します。 ドライバーのハンドルのポインター値が一意になるし、メモリの領域を指すように、ハンドルの有効期間の定数のサイズがによって返される_CalcPrivate_**ObjType** _サイズ_します。 ユーザー モードのディスプレイ ドライバーは、必要に応じてこのメモリ領域を使用できます。 ドライバーは、ランタイムによって提供されるメモリの領域に、頻繁にアクセスされるデータを配置することにより、効率化の増加を得る必要があります。

 

 





