---
title: ビデオ キャプチャ ミニドライバーのプロパティ セット
description: ビデオ キャプチャ ミニドライバーのプロパティ セット
ms.assetid: adbf62c4-1c66-46e9-ae8e-867a88bb107c
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f82ee31d07d3d901c8c33dcd0081343212527b8c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385387"
---
# <a name="video-capture-minidriver-property-sets"></a>ビデオ キャプチャ ミニドライバーのプロパティ セット


## <span id="ddk_video_capture_minidriver_property_sets_ks"></span><span id="DDK_VIDEO_CAPTURE_MINIDRIVER_PROPERTY_SETS_KS"></span>


このセクションには、Microsoft Windows XP、Windows 2000、および Windows 98 で WDM カーネル ストリーミング サービスを使用するビデオ キャプチャ ミニドライバーで利用可能なビデオのキャプチャに固有のプロパティ セットがについて説明します/と以降のオペレーティング システム。

各プロパティのリファレンス ページには、次の列見出しのテーブルが含まれています。


| 取得 | 設定 | 対象 | プロパティ記述子の型 | プロパティ値の型 |
|-----|-----|--------|--------------------------|---------------------|
|     |     |        |                          |                     |

これらの見出しには、次の意味があります。

-   **取得**

    KS ターゲット オブジェクトのサポート、KSPROPERTY\_型\_プロパティの GET 要求ですか?

-   **設定**

    KS ターゲット オブジェクトのサポート、KSPROPERTY\_型\_セット プロパティ要求でしょうか。

-   **移行先**

    ターゲットは、要求が送信されるどのプロパティに KS オブジェクトです。 ビデオ キャプチャ プロパティの対象は、フィルターまたは pin のいずれかです。 (プロパティ要求を指定します、ターゲット オブジェクトがカーネル ハンドルによって。)

-   **プロパティ記述子の型**

    プロパティ記述子には、プロパティとそのプロパティに対して実行する操作を指定します。 記述子が常に始まり、 [ **KSPROPERTY** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)構造がいくつかの型記述子の追加情報を格納します。 たとえば、 [ **KSNODEPROPERTY** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty)構造体は、プロパティ記述子を KSPROPERTY 構造で始まりますが、ノード識別子も含まれています。

-   **プロパティ値の型**

    プロパティの値を持つし、この値の型は、プロパティによって異なります。 たとえば、オンまたはオフ----だけ 2 つの状態のいずれかの可能性のあるプロパティには、ブール値通常があります。 ULONG 値 0x0 からの整数値を 0 xffffffff にことが前提としているプロパティがあります。 複雑なプロパティは、配列や構造体の値があります。

プロパティ記述子と上記のプロパティ値は、インスタンス仕様のプロパティに固有のバージョンおよび操作データをバッファーする[KS プロパティ、イベント、およびメソッド](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-properties--events--and-methods)について説明します。

プロパティ要求では、次のフラグのいずれかを使用して、プロパティに対して実行する操作を指定します。

-   KSPROPERTY\_型\_BASICSUPPORT

-   KSPROPERTY\_型\_取得

-   KSPROPERTY\_型\_設定

フィルターと暗証番号 (pin) のすべてのオブジェクトは、それらのプロパティを basic サポート操作をサポートします。 サポートされるかどうか、*取得*と*設定*操作は、プロパティによって異なります。 フィルターまたは pin オブジェクトの固有の機能を表すプロパティは、get 操作のみを必要とする可能性があります。 構成可能な設定を表すプロパティがありますのみが必要です、*設定*操作が、get 操作が現在の設定を読み取るために役立つ可能性も。 ビデオ キャプチャ プロパティで、get、セット、および操作を basic サポートを使用する方法の詳細については、次を参照してください。 [KS プロパティ](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-properties)します。

すべてのプロパティの説明には、ビデオ キャプチャ ミニドライバーが読み取りまたは書き込みのプロパティをサポートする必要があるかどうかを示すテーブルが含まれています。 ビデオ キャプチャ ミニドライバーは、状態を返す必要があります\_いない\_を取得または設定、ミニドライバーでサポートされていないプロパティに対する要求の応答ではサポートされています。

次の一覧には、カーネルがストリーミング ビデオ キャプチャ ミニドライバーを使用するプロパティ セットについて説明します。

[PROPSETID\_アロケーター\_コントロール](propsetid-allocator-control.md)

[PROPSETID\_EXT\_デバイス](propsetid-ext-device.md)

[PROPSETID\_EXT\_トランスポート](propsetid-ext-transport.md)

[PROPSETID\_タイムコード\_リーダー](propsetid-timecode-reader.md)

[PROPSETID\_チューナー](propsetid-tuner.md)

[PROPSETID\_しました\_CAMERACONTROL](propsetid-vidcap-cameracontrol.md)

[KSPROPERTYSETID\_ExtendedCameraControl](kspropertysetid-extendedcameracontrol.md)

[PROPSETID\_しました\_クロスバー](propsetid-vidcap-crossbar.md)

[PROPSETID\_VIDCAP\_DROPPEDFRAMES](propsetid-vidcap-droppedframes.md)

[PROPSETID\_VIDCAP\_TVAUDIO](propsetid-vidcap-tvaudio.md)

[PROPSETID\_しました\_VIDEOCOMPRESSION](propsetid-vidcap-videocompression.md)

[PROPSETID\_しました\_VIDEOCONTROL](propsetid-vidcap-videocontrol.md)

[PROPSETID\_しました\_VIDEODECODER](propsetid-vidcap-videodecoder.md)

[PROPSETID\_VIDCAP\_VIDEOPROCAMP](propsetid-vidcap-videoprocamp.md)

次のプロパティのセットで使用できる、 [USB ビデオ クラス ドライバー](https://docs.microsoft.com/windows-hardware/drivers/stream/usb-video-class-driver):

[PROPSETID\_しました\_CAMERACONTROL](propsetid-vidcap-cameracontrol.md)

[KSPROPERTYSETID\_ExtendedCameraControl](kspropertysetid-extendedcameracontrol.md)

[PROPSETID\_VIDCAP\_VIDEOPROCAMP](propsetid-vidcap-videoprocamp.md)

[PROPSETID\_しました\_セレクター](propsetid-vidcap-selector.md)

 

 





