---
title: サーフェスの種類
description: サーフェスの種類
ms.assetid: 7374b783-ef09-4238-a17a-fafcd9d87b3f
keywords:
- DIB WDK GDI
- デバイス管理のサーフェス WDK GDI
- WDK GDI エンジン管理画面
- セキュリティ ネゴシエーション WDK GDI、サーフェイスのタイプ
- WDK GDI の種類を画面します。
- デバイス依存ビットマップ WDK GDI
- DDB WDK GDI
- WDK GDI のデバイスに依存しないビットマップ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d9a36f88e5be4804d74aa33ff48f5d5e94c95a81
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354208"
---
# <a name="surface-types"></a>サーフェスの種類


## <span id="ddk_surface_types_gg"></span><span id="DDK_SURFACE_TYPES_GG"></span>


処理方法のコンテキストでは、サーフェイスのタイプを表示できます。 次の種類があります。

-   サーフェスのエンジン管理

-   デバイス管理のサーフェス (標準形式のビットマップ)

-   デバイス管理のサーフェス (標準以外の形式のビットマップ)

### <a name="span-idengine-managedsurfacesspanspan-idengine-managedsurfacesspanspan-idengine-managedsurfacesspanengine-managed-surfaces"></a><span id="Engine-Managed_Surfaces"></span><span id="engine-managed_surfaces"></span><span id="ENGINE-MANAGED_SURFACES"></span>サーフェスのエンジン管理

エンジンが管理の画面には:

-   作成され、GDI によって管理されます。

-   標準 DIB のいずれかでデバイスに依存しないビットマップ (DIB) 形式として作成されます: 配信元が左上隅にあるの上から下へ、またはボトムアップ、配信元が左上隅にあるのです。

-   %S 型の種類の\_ビットマップ。

-   処理を画面に対応するデバイスはありません。

標準形式のビットマップは、1 つの平面ピクセル (各ピクセルのデータは連続的に格納) 形式のビットマップ。 ビットマップの場合は、各スキャン ラインは、4 バイト境界に揃えられます。

