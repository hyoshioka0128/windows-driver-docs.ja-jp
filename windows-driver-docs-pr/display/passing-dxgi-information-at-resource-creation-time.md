---
title: リソース作成時に DXGI 情報を渡す
description: リソース作成時に DXGI 情報を渡す
ms.assetid: d99fc77a-7192-4e45-852a-7a2ae87cc9a2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a6597ddccb98d6abce6025bf6a51634938aac662
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377378"
---
# <a name="passing-dxgi-information-at-resource-creation-time"></a>リソース作成時に DXGI 情報を渡す


ユーザー モードのディスプレイ ドライバーを呼び出すときに、Direct3D のバージョン 10 ランタイムは DXGI に固有の情報を渡すことができます[ **CreateResource(D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createresource)リソースを作成する関数。 ランタイムへのポインターを渡すことができます、 [ **DXGI\_DDI\_プライマリ\_DESC** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi_ddi_primary_desc)構造体、 **pPrimaryDesc**のメンバー、[ **D3D10DDIARG\_CREATERESOURCE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_createresource)プライマリとして、リソースを使用できることを指定する構造体 (つまり、リソース スキャンできますを表示するため)。 ランタイム セット**pPrimaryDesc** 、ランタイムは、D3D10 も設定する場合にのみ NULL 以外の値を\_DDI\_バインド\_内のビットを現在のところ、 **BindFlags**のメンバーD3D10DDIARG\_CREATERESOURCE します。

ランタイムは、DXGI を指定できます\_DDI\_プライマリ\_省略可能フラグ、**フラグ**DXGI のメンバー\_DDI\_プライマリ\_DESC に通知する、ドライバーはフリップ スタイル プレゼンテーションのリソースの使用からオプトアウトできますユーザー モード ディスプレイ ドライバー。 ドライバー、DXGI の設定にフリップ スタイル プレゼンテーションでリソースを使用する必要があることをランタイムに通知、\_DDI\_プライマリ\_ドライバー\_フラグ\_いいえ\_ SCANOUTフラグ**DriverFlags** DXGI のメンバー\_DDI\_プライマリ\_DESC です。

ドライバーは、DXGI を返す場合\_DDI\_プライマリ\_ドライバー\_フラグ\_いいえ\_で SCANOUT、 [ **CreateResource(D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createresource)呼び出すリソースの作成に、常に、ランタイムがこのビット ブロック転送 (bitblt) を実行-(フリップ スタイル プレゼンテーション) ではなくプレゼンテーションをスタイル設定、リソースが、プレゼンテーションのソースの場合。 この機能は、特定のリソースの種類の特定のサブセットをグラフィックス ハードウェアをスキャンできない場合に便利です。 たとえば、グラフィックス ハードウェアは可能性があります。 またはマルチ サンプリングされたバック バッファーの種類のリソースをスキャンできない可能性があります。 さらに、マルチ サンプリングされたバック バッファーをスキャンし、さらに、画面の形式に依存します。 グラフィックス ハードウェアは、特定のマルチ サンプリングされた形式をスキャンできませんだった場合、ユーザー モードのディスプレイ ドライバーは、DXGI 設定\_DDI\_プライマリ\_ドライバー\_フラグ\_いいえ\_SCANOUT フラグ、 **DriverFlags** DXGI のメンバー\_DDI\_プライマリ\_形式のリソースの場合は DESC です。

ランタイムは、DXGI を設定していない場合\_DDI\_プライマリ\_省略可能フラグ、**フラグ**DXGI のメンバー\_DDI\_プライマリ\_DESC ドライバーに通知しますフリップ スタイル プレゼンテーションのリソースの使用を無効にする可能性について、ドライバーは引き続き、DXGI を返す\_DDI\_ERR\_サポートされていないエラー コード、DXGI と共に\_DDI\_プライマリ\_ドライバー\_フラグ\_いいえ\_への呼び出しから SCANOUT フラグ[ **CreateResource(D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createresource)します。 ドライバーの*CreateResource(D3D10)* 渡します DXGI\_DDI\_ERR\_への呼び出しでサポートされていない、 [ **pfnSetErrorCb** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_seterror_cb)関数の場合は、ドライバーはこのようなプライマリをスキャンできません。 返す DXGI\_DDI\_ERR\_DXGI と共にサポートされていない\_DDI\_プライマリ\_ドライバー\_フラグ\_いいえ\_SCANOUT によりする DXGIバック バッファーと、プライマリの画面の間、プレゼンテーションのパスでプロキシのサーフェスを interpose します。 プロキシ画面は、サイズ、マルチ サンプリング、および回転の観点から、プライマリ (スキャン アウト) 画面を常に一致します。 このプロセスの最初の手順は、マルチ サンプリングの判断するために、DXGI または回転の設定により、スキャンしたこれらの設定画面を拒否するように、ドライバー。 DXGI は、背面のスケーリングと回転せず、マルチ サンプリング、なし、または両方を指定せずにプライマリを作成しようとしてこの判断を行います。 スキャン アウト機能のドライバーのサポートを決定する DXGI、DXGI によってプライマリ サーバーとプロキシのサーフェスが作成され、ドライバーは、これら 2 つの画面間を反転できる必要があります。 DXGI 呼び出してドライバーの自動回転またはマルチ サンプリングされたバック バッファーのアプリケーションの要求を満たす後まだ[ **BltDXGI** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi_ddi_base_functions)関数戻るから bitblt を実行するバッファーをプロキシのサーフェイス。 これら bitblt multisample 解決を実行するドライバーを要求または回転します。 詳細については*BltDXGI*を参照してください、 **BltDXGI**リファレンス ページです。

 

 





