---
title: PROPSETID\_しました\_ビデオ プロシージャ アンプ
description: PROPSETID\_しました\_ビデオ プロシージャ アンプ
ms.assetid: ea1d9c96-b1a5-4849-b607-4c508a526512
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5373370c0e7ce409577b4c8655466334ea04b4d2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385696"
---
# <a name="propsetidvidcapvideoprocamp"></a>PROPSETID\_しました\_ビデオ プロシージャ アンプ


## <span id="ddk_propsetid_vidcap_videoprocamp_ks"></span><span id="DDK_PROPSETID_VIDCAP_VIDEOPROCAMP_KS"></span>


PROPSETID\_しました\_ビデオ プロシージャ アンプ プロパティは、アナログまたはデジタル信号のイメージの色属性を調整できるコントロール デバイスを設定します。

KSPROPERTY\_しました\_でビデオ プロシージャ アンプ列挙*ksmedia.h*このセットのプロパティを指定します。

このプロパティ セットのサポートは省略可能で、明るさ、コントラスト、色合い、およびその他のイメージの調整の品質設定を許可しているデバイスでのみ実装する必要があります。

USB ビデオ クラスでは、前に、この列挙体には、以下プロパティにはが含まれています。

[**KSPROPERTY\_ビデオ プロシージャ アンプ\_バックライト\_補正**](ksproperty-videoprocamp-backlight-compensation.md)

[**KSPROPERTY\_ビデオ プロシージャ アンプ\_明るさ**](ksproperty-videoprocamp-brightness.md)

[**KSPROPERTY\_ビデオ プロシージャ アンプ\_COLORENABLE**](ksproperty-videoprocamp-colorenable.md)

[**KSPROPERTY\_ビデオ プロシージャ アンプ\_コントラスト**](ksproperty-videoprocamp-contrast.md)

[**KSPROPERTY\_ビデオ プロシージャ アンプ\_ガンマ**](ksproperty-videoprocamp-gamma.md)

[**KSPROPERTY\_ビデオ プロシージャ アンプ\_HUE**](ksproperty-videoprocamp-hue.md)

[**KSPROPERTY\_ビデオ プロシージャ アンプ\_彩度**](ksproperty-videoprocamp-saturation.md)

[**KSPROPERTY\_ビデオ プロシージャ アンプ\_鮮明度**](ksproperty-videoprocamp-sharpness.md)

[**KSPROPERTY\_ビデオ プロシージャ アンプ\_ホワイト バランス**](ksproperty-videoprocamp-whitebalance.md)

[**KSPROPERTY\_ビデオ プロシージャ アンプ\_を得る**](ksproperty-videoprocamp-gain.md)

導入に伴い、 [USB ビデオ クラス ドライバー](https://docs.microsoft.com/windows-hardware/drivers/stream/usb-video-class-driver)、次のプロパティは、KSPROPERTY に追加された\_しました\_ビデオ プロシージャ アンプ列挙体。

[**KSPROPERTY\_ビデオ プロシージャ アンプ\_デジタル\_乗数**](ksproperty-videoprocamp-digital-multiplier.md)

[**KSPROPERTY\_ビデオ プロシージャ アンプ\_デジタル\_乗数\_制限**](ksproperty-videoprocamp-digital-multiplier-limit.md)

[**KSPROPERTY\_ビデオ プロシージャ アンプ\_ホワイト バランス\_コンポーネント**](ksproperty-videoprocamp-whitebalance-component.md)

[**KSPROPERTY\_ビデオ プロシージャ アンプ\_POWERLINE\_頻度**](ksproperty-videoprocamp-powerline-frequency.md)

各プロパティで、PROPSETID\_ビデオ プロシージャ アンプ プロパティ セットには範囲と既定値が含まれています。 プロパティ セットの範囲は、パラメーターのプログラムによる制御を許可する実際の単位で定義されます。 各デバイスには、ステップのサイズと同様に、この範囲のサブセットを定義できます。 これにより、スライダーやスクロール バーの各ステップの表示に影響を与えるプログラムを作成するなどのコントロールです。

たとえば、明るさの全体的な理論上の範囲は 100 切る単位に-100 として定義されます。 切るは、NTSC 定義されているメジャーが 0 に、非対応、ビデオのレベルの完全な黒のレベルと 100 は、純粋な白を表します。 (おそらくはカメラのレンズを完全にカバーによって生成される)、純粋な黒入力信号をシフトして、純粋な空白として表示される、ビデオ プロシージャ アンプができたし、その範囲は 0 ~ 100 切るになります。

実際には、ほとんど VideoProcAmps は輝度の制限の範囲を提供します。 範囲を評価するための 1 つの方法では、カメラのレンズをカバーし調整の範囲で出力シグナルを特定し、これを切るユニットに正規化します。 ステップ実行の値を最大と最小値を取得し、調整ステップ数で除算することによって派生できる範囲が計算された後 **(最大 + 分)/N 調整手順**します。

プロパティ セットで使用される値はきめ細かさの向上に 100 を乗算することに注意してください。

### <a name="span-iddirectshowinterfacespanspan-iddirectshowinterfacespandirectshow-interface"></a><span id="directshow_interface"></span><span id="DIRECTSHOW_INTERFACE"></span>DirectShow インターフェイス

DirectShow **IAMVideoProcAmp**インターフェイスには、このセットのプロパティへのアクセスが用意されています (Microsoft Windows SDK の DirectShow のドキュメントを参照してください)。

 

 





