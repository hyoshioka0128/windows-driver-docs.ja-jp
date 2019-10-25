---
title: リソース作成時に DXGI 情報を渡す
description: リソース作成時に DXGI 情報を渡す
ms.assetid: d99fc77a-7192-4e45-852a-7a2ae87cc9a2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: af50947aa02fb92a8b73742c43c36baaed8415b0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829861"
---
# <a name="passing-dxgi-information-at-resource-creation-time"></a>リソース作成時に DXGI 情報を渡す


Direct3D バージョン10ランタイムは、ユーザーモードの display driver の[**Createresource (D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createresource)関数を呼び出してリソースを作成するときに、DXGI 固有の情報を渡すことができます。 ランタイムは、 [**D3D10DDIARG\_CREATERESOURCE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_createresource)構造体の**pprimarydesc**メンバーで、 [**DXGI\_DDI\_プライマリ\_DESC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_primary_desc)構造体へのポインターを渡して、リソースをプライマリとして使用できることを指定します (つまり、リソースが表示されます。 ランタイムは、D3D10DDIARG\_CREATERESOURCE の**Bindflags**メンバー内の D3D10\_DDI\_BIND\_PRESENT を設定する場合にのみ、 **PPRIMARYDESC**を NULL 以外の値に設定します。

ランタイムでは、dxgi\_\_の**Flags**メンバーである\_DDI\_プライマリ\_オプションのフラグを指定できます。このフラグは、ドライバーがのリソースを使用しないことをユーザーモード表示ドライバーに通知するために使用します。フリップスタイルのプレゼンテーション。 フリップスタイルのプレゼンテーションでリソースを使用しないことをランタイムに通知するために、ドライバーでは、dxgi の**Driverflags**メンバーに\_\_\_フラグが設定されていないことを示す、\_DDI\_プライマリドライバーを設定\__ DDI\_プライマリ\_DESC です。

ドライバーが DXGI\_DDI\_プライマリ\_ドライバー\_フラグを返した場合、リソースを作成するために[**Createresource (D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createresource)の呼び出しで\_\_はスキャンされません。ランタイムは常にビットブロック転送 (bitblt) スタイルを実行します。リソースがプレゼンテーションのソースである場合は、(フリップスタイルのプレゼンテーションではなく) プレゼンテーション。 この機能は、グラフィックスハードウェアが特定のリソースの種類の特定のサブセットをスキャンできない場合に便利です。 たとえば、グラフィックスハードウェアでは、マルチサンプリングテクスチャバックバッファーの種類のリソースをスキャンできない場合があります。 さらに、マルチサンプリングテクスチャバックバッファーをスキャンする機能は、サーフェイスの形式によってさらに依存する場合があります。 グラフィックスハードウェアが特定のマルチサンプリングテクスチャ形式をスキャンできなかった場合は、ユーザーモードの表示ドライバーによって、 **Driverflags**\_DDI\_プライマリ\_ドライバー\_\_フラグが設定されます。この形式のリソースについては、DXGI\_DDI のメンバーがプライマリ\_DESC\_ます。

ランタイムが DXGI\_DDI を設定していない場合は、\_DXGI の**Flags**メンバーで\_\_オプションフラグが指定されていません。このフラグは、\_次のリソースを使用しなくなった場合に、ドライバーに通知します。フリップスタイルのプレゼンテーションでも、ドライバーは、\_サポートされていないエラーコードと共に、dxgi\_DDI\_プライマリ\_ドライバー\_フラグを返すことができます。また、呼び出しからの\_\_の\_\_SCANOUT フラグません。[**Createresource (D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createresource)にします。 ドライバーの*Createresource (D3D10)* は、ドライバーがプライマリをスキャンできない場合に、 [**pfnSetErrorCb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_seterror_cb)関数の呼び出しでサポートされていない\_DDI\_\_ERR を渡します。 Dxgi\_DDI\_の\_サポートされていません。 DXGI\_DDI\_プライマリ\_ドライバ\_フラグ\_\_の SCANOUT によって、interpose がプレゼンテーションパスのプロキシ画面に表示されます。バックバッファーとプライマリサーフェイスの間。 プロキシサーフェスは、サイズ、マルチサンプリング、および回転という点で、プライマリ (スキャンアウト) サーフェイスと常に一致します。 このプロセスの最初の手順は、DXGI によって、ドライバーがこれらの設定でサーフェイスをスキャンすることを拒否するマルチサンプリングまたはローテーションの設定を決定することです。 DXGI は、スケールバックしてプライマリを作成しようとすることで、マルチサンプリングを使用したり、両方を使用したりせずに、この決定を行います。 DXGI によってスキャンアウト機能のドライバーのサポートが決定された後、DXGI によってプライマリサーフェスとプロキシサーフェスが作成され、ドライバーはこれらの2つのサーフェス間を反転できるようになります。 また、バッファーからプロキシ画面に bitblts を実行するには、ドライバーの[**Bltdxgi**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_base_functions)関数を呼び出して、自動回転またはマルチサンプリングテクスチャバックバッファーに対するアプリケーションの要求を処理します。 これらの bitblts は、マルチサンプリングの解決またはローテーションを実行するようにドライバーに要求します。 *Bltdxgi*の詳細については、 **bltdxgi**のリファレンスページを参照してください。

 

 





