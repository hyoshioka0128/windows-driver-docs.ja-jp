---
title: サーフェス メモリの要求と使用
description: サーフェス メモリの要求と使用
ms.assetid: 7913acc6-ff30-4f2a-8389-37a79940ae8b
keywords:
- WDK ディスプレイの表面のメモリ
- WDK の表示サーフェイスを一覧表示します。
- リソース オブジェクトの表面のメモリ WDK の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 37d574d5e4cb5789751a02bb3407c69807553fe4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356353"
---
# <a name="requesting-and-using-surface-memory"></a>サーフェス メモリの要求と使用


## <span id="ddk_requesting_and_using_surface_memory_gg"></span><span id="DDK_REQUESTING_AND_USING_SURFACE_MEMORY_GG"></span>


ユーザー モードのディスプレイ ドライバーへの呼び出しを受け取るその[ **CreateResource** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource) Microsoft Direct3D ランタイムでは、画面の一覧の作成時に機能します。 Direct3D のランタイムでは、ユーザー モードのディスプレイ ドライバーは、ランタイムにコールバックを使用して画面の一覧にリソース ハンドルを指定します。 ユーザー モードのディスプレイ ドライバーは、サーフェスの一覧を表すためのリソース オブジェクトを作成します。、このオブジェクトを識別する一意のハンドルを生成し、Direct3D のランタイムに戻さハンドルを返します。 ランタイムでは、ドライバーの後続の呼び出しでこの一意のハンドルを使用して、サーフェスの一覧を特定します。 ランタイムに含まれる配列で、画面のインデックスを指定して特定の画面を識別する、 **pSurfList**のメンバー、 [ **D3DDDIARG\_CREATERESOURCE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dukmdt/ns-d3dukmdt-_d3dddiarg_createresource)構造体。

ユーザー モードのディスプレイ ドライバーは、リソースを参照するための呼び出しで、ドライバーの定義済みのリソース ハンドルを受け取る、ため、ドライバーをドライバー定義のリソース オブジェクトを検索するにはコストのかかるハンドルを参照する必要はありません。 同様に、ため、ランタイムがハンドルを参照することも必要ありません、ユーザー モード ドライバーは Direct3D ランタイム定義のリソース ハンドルときに表示されるユーザー モードのドライバーの呼び出し、実行時に表示します。

ユーザー モード ドライバーの呼び出しを表示する、 [ **pfnAllocateCb** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_allocatecb)サーフェスのメモリを割り当てる関数。 **PfnAllocateCb**呼び出し、ユーザー モードのディスプレイ ドライバーは、サーフェスのリストと各個々 の画面で、プライベート データを渡すことができます、 **pPrivateDriverData**のメンバー、 [ **D3DDDICB\_ALLOCATE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddicb_allocate)と[ **D3DDDI\_ALLOCATIONINFO** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dukmdt/ns-d3dukmdt-_d3dddi_allocationinfo)構造体に、それぞれします。 ただし、ユーザー モードのディスプレイ ドライバーがからプライベート データを受け取ることはできません、 **pPrivateDriverData**メンバー。 ユーザー モードのディスプレイ ドライバーはこのプライベート データのメモリを割り当てることができ、後のメモリを解放することができます、 **pfnAllocateCb**戻り値を呼び出すか、スタック メモリを使用して、このプライベート データを渡すことができます。 **PfnAllocateCb**関数がユーザー モードのディスプレイ ドライバーに割り当てられた各画面の各割り当てを識別するハンドルを返します。

**注**  ユーザー モードのディスプレイ ドライバーを呼び出す必要があります、 **pfnAllocateCb**各共有するサーフェス デバイスごとに 1 回の関数。 たとえば、デバイス 1 は、2、3、および 4 のデバイスでも使用される共有画面を作成する場合、2、3、および 4 デバイス呼び出す必要がありますも**pfnAllocateCb**割り当てハンドルを取得するために、共有するサーフェスに 1 回です。

 

ユーザー モードのディスプレイ ドライバーでは、画面の割り当てのハンドル テーブルを維持することにより、通常は、それぞれの面を各割り当てハンドルに追跡する必要があります。 ユーザー モードのディスプレイ ドライバーがドライバー定義のリソース オブジェクト内では、各割り当てハンドルを格納する必要があります。

Direct3D のランタイムが以前に割り当てられた画面で操作を実行する場合 (たとえば、ユーザー モードへの呼び出しでのディスプレイ ドライバーの[ **Blt** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_blt)関数)、ユーザー モードのディスプレイ ドライバーの受信、場合によっては、画面のインデックスで、リソースへのハンドルします。 ユーザー モードのディスプレイ ドライバーでは、このリソース ハンドルを使用して、ドライバーで定義されたリソース オブジェクトを取得します。 ドライバーは、リソース オブジェクトに格納されている割り当てハンドルを取得し、コマンド バッファーにまとめます。 ユーザー モードのディスプレイ ドライバーを呼び出すときに、画面に対応する割り当てハンドルを使用して、 [ **pfnRenderCb** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_rendercb)ディスプレイのミニポート ドライバーをコマンド バッファーを送信する関数。 ディスプレイのミニポート ドライバーを呼び出すことができます、 [ **DxgkCbGetHandleData** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkcb_gethandledata)ユーザー モードのディスプレイ ドライバーが参照するどのサーフェスの割り当てを判断する関数。

 

 





