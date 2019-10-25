---
title: テクスチャ形式リスト
description: テクスチャ形式リスト
ms.assetid: 5e60d6e3-d0a2-4b52-86cb-06de839f970a
keywords:
- DirectX 8.0 リリースノート WDK Windows 2000 display、テクスチャ形式の一覧
- テクスチャ形式は、WDK DirectX 8.0 を一覧表示します
- Dピクセル形式
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 08520cd5664624e7dc6d102f7378ef6c912502a6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825503"
---
# <a name="the-texture-format-list"></a>テクスチャ形式リスト


## <span id="ddk_the_texture_format_list_gg"></span><span id="DDK_THE_TEXTURE_FORMAT_LIST_GG"></span>


ダイレクト8.0 では、ピクセル形式を記述するための新しいメカニズムが導入されています。 以前のバージョンの DirectDraw および Direct3D ピクセル形式は、データ構造 (**dd画素形式**) で記述されていました (direct3d ピクセル形式は、ほとんどの場合、最小の重要なバイトが0である)。

DDピクセル形式のデータ構造は、API レベルのインターフェイスを介して公開されなくなりました。 ただし、これは引き続き DDI レベルで使用されます。 ドライバーは、埋め込みの DDピクセル形式のデータ構造を含む表面の説明で構成されるテクスチャ形式配列を通じて、サポートされているテクスチャ形式を報告します。 ただし、埋め込みピクセル形式の構造を使用して、新しいスタイルピクセル形式を報告できるようになりました。 DDPIXEL 形式のデータ構造を使用して新しいスタイルピクセル形式を指定するには、構造体の**dwFlags**フィールドを値 ddpf\_D3DFORMAT に設定し、新しいピクセル形式識別子を**dwfourcc**フィールドに格納します。

さらに、新しいフィールドが DDピクセル形式に追加されています (新しいフィールドは、既存のフィールドと共に共用体のメンバーとして追加されているため、データ構造のサイズは同じです)。 これらのフィールドには、 **Dwoperations**、 **dwprivateformatbitcount**、 **wFlipMSTypes**と**wBltMSTypes**が含まれます。

DirectX 8.0 DDI に準拠しているドライバーは、標準のメカニズム、つまり、グローバルドライバーのデータ構造 ([**D3DHAL\_GLOBALDRIVERDATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_globaldriverdata)) と Z/ステンシルで報告されたテクスチャ形式の一覧を使用して、DX7 スタイルの表面形式を報告する必要があります。リストは、 [**Ddgetdriverinfo**](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_getdriverinfo)から GUID\_Zピクセル形式に応答して報告されます。 ただし、ドライバーは、以下で説明する新しい DirectX 8.0 DDI メカニズムを使用して、サポートされているすべての表面形式を報告する必要があります。

DirectX 8.0 DDI スタイルのサーフェイス形式は、 **GetDriverInfo2**を使用して報告されます。 2つの**GetDriverInfo2**クエリの種類は、ドライバーからの surface 形式を照会するためにランタイムによって使用されます。 D3DGDI2\_TYPE\_GETFORMATCOUNT は、ドライバーでサポートされている DirectX 8.0 スタイルのサーフェイス形式の数を要求するために使用されます。 D3DGDI2\_TYPE\_GETFORMAT は、ドライバーから特定の surface 形式を照会するために使用されます。

D3DGDI2\_TYPE\_GETFORMATCOUNT を処理するには、ドライバーは、 [**DD\_GETFORMATCOUNTDATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_dd_getformatcountdata)の**dwFormatCount**フィールドでサポートされている DirectX 8.0 DDI 形式の画面の数を格納する必要があります。

ランタイムは、ドライバーからサポートされている形式の数を受信すると、D3DGDI2\_TYPE\_GETFORMAT 型の**GetDriverInfo2**クエリを使用して、各サーフェス形式に対してクエリを実行します。 [**Dd\_GETDRIVERINFODATA**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_getdriverinfodata)データ構造の**lpvdata**フィールドが指すデータ構造は、この場合は[**dd\_getformatdata**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_dd_getformatdata)です。

DirectX 8.0 ランタイムは、ドライバーによって報告された、各ピクセル形式の**dwFlags**フィールドを調べるテクスチャ形式の一覧をスキャンします。 いずれかのテクスチャ形式で、 **dwFlags**が ddpf\_D3DFORMAT に設定されている場合、ランタイムはこのテクスチャ形式リストを DX8 style として識別し、ピクセル形式が ddpf\_D3DFORMAT としてフラグ付けされていないすべてのテクスチャ形式をフィルター処理します。 さらに、DX7 ランタイムは、DDPF\_D3DFORMAT set を含むすべてのテクスチャ形式をフィルター処理します。 このため、DX8 DDI をサポートするドライバーは、サポートされている各形式の2つのエントリを含むテクスチャ形式リストを返すことができます。1つは古いスタイルで指定され、もう1つは新しいに含まれます。 DX8 ランタイムは、新しいスタイルで指定された形式を使用し、DX7 ランタイムは古いスタイルで指定された形式を使用します。

テクスチャ、深度、ステンシルバッファー、レンダーターゲットなど、サポートされているすべてのサーフェス形式は、 **GetDriverInfo2**メカニズムを使用して報告する必要があります。 レガシメカニズム (D3DHAL\_GLOBALDRIVERDATA および GUID\_Zピクセル形式) によって返されたテクスチャおよび Z/ステンシル形式は、ランタイムによって無視されます。 これらの形式を DirectX 8.0 ドライバーの DX8 スタイル形式にマップしようとしていません。 ただし、レガシ形式は DirectX 7.0 以前のドライバーの新しいスタイルにマップされます。 そのため、ドライバーは DirectX 8.0 DDI を通じて、サポートされているすべての表面形式を報告する必要があります。 また、レガシランタイムは新しいスタイルの表面形式を古いスタイルの形式にマップしないため、ドライバーは従来のメカニズムを使用して DirectX 7.0 のスタイル画面と Z/ステンシル形式を引き続きレポートすることが重要です。

 

 





