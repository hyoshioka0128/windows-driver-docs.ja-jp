---
title: DitherOnRealize フラグのサポート
description: DitherOnRealize フラグのサポート
ms.assetid: 2a480045-ed2e-4650-80a4-a374f0388591
keywords:
- ディスプレイ ドライバー WDK Windows 2000 では、ディザリング
- DrvDitherColor
- ディザー WDK Windows 2000 の表示
- ディザリング WDK Windows 2000 の表示の色
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f58ecc950acff5fe717fc9f544d42ea91dd6641b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361228"
---
# <a name="supporting-the-ditheronrealize-flag"></a>DitherOnRealize フラグのサポート


## <span id="ddk_supporting_the_ditheronrealize_flag_gg"></span><span id="DDK_SUPPORTING_THE_DITHERONREALIZE_FLAG_GG"></span>


GDI とグラフィックス DDI の以前のバージョン、GDI によってドライバー関数を表示する 2 つの呼び出しがディザー指定した色と、その色のブラシにする必要です。 たとえば、アプリケーションでは、ディザリングされた色で四角形を入力することを要求、GDI 通常呼び出し[ **DrvBitBlt**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvbitblt)、四角形を使用するブラシ オブジェクトのエクステントを渡します。 ブラシを確認します。、実現されていないと、で GDI を呼び出して、検索し、ディスプレイ ドライバー [ **BRUSHOBJ\_pvGetRbrush** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-brushobj_pvgetrbrush)ブラシの GDI の実現にします。 GDI のディザリングの最初のアプリケーションに指定された RGB に渡します、GDI ではない、ディスプレイ ドライバーは、ブラシのディザリングを実行するため、 [ **DrvDitherColor** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdithercolor)ディスプレイ ドライバーにコールバックします。

*DrvDitherColor* GDI に指定された色のディザー情報を記述するカラー インデックスの配列へのポインターを返します。 呼び出しで、ディスプレイ ドライバーに、このディザー情報を即座に渡されます GDI [ **DrvRealizeBrush**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvrealizebrush)します。 [ **BRUSHOBJ** ](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_brushobj)が実際に制御が戻ります GDI に返送され、その後、元に戻す*DrvBitBlt*関数。

上記の手法を使用してディザリングを実現する GDI を呼び出す必要があります*DrvDitherColor*への呼び出しですぐにその後に、 *DrvRealizeBrush* -2 つの個別の関数呼び出し。 設定、GCAPS\_DITHERONREALIZE フラグ、 [ **DEVINFO** ](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-tagdevinfo)構造と変更*DrvRealizeBrush*これら 2 つの関数を効果的に結合するには別個の呼び出しをする必要がなくなります*DrvDitherColor*もいくつかのメモリ割り当てを保存します。 ディスプレイ ドライバー GCAPS を設定する場合、このスキームで\_DITHERONREALIZE、GDI 呼び出す*DrvRealizeBrush*滑らかに RGB と、RB\_DITHERCOLOR フラグを設定*iHatch*. RB\_DITHERCOLOR フラグの高位バイトに設定されて*iHatch*、滑らかに RGB 色は、次の 3 つの下位バイトに含まれています。 呼び出す必要*DrvDitherColor*両方の呼び出しの機能が 1 つに切り替わるため、このような状況では除去します。

コード例を参照してください、 *Permedia*ディスプレイ ドライバーのサンプルです。

**注**   3 dlabs permedia2 チップが、Microsoft Windows Driver Kit (WDK) に含まれていない (*3dlabs.htm*) と 3 dlabs Permedia3 (*Perm3.htm*) ディスプレイ ドライバーのサンプルです。 これらのサンプル ドライバーから、Windows Server 2003 SP1 ドライバー開発キット (DDK)、DDK - WDHC web サイトの Windows ドライバー開発キットのページからダウンロード可能を取得できます。

 

 

 





