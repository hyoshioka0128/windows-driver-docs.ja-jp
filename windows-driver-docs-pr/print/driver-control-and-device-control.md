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
ms.openlocfilehash: eca096b1cd3598e2da5db8434a491f6db8d4efb5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387266"
---
# <a name="driver-control-and-device-control"></a>ドライバー コントロールとデバイス コントロール





色の管理が指定されている場合、いずれかのドライバーまたはプリンターのハードウェア、ドライバーの[プリンター グラフィックス DLL](printer-graphics-dll.md) 、GCAPS を設定する必要があります\_ICM フラグ、 [ **DEVINFO**](https://msdn.microsoft.com/library/windows/hardware/ff552835)構造体。

ドライバーは CYMK 色空間 (該当する場合)、「」のサポートを指定する必要があります[CMYK カラー領域をサポートしている](supporting-cmyk-color-space.md)します。

プリンター グラフィックス Dll には、次の 3 つの関数を定義する必要があります。

[**DrvIcmCreateColorTransform**](https://msdn.microsoft.com/library/windows/hardware/ff556239)

[**DrvIcmDeleteColorTransform**](https://msdn.microsoft.com/library/windows/hardware/ff556241)

[**DrvIcmCheckBitmapBits**](https://msdn.microsoft.com/library/windows/hardware/ff556238)

GDI の呼び出し、 [ **DrvIcmCreateColorTransform** ](https://msdn.microsoft.com/library/windows/hardware/ff556239) ICC プロファイルが (Microsoft Windows SDK のドキュメントで説明) を使用した印刷ジョブのドライバーを指定する関数。 関数は、これらのプロファイルを指定するには、色の情報を修正するときに使用する、内部色変換を作成できます。 色の変換は、ドライバー固有、内部的に定義されている 1 つの色空間から別のマッピングです。 関数は、GDI を格納すると、変換にハンドルを返します。

内のフラグ、 [ **BRUSHOBJ** ](https://msdn.microsoft.com/library/windows/hardware/ff538261)と[ **XLATEOBJ** ](https://msdn.microsoft.com/library/windows/hardware/ff570634)構造体は、色の管理をシステムによって実行されているかどうかを示します (またはアプリケーションの場合) またはドライバー (またはデバイス)。 各ドライバー実装グラフィックスにこれらの構造体のいずれか (または両方) を受け取る DDI 描画関数、フラグをチェックする必要があります。 システムまたはアプリケーションでは、色の管理を処理することは現在場合、ドライバーまたはデバイスは許可されません。 ドライバーまたはデバイスの色の管理が有効になっている場合、グラフィックス DDI 関数を呼び出す必要があります[ **BRUSHOBJ\_hGetColorTransform** ](https://msdn.microsoft.com/library/windows/hardware/ff538262)または[ **XLATEOBJ\_hGetColorTransform** ](https://msdn.microsoft.com/library/windows/hardware/ff570639) (または両方) を使用する色変換を識別するハンドルを取得します。 ハンドルには、以前の呼び出しへの応答に、ドライバーが用意されているいずれかになります、 [ **DrvIcmCreateColorTransform** ](https://msdn.microsoft.com/library/windows/hardware/ff556239)関数。

### <a name="handling-proprietary-color-management"></a>独自の色の管理を処理します。

一部のデバイスでは、独自の色の管理または実行されます (いずれか、ドライバーによってハードウェアによって) ICM が有効になっているかどうかに関係なく。 このようなデバイス ドライバーがイメージを受信したデータは既に修正されている場合に実行する色補正することはできません。 場合、precorrected データを受信できます。

-   アプリケーションが色補正"DC"の外部イメージ (Microsoft Windows SDK のドキュメントを参照してください)。

-   色の管理は、システムによって処理されます。

これらのシナリオでは、両方、BR のいずれかの\_ホスト\_ICM フラグ、 **flColorType**のメンバー [ **BRUSHOBJ** ](https://msdn.microsoft.com/library/windows/hardware/ff538261)と、XO\_ホスト\_ICM フラグ、 **flXlate**のメンバー [ **XLATEOBJ** ](https://msdn.microsoft.com/library/windows/hardware/ff570634)が設定されます。 これらのフラグを設定する場合でも、 **dmICMMethod**のメンバー [ **DEVMODEW** ](https://msdn.microsoft.com/library/windows/hardware/ff552837)は DMICMMETHOD\_NONE。

 

 




