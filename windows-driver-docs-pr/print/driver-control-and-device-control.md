---
title: ドライバー コントロールとデバイス コントロール
description: ドライバー コントロールとデバイス コントロール
ms.assetid: ff515e88-9a94-420f-a6c8-fba3483c00e5
keywords:
- WDK の印刷の独自の色の管理
- DrvIcmCreateColorTransform
- WDK の印刷の色のドライバー制御の管理
- WDK の印刷の色のデバイス制御の管理
- ドライバーの色の管理色管理 WDK の WDK を参照してください。
- デバイスの色の管理色管理 WDK の WDK を参照してください。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cea941a3b82435bc705b2d8e2c6c94d122bef660
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383540"
---
# <a name="driver-control-and-device-control"></a>ドライバー コントロールとデバイス コントロール





色の管理が指定されている場合、いずれかのドライバーまたはプリンターのハードウェア、ドライバーの[プリンター グラフィックス DLL](printer-graphics-dll.md) 、GCAPS を設定する必要があります\_ICM フラグ、 [ **DEVINFO**](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-tagdevinfo)構造体。

ドライバーは CYMK 色空間 (該当する場合)、「」のサポートを指定する必要があります[CMYK カラー領域をサポートしている](supporting-cmyk-color-space.md)します。

プリンター グラフィックス Dll には、次の 3 つの関数を定義する必要があります。

[**DrvIcmCreateColorTransform**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvicmcreatecolortransform)

[**DrvIcmDeleteColorTransform**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvicmdeletecolortransform)

[**DrvIcmCheckBitmapBits**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvicmcheckbitmapbits)

GDI の呼び出し、 [ **DrvIcmCreateColorTransform** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvicmcreatecolortransform) ICC プロファイルが (Microsoft Windows SDK のドキュメントで説明) を使用した印刷ジョブのドライバーを指定する関数。 関数は、これらのプロファイルを指定するには、色の情報を修正するときに使用する、内部色変換を作成できます。 色の変換は、ドライバー固有、内部的に定義されている 1 つの色空間から別のマッピングです。 関数は、GDI を格納すると、変換にハンドルを返します。

内のフラグ、 [ **BRUSHOBJ** ](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_brushobj)と[ **XLATEOBJ** ](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_xlateobj)構造体は、色の管理をシステムによって実行されているかどうかを示します (またはアプリケーションの場合) またはドライバー (またはデバイス)。 各ドライバー実装グラフィックスにこれらの構造体のいずれか (または両方) を受け取る DDI 描画関数、フラグをチェックする必要があります。 システムまたはアプリケーションでは、色の管理を処理することは現在場合、ドライバーまたはデバイスは許可されません。 ドライバーまたはデバイスの色の管理が有効になっている場合、グラフィックス DDI 関数を呼び出す必要があります[ **BRUSHOBJ\_hGetColorTransform** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-brushobj_hgetcolortransform)または[ **XLATEOBJ\_hGetColorTransform** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-xlateobj_hgetcolortransform) (または両方) を使用する色変換を識別するハンドルを取得します。 ハンドルには、以前の呼び出しへの応答に、ドライバーが用意されているいずれかになります、 [ **DrvIcmCreateColorTransform** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvicmcreatecolortransform)関数。

### <a name="handling-proprietary-color-management"></a>独自の色の管理を処理します。

一部のデバイスでは、独自の色の管理または実行されます (いずれか、ドライバーによってハードウェアによって) ICM が有効になっているかどうかに関係なく。 このようなデバイス ドライバーがイメージを受信したデータは既に修正されている場合に実行する色補正することはできません。 場合、precorrected データを受信できます。

-   アプリケーションが色補正"DC"の外部イメージ (Microsoft Windows SDK のドキュメントを参照してください)。

-   色の管理は、システムによって処理されます。

これらのシナリオでは、両方、BR のいずれかの\_ホスト\_ICM フラグ、 **flColorType**のメンバー [ **BRUSHOBJ** ](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_brushobj)と、XO\_ホスト\_ICM フラグ、 **flXlate**のメンバー [ **XLATEOBJ** ](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_xlateobj)が設定されます。 これらのフラグを設定する場合でも、 **dmICMMethod**のメンバー [ **DEVMODEW** ](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-_devicemodew)は DMICMMETHOD\_NONE。

 

 




