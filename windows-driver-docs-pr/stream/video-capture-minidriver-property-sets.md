---
title: ビデオ キャプチャ ミニドライバーのプロパティ セット
description: ビデオ キャプチャ ミニドライバーのプロパティ セット
ms.assetid: adbf62c4-1c66-46e9-ae8e-867a88bb107c
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a4ec95337d16e765de3a21982fc59b33cec735b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844972"
---
# <a name="video-capture-minidriver-property-sets"></a>ビデオ キャプチャ ミニドライバーのプロパティ セット


## <span id="ddk_video_capture_minidriver_property_sets_ks"></span><span id="DDK_VIDEO_CAPTURE_MINIDRIVER_PROPERTY_SETS_KS"></span>


このセクションでは、Microsoft Windows XP、Windows 2000、Windows 98/Me、およびそれ以降のオペレーティングシステムで WDM カーネルストリーミングサービスを使用するビデオキャプチャミニドライバーで使用できるビデオキャプチャ固有のプロパティセットについて説明します。

各プロパティの参照ページには、次の列見出しを持つテーブルが含まれています。


| [購入] | 設定 | 対象 | プロパティ記述子の型 | プロパティ値の型 |
|-----|-----|--------|--------------------------|---------------------|
|     |     |        |                          |                     |

これらの見出しの意味は次のとおりです。

-   **取得**

    ターゲットの KS オブジェクトは、プロパティの取得\_\_型の KSK プロパティをサポートしていますか?

-   **一連**

    ターゲットの KS オブジェクトでは、プロパティ\_型\_SET プロパティがサポートされているかどうかを確認できます。

-   **接続**

    ターゲットは、プロパティ要求が送信される KS オブジェクトです。 ビデオキャプチャプロパティのターゲットは、フィルターまたは pin です。 (プロパティ要求では、カーネルハンドルによってターゲットオブジェクトが指定されます)。

-   **プロパティ記述子の型**

    プロパティ記述子は、プロパティと、そのプロパティに対して実行する操作を指定します。 記述子は常に[**Ksk プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)構造で始まりますが、一部の種類の記述子には追加情報が含まれています。 たとえば、 [**KSNODEPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)構造体は、ksk プロパティ構造体で始まるプロパティ記述子ですが、ノード識別子も含まれています。

-   **プロパティ値の型**

    プロパティには値があり、この値の型はプロパティによって異なります。 たとえば、2つの状態 (on または off) のいずれかであるプロパティは、通常、ブール値を持ちます。 0x0 から0xFFFFFFFF の整数値を想定できるプロパティは、ULONG 値を持つ場合があります。 より複雑なプロパティには、配列または構造体の値が含まれる場合があります。

上記のプロパティ記述子とプロパティ値は、 [KS プロパティ、イベント、およびメソッド](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-properties--events--and-methods)によって説明されている、インスタンス仕様および操作データバッファーのプロパティ固有バージョンです。

プロパティ要求では、次のいずれかのフラグを使用して、プロパティに対して実行する操作を指定します。

-   KSPROPERTY\_TYPE\_BASICSUPPORT

-   KSK プロパティ\_TYPE\_GET

-   KSK プロパティ\_TYPE\_SET

すべてのフィルターオブジェクトとピンオブジェクトは、そのプロパティに対する基本サポート操作をサポートしています。 *Get*操作と*Set*操作をサポートするかどうかは、プロパティによって異なります。 Filter オブジェクトまたは pin オブジェクトの固有の機能を表すプロパティは、get 操作のみを必要とする可能性があります。 構成可能な設定を表すプロパティは、*設定*操作のみを必要とする場合がありますが、get 操作は現在の設定の読み取りにも便利な場合があります。 ビデオキャプチャのプロパティで get、set、および basic サポート操作を使用する方法の詳細については、「 [KS のプロパティ](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-properties)」を参照してください。

すべてのプロパティの説明には、ビデオキャプチャミニドライバーがプロパティの読み取りまたは書き込みをサポートする必要があるかどうかを示すテーブルが含まれています。 ビデオキャプチャミニドライバーは、ミニドライバーでサポートされていないプロパティの取得または設定要求に応答して、状態\_返され\_ないようにする必要があります。

次の一覧では、video capture ミニドライバーで使用されるカーネルストリーミングのプロパティセットについて説明します。

[PROPSETID\_アロケーター\_コントロール](propsetid-allocator-control.md)

[PROPSETID\_EXT\_デバイス](propsetid-ext-device.md)

[PROPSETID\_EXT\_TRANSPORT](propsetid-ext-transport.md)

[PROPSETID\_タイムコード\_リーダー](propsetid-timecode-reader.md)

[PROPSETID\_チューナー](propsetid-tuner.md)

[PROPSETID\_VIDCAP\_CAMERACONTROL](propsetid-vidcap-cameracontrol.md)

[KSK PROPERTYSETID\_ExtendedCameraControl](kspropertysetid-extendedcameracontrol.md)

[PROPSETID\_VIDCAP\_クロスバー](propsetid-vidcap-crossbar.md)

[PROPSETID\_VIDCAP\_DROPPEDFRAMES](propsetid-vidcap-droppedframes.md)

[PROPSETID\_VIDCAP\_TVAUDIO](propsetid-vidcap-tvaudio.md)

[PROPSETID\_VIDCAP\_VIDEOCOMPRESSION](propsetid-vidcap-videocompression.md)

[PROPSETID\_VIDCAP\_VIDEOCONTROL](propsetid-vidcap-videocontrol.md)

[PROPSETID\_VIDCAP\_VIDEODECODER](propsetid-vidcap-videodecoder.md)

[PROPSETID\_VIDCAP\_VIDEOPROCAMP](propsetid-vidcap-videoprocamp.md)

次のプロパティセットは、 [USB ビデオクラスドライバー](https://docs.microsoft.com/windows-hardware/drivers/stream/usb-video-class-driver)で使用できます。

[PROPSETID\_VIDCAP\_CAMERACONTROL](propsetid-vidcap-cameracontrol.md)

[KSK PROPERTYSETID\_ExtendedCameraControl](kspropertysetid-extendedcameracontrol.md)

[PROPSETID\_VIDCAP\_VIDEOPROCAMP](propsetid-vidcap-videoprocamp.md)

[PROPSETID\_VIDCAP\_SELECTOR](propsetid-vidcap-selector.md)

 

 





