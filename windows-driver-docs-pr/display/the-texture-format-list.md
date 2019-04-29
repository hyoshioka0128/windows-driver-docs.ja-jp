---
title: テクスチャ形式リスト
description: テクスチャ形式リスト
ms.assetid: 5e60d6e3-d0a2-4b52-86cb-06de839f970a
keywords:
- テクスチャ形式の一覧が DirectX 8.0 リリース ノート WDK Windows 2000 の表示
- テクスチャ形式には、WDK の DirectX 8.0 が一覧表示されます。
- DPIXELFORMAT
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ea327bef458a156b3b663da7041de9890c896ce9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63389884"
---
# <a name="the-texture-format-list"></a>テクスチャ形式リスト


## <span id="ddk_the_texture_format_list_gg"></span><span id="DDK_THE_TEXTURE_FORMAT_LIST_GG"></span>


直接 8.0 では、ピクセル形式を記述するための新しいメカニズムが導入されています。 DirectDraw、Direct3D のピクセルの以前のバージョンでは、形式がデータ構造体で記述 (**DDPIXELFORMAT** (Direct3D ピクセル形式はすべて Fourcc だけですが、0 をされている最下位バイト)。

DDPIXELFORMAT データ構造体は不要になった API レベルのインターフェイスを通じて公開されます。 ただし、DDI レベルでは使用もします。 ドライバーでは、テクスチャ形式の配列が埋め込まれた DDPIXELFORMAT データ構造を持つサーフェスの説明で構成される場合は、そのサポートされているテクスチャ形式を報告します。 ただし、埋め込みのピクセル形式の構造体は、新しいスタイルのピクセル形式をレポートするようになりました使用できます。 DDPIXELFORMAT のデータ構造を使用して、新しいスタイルのピクセル形式を指定するには、設定、 **dwFlags** DDPF 値構造体のフィールド\_D3DFORMAT と新しいピクセルのストア内の識別子の書式指定、 **dwFourCC**フィールド。

さらに、その他の特定の新しいフィールドが DDPIXELFORMAT (新しいフィールドが追加されて既存のフィールドを持つ共用体のメンバーとして、データ構造のサイズは、同じように追加されています。 これらのフィールドが含まれます: **dwOperations**、 **dwPrivateFormatBitCount**、および**wFlipMSTypes**と**wBltMSTypes**します。

DirectX 8.0 DDI 準拠のドライバーは、標準のメカニズムを通じてレポート DX7 スタイルのサーフェスの形式を続行する必要があります、テクスチャ形式の一覧で報告されたドライバーのグローバル データ構造体 ([**D3DHAL\_GLOBALDRIVERDATA**](https://msdn.microsoft.com/library/windows/hardware/ff545963)) と GUID への応答で Z/ステンシルの一覧を報告\_から ZPixelFormats [ **DdGetDriverInfo**](https://msdn.microsoft.com/library/windows/hardware/ff549404)します。 ただし、ドライバーも報告、サポートされる surface 形式のすべて以下に示す新しい DirectX 8.0 DDI メカニズムを通じてします。

使用して DirectX 8.0 DDI スタイルのサーフェスの形式が報告された**GetDriverInfo2**します。 2 つ**GetDriverInfo2**クエリの種類は、ランタイムに使用クエリ画面形式のドライバーから。 D3DGDI2\_型\_GETFORMATCOUNT はドライバーによってサポートされる DirectX 8.0 スタイル画面形式の番号を要求するために使用します。 D3DGDI2\_型\_GETFORMAT が使用される、ドライバーから特定の画面形式のクエリにします。

D3DGDI2 を処理するために\_型\_GETFORMATCOUNT、ドライバーは DirectX 8.0 DDI スタイル サーフェスの形式でサポートされる数を格納する必要があります、 **dwFormatCount**のフィールド、 [ **DD\_GETFORMATCOUNTDATA**](https://msdn.microsoft.com/library/windows/hardware/ff551566)します。

ランタイムが、ドライバーからサポートされている形式の数を受信するとを照会し、各画面の形式の順番で**GetDriverInfo2** D3DGDI2 の種類のクエリ\_型\_GETFORMAT します。 によって示されるデータ構造、 **lpvData**のフィールド、 [ **DD\_GETDRIVERINFODATA** ](https://msdn.microsoft.com/library/windows/hardware/ff551550)データ構造は、この場合、 [ **DD\_GETFORMATDATA**](https://msdn.microsoft.com/library/windows/hardware/ff551569)します。

DirectX 8.0 ランタイムは、ドライバーを調べることによって報告されたテクスチャ形式の一覧をスキャン、 **dwFlags**フィールドの各ピクセル形式。 テクスチャ形式のいずれかであれば**dwFlags** DDPF に設定\_DX8 スタイルとしてこのテクスチャ形式のリストを識別し、ピクセル形式が DDPFとしてマークされていないすべてのテクスチャ形式をフィルター処理、D3DFORMATし、ランタイム\_D3DFORMAT します。 さらに、DDPF のある任意のテクスチャ形式のフィルター DX7 ランタイム\_D3DFORMAT を設定します。 そのため、DX8 DDI をサポートしているドライバーは古いスタイルで指定された 1 つ使用と、新しい 1 つを使用する、サポートされている各形式に対する 2 つのエントリを含むテクスチャ形式の一覧を返すことができます。 DX8 ランタイムは、新しいスタイルで指定された形式を使用し、DX7 ランタイムが古い形式で指定された形式を使用します。

テクスチャや深度やステンシル バッファー、レンダー ターゲット、を通してレポートする必要がありますなど、画面の形式のサポートされるすべての**GetDriverInfo2**メカニズム。 ランタイムは、テクスチャと従来のメカニズムによって返される Z/ステンシル形式を無視 (D3DHAL\_GLOBALDRIVERDATA と GUID\_ZPixelFormats)。 これらの形式を DirectX 8.0 ドライバー DX8 スタイルの形式にマップする処理は行われません。 ただし、以前の形式は、DirectX 7.0 以前のドライバーの新しいスタイルにマップされます。 そのため、ドライバーがサポートされているすべての DirectX 8.0 DDI を通じてサーフェスの形式をレポートする必要があります。 さらに、レガシ ランタイムが以前のスタイル書式設定を新しいスタイルのサーフェス形式をマップされていないために、ドライバーが、従来のメカニズムを通じて DirectX の 7.0 スタイルのサーフェスと Z/ステンシル形式を報告し続けることが重要です。

 

 





