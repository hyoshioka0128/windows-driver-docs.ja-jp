---
title: サーフェス メモリの要求と使用
description: サーフェス メモリの要求と使用
ms.assetid: 7913acc6-ff30-4f2a-8389-37a79940ae8b
keywords:
- surface メモリ WDK 表示
- サーフェスの一覧表示 WDK ディスプレイ
- リソースオブジェクトのサーフェイスメモリの WDK 表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 85d6f6eee6e9b11d6b8bdf5c5634738e25f097c6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825927"
---
# <a name="requesting-and-using-surface-memory"></a>サーフェス メモリの要求と使用


## <span id="ddk_requesting_and_using_surface_memory_gg"></span><span id="DDK_REQUESTING_AND_USING_SURFACE_MEMORY_GG"></span>


ユーザーモードの表示ドライバーは、Microsoft Direct3D ランタイムがサーフェイスの一覧の作成を必要とするときに、 [**Createresource**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource)関数の呼び出しを受け取ります。 Direct3D ランタイムは、ユーザーモード表示ドライバーがランタイムにコールバックするために使用するサーフェイスのリストへのリソースハンドルを指定します。 ユーザーモードの表示ドライバーは、サーフェイスのリストを表すリソースオブジェクトを作成し、このオブジェクトへの一意のハンドルを生成し、そのハンドルを Direct3D ランタイムに戻します。 ランタイムは、後続のドライバー呼び出しでこの一意のハンドルを使用して、サーフェイスの一覧を識別します。 ランタイムは、 [**D3DDDIARG\_CREATERESOURCE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddiarg_createresource)構造体の**p**メンバーに格納されている配列内のサーフェイスのインデックスを指定することによって、特定のサーフェイスを識別します。

ユーザーモードの表示ドライバーは、リソースを参照する呼び出しでドライバーによって定義されたリソースハンドルを受け取るため、ドライバーで定義されたリソースオブジェクトを検索するために、コストのかかるハンドルの参照を実行する必要はありません。 同様に、ランタイムがハンドルの参照を実行する必要がないように、ユーザーモードの表示ドライバーは、ユーザーモードの display ドライバーがランタイムにコールバックするときに、Direct3D ランタイムによって定義されたリソースハンドルを使用します。

ユーザーモード表示ドライバーは、 [**Pfnallocatecb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_allocatecb)関数を呼び出して、サーフェイスにメモリを割り当てます。 **Pfnallocatecb**呼び出しでは、ユーザーモードの表示ドライバーは、各画面の一覧と、 [**D3DDDICB\_ALLOCATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddicb_allocate)と[**D3DDDI\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddi_allocationinfo)の割り当て情報構造体の**pprivatedriverdata**メンバー内の個々のサーフェイスのプライベートデータを渡すことができます。 ただし、ユーザーモード表示ドライバーは、 **Pprivatedriverdata**メンバーからプライベートデータを受信することはできません。 ユーザーモードの表示ドライバーは、このプライベートデータにメモリを割り当てることができ、 **Pfnallocatecb**呼び出しが返された後でメモリを解放したり、スタックメモリを使用してこのプライベートデータを渡したりすることができます。 **Pfnallocatecb**関数は、割り当てられた各サーフェイスの各割り当てを示すハンドルをユーザーモード表示ドライバーに返します。

ユーザーモードの表示ドライバーでは、各デバイスの共有サーフェイスごとに**Pfnallocatecb**関数を1回呼び出す必要**が   ます**。 たとえば、デバイス1がデバイス2、3、および4でも使用される共有サーフェスを作成する場合、デバイス2、3、および4も、割り当てハンドルを取得するために、共有サーフェスに対して**Pfnallocatecb**を1回呼び出す必要があります。

 

ユーザーモードの表示ドライバーでは、各割り当てハンドルに対して各画面を追跡する必要があります。通常は、画面に割り当てられたハンドルテーブルを維持します。 ユーザーモードの表示ドライバーでは、ドライバー定義のリソースオブジェクト内に各割り当てハンドルを格納する必要があります。

Direct3D ランタイムが、以前に割り当てられたサーフェイスに対して操作を実行すると (たとえば、ユーザーモード表示ドライバーの[**Blt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_blt)関数の呼び出しで)、ユーザーモードの表示ドライバーは、リソースへのハンドルを受け取ります (場合によってはサーフェイスインデックスを使用します)。 ユーザーモードの表示ドライバーは、このリソースハンドルを使用して、ドライバーによって定義されたリソースオブジェクトを取得します。 ドライバーは、リソースオブジェクトに格納されている割り当てハンドルを取得し、それらをコマンドバッファーにアセンブルします。 ユーザーモード表示ドライバーは、 [**Pfnrendercb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_rendercb)関数を呼び出してディスプレイミニポートドライバーにコマンドバッファーを送信するときに、サーフェイスに対応する割り当てハンドルを使用します。 表示ミニポートドライバーは、 [**DxgkCbGetHandleData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkcb_gethandledata)関数を呼び出して、ユーザーモード表示ドライバーで参照されているサーフェイスの割り当てを確認できます。

 

 