ビットマップが作成された、 [ **EngCreateBitmap** ](https://msdn.microsoft.com/library/windows/hardware/ff564199)関数は DIB 形式。 ビットマップは、管理するエンジンの DIB 形式でなければなりません。

### <a name="span-iddevice-managedsurfacesstandard-formatbitmapsspanspan-iddevice-managedsurfacesstandard-formatbitmapsspanspan-iddevice-managedsurfacesstandard-formatbitmapsspandevice-managed-surfaces-standard-format-bitmaps"></a><span id="Device-Managed_Surfaces__Standard-Format_Bitmaps_"></span><span id="device-managed_surfaces__standard-format_bitmaps_"></span><span id="DEVICE-MANAGED_SURFACES__STANDARD-FORMAT_BITMAPS_"></span>デバイス管理のサーフェス (標準形式のビットマップ)

デバイス管理の画面:

-   デバイス ドライバーへの呼び出しによって作成された[ **DrvCreateDeviceBitmap** ](https://msdn.microsoft.com/library/windows/hardware/ff556185)関数。

-   関連付けられているデバイス、画面へのハンドルを持つ (DHSURF; 詳細については、次を参照してください。 [ **SURFOBJ**](https://msdn.microsoft.com/library/windows/hardware/ff569901))。

-   いずれかになります*不透明*または*nonopaque*します。

非透過のデバイス管理の画面とは、GDI がいるビットマップ形式に関する情報も、ビットへの参照をビットマップ内のことです。 これらの理由から、ドライバーする必要がありますをサポートして、少なくとも、 [ **DrvBitBlt**](https://msdn.microsoft.com/library/windows/hardware/ff556180)、 [ **DrvTextOut**](https://msdn.microsoft.com/library/windows/hardware/ff557277)、および[ **DrvStrokePath** ](https://msdn.microsoft.com/library/windows/hardware/ff556316)関数。 このようなサーフェイスの型は %s 型\_DEVBITMAP します。

Nonopaque デバイス管理の画面は対象の GDI ビットマップ形式に関する情報があるし、ビットマップ内のビットの場所を知っています。 このため、ドライバーは、すべての GDI に遅延の描画操作を実装するには必要ありません。 このような画面の種類は SYTPE\_ビットマップ。

デバイス管理の不透明なビットマップを nonopaque ものに変換するドライバー、呼び出す必要があります、 [ **EngModifySurface** ](https://msdn.microsoft.com/library/windows/hardware/ff564976)関数。 この呼び出しで、ドライバーはビットマップ形式の GDI とビットマップ メモリ内の場所お知らせいたします。

ドライバーにデバイスで管理された DIB 領域がある場合は、ドライバーが GDI GDI サーフェイスに描画するに戻る呼び出すことができます。 DIB をラップすることで GDI にコールバックを引き続き参照できますが、独自のサーフェスを管理するの DIB を使用してドライバー (で作成されますが、 [ **EngCreateBitmap** ](https://msdn.microsoft.com/library/windows/hardware/ff564199)関数)、画面の周りします。 次の手順では、ドライバーが GDI のデバイス管理の DIB 表面に描画を持つことができますかについて説明します。

1.  ドライバー呼び出し[ **EngCreateBitmap** ](https://msdn.microsoft.com/library/windows/hardware/ff564199) DIB のエンジン管理画面を作成します。

2.  ドライバーの呼び出し、 [ **EngCreateDeviceBitmap** ](https://msdn.microsoft.com/library/windows/hardware/ff564204)デバイスで管理された DIB サーフェスはデバイス依存ビットマップ (DDB) 画面を作成する関数。

3.  ドライバーは、DDB のデバイスで管理されたデータで内部的には DIB のエンジンに管理されたデータを保存します。

4.  GDI は、デバイスで管理された DDB データを画面と対話するドライバーを常に呼び出します。

5.  ドライバーが GDI から呼び出しを受信し、呼び出しを処理することはできません (たとえば、ドライバー処理できない複雑なクリッピング)、ドライバーは DDB データに格納され、DIB データを表示するために、GDI に渡す DIB データを取得します。

### <a name="span-iddevice-managedsurfacesnonstandard-formatbitmapsspanspan-iddevice-managedsurfacesnonstandard-formatbitmapsspanspan-iddevice-managedsurfacesnonstandard-formatbitmapsspandevice-managed-surfaces-nonstandard-format-bitmaps"></a><span id="Device-Managed_Surfaces__Nonstandard-Format_Bitmaps_"></span><span id="device-managed_surfaces__nonstandard-format_bitmaps_"></span><span id="DEVICE-MANAGED_SURFACES__NONSTANDARD-FORMAT_BITMAPS_"></span>デバイス管理のサーフェス (標準以外の形式のビットマップ)

ドライバーは、デバイスで管理された非 DIB 画面を有効に呼び出すことによって、 [ **EngCreateDeviceSurface** ](https://msdn.microsoft.com/library/windows/hardware/ff564206)が GDI サーフェスを作成しを識別するハンドルを返す関数。 GDI は、およびデバイス管理の画面から読み取り、描画コントロールへのアクセスには、ドライバーに依存します。

デバイス形式のビットマップとも呼ばれますが、デバイス依存ビットマップ (DDB) は、別の種類の DIB 以外、デバイス管理の画面です。 DDB は高速画面ビットマップに対してブロック転送を実装するために、VGA ドライバーなど、特定のドライバーを許可するサポートされています。 DDB では、オフスクリーン表示メモリ バンクに描画するためにドライバーや非 DIB ビットマップもできます。 ドライバーがサポートできる、DDB が必要な場合、 [ **DrvCreateDeviceBitmap** ](https://msdn.microsoft.com/library/windows/hardware/ff556185)関数と呼び出し、 [ **EngCreateDeviceBitmap** ](https://msdn.microsoft.com/library/windows/hardware/ff564204)関数をビットマップへのハンドルを返すエンジン。

 

 





