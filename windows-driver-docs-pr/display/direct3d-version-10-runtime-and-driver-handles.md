---
title: Direct3D バージョン 10 ランタイムおよびドライバー ハンドル
description: Direct3D バージョン 10 ランタイムおよびドライバー ハンドル
ms.assetid: 1e50afe1-7103-45c4-8f58-a08d51423b22
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c8920e6ff83f7b90aa401d6f8bec27d9b4e9d702
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839733"
---
# <a name="direct3d-version-10-runtime-and-driver-handles"></a>Direct3D バージョン 10 ランタイムおよびドライバー ハンドル


Direct3D version 10 runtime と driver handle は同じ有効期間を共有します。 Direct3D ランタイムは、作成型関数の呼び出し ( [**Createresource (D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createresource)など) と破棄型関数の呼び出し (たとえば、 [**DESTROYRESOURCE (D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_destroyresource)) の間のオブジェクトの有効期間を指定します。 ランタイムは、ドライバーハンドルの値とランタイムハンドルの値を提供します。 これらのハンドルは、基本的に、操作対象のオブジェクトを識別するために厳密な型でラップされたポインターです。 リソースのランタイムハンドルとドライバーハンドルの例を次に示します。

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

レンダリングデバイスオブジェクトとその子オブジェクトのすべてのドライバーハンドルは、次の2つのパスの作成メカニズムを使用します。

1.  ドライバーハンドルポインターの値を確認するために、ランタイムは最初に_CalcPrivate_**ObjType**_Size_関数 (たとえば、 [**CalcPrivateResourceSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_calcprivateresourcesize)関数) を呼び出します。 この呼び出しでは、ランタイムは作成パラメーター ( [**D3D10DDIARG\_CREATERESOURCE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_createresource)構造体へのポインターなど) を渡します。 ランタイムは、 _Create_**ObjType**関数の呼び出しで作成パラメーターも渡します。

    通常、ユーザーモードの表示ドライバーでは、 _CalcPrivate_**ObjType**_Size_の呼び出し中に何も割り当てる必要はありません。 ただし、ドライバーが失敗した場合、または他の種類のエラー条件を示す必要がある場合、ドライバーは\_T (-1) のサイズを返してハンドルの作成を防止できます。 次に、ランタイムは、OUTOFMEMORY エラー条件を呼び出し元アプリケーションに\_返します。

    最小では、ドライバーは_CalcPrivate_**ObjType**_Size_の呼び出しから**sizeof (** void\* **)** を返します。

2.  ランタイムが、ユーザーモード表示ドライバーに必要なサイズを満たすために十分な領域を割り当てることができる場合、ランタイムは、同じ作成パラメーターを使用して_Create_**ObjType**関数 (たとえば、 [**createresource (D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createresource)) を呼び出します。と共に、ドライバーハンドルの新しい一意の値を指定します。 ドライバーハンドルのポインター値は、 _CalcPrivate_**ObjType**_size_によって返されたサイズのメモリ領域を指すため、ハンドルの有効期間に対して一意であり、定数になります。 ユーザーモードの表示ドライバーでは、必要に応じてこのメモリ領域を使用できます。 頻繁にアクセスされるデータをランタイムが提供するメモリ領域に配置することにより、ドライバーの効率が向上します。

 

 





