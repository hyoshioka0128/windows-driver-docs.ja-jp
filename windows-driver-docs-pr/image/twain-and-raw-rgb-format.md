---
title: TWAIN および RGB の生の形式
description: TWAIN および RGB の生の形式
ms.assetid: 0de4a547-6c8e-4fbf-a7a3-7af440bf72f3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d691b11c1ff1c842d0c53606f8a36114233655e1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557788"
---
# <a name="twain-and-raw-rgb-format"></a>TWAIN および RGB の生の形式





ときに、アプリケーションは、イメージ形式の GUID が WiaImgFmt\_RAWRGB (ヘッダー ファイルで定義されている*wiadef.h*)、イメージには、次のプロパティは、イメージの正しい値を含める必要があります。

-   WIA\_IPA\_チャネル\_1 秒あたり\_ピクセル

-   WIA\_IPA\_ビット\_1 秒あたり\_チャネル

-   WIA\_IPA\_ピクセル\_1 秒あたり\_行

-   WIA\_IPA\_数\_の\_行

-   WIA\_IP\_XRES

-   WIA\_IP\_YRES

さらに、WIA\_IPA\_WIA に DATATYPE プロパティを設定する必要があります\_データ\_色と、WIA\_IPA\_以上 24 に、DEPTH プロパティを設定する必要があります。 これらのプロパティの詳細については、Microsoft Windows SDK のドキュメントを参照してください。

転送される生の RGB 形式のデータがある必要があります。

-   圧縮されていません。

-   RGB のバイト順で並べ替え

-   DWORD の境界にアラインされます。

イメージ ヘッダーなしでは、データを転送する必要があります。 **IWiaDataCallback::BandedDataCallback**メソッド (Windows SDK のドキュメントで説明) イメージ ビットのみを送信します。

TWAIN 互換レイヤー (を参照してください[TWAIN と互換性のあるアプリケーションのサポート](support-for-twain-compatible-applications.md)) サポート、WiaImgFmt\_RAWRGB 形式の GUID。 これによりメモリ コールバック転送を使用して、32 ビットを超えるピクセル深度でイメージを転送する TWAIN アプリケーション。

 

 




