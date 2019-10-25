---
title: ビデオ キャプチャのプロパティ セット
description: ビデオ キャプチャのプロパティ セット
ms.assetid: 23f61735-ae04-4143-8bd5-b713a2ab0e90
keywords:
- ビデオキャプチャ WDK AVStream、プロパティセット
- ビデオをキャプチャする WDK AVStream、プロパティセット
- プロパティ設定 WDK ビデオキャプチャ
- ハードウェアプロパティの WDK ビデオキャプチャの設定
- ストリームプロパティの WDK ビデオキャプチャの設定
- 範囲 WDK ビデオキャプチャ
- 既定のビデオキャプチャプロパティは、WDK AVStream を設定します。
- キャプチャプロパティセット WDK ビデオキャプチャ
ms.date: 06/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: ae901aebc8986487c0550ff4d608e6153e01c640
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844931"
---
# <a name="video-capture-property-sets"></a>ビデオ キャプチャのプロパティ セット


ビデオキャプチャプロパティは、デバイスとストリームのグループ関連のプロパティを設定します。 可能な場合は常に、ミニドライバーヘッダーファイルで定義されている標準のプロパティセットを実装する必要があります *。* たとえば、 [kspropsetid\_Pin](kspropsetid-pin.md)や[PROPSETID\_アロケーター\_コントロール](propsetid-allocator-control.md)です。 標準プロパティセットの1つが同じ機能を提供する場合、ミニドライバーは新しいプロパティセットを定義しないようにする必要があります。

ユーザーモードアプリケーションは、通常、プロパティ設定を制御するために COM インターフェイスを呼び出します。 次に、COM インターフェイスは、Win32 **DeviceIoControl** API を使用してストリームとアダプターのプロパティセットをミニドライバーに送信し、受信します。 各プロパティセットの参照ページは、ユーザーモードアプリケーションがそのセットのカーネルストリームプロパティを制御するために呼び出す COM インターフェイスを記述します。

ミニドライバーが使用するカーネルストリーミングインターフェイス (AVStream または Stream クラス) に応じて、ミニドライバーは、サポートするビデオキャプチャのプロパティセットを指定します。 たとえば、ミニドライバーが AVStream インターフェイスを使用している場合は、 [**Ksk プロパティ\_SET**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_set)構造体にカプセル化された再帰型階層でそのプロパティを指定します。 ミニドライバーが Stream クラスインターフェイスを使用する場合は、そのプロパティを[**HW\_ストリーム\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_header)構造体で指定します。 Microsoft では、ミニドライバーが使用するカーネルストリーミングインターフェイスに関係なく、ドライバー開発者がミニドライバーでサポートするプロパティを指定するために使用できるいくつかのマクロを定義しています。

ミニドライバーが AVStream インターフェイスを使用している場合にプロパティとプロパティセットをサポートする方法の詳細については、 [Avstream フィルター中心のシミュレートされたキャプチャドライバー (Avssamp)](https://github.com/Microsoft/Windows-driver-samples/tree/master/avstream/avssamp)と Avstream のシミュレートされた[ハードウェアサンプルドライバー (avshws) を参照してください。](https://github.com/Microsoft/Windows-driver-samples/tree/master/avstream/avshws)GitHub の Windows ドライバーサンプルリポジトリのサンプルミニドライバー。

ミニドライバーで Stream クラスインターフェイスを使用する場合のプロパティとプロパティセットのサポート方法の詳細については、「[プロパティセットのサポート](supporting-property-sets.md)」を参照してください。

### <a name="hardware-and-stream-property-sets"></a>ハードウェアおよびストリームのプロパティセット

プロパティセットは、ハードウェアまたは特定のストリームのいずれかに属しているものとして分類されます。 ハードウェアプロパティセットはすべてのデバイスに適用され、すべてのストリームに影響します。 たとえば、カメラの配置に使用される[Propsetid\_VIDCAP\_CAMERACONTROL](propsetid-vidcap-cameracontrol.md)は、すべての出力ストリームに影響を与えるため、ハードウェアのプロパティセットとして分類されます。 1つの出力ストリームの圧縮動作を制御する[Propsetid\_VIDCAP\_VIDEOCOMPRESSION](propsetid-vidcap-videocompression.md)などの一部のプロパティセットは、特定のストリームへのインデックスを含むハードウェアプロパティセットとして実装されることに注意してください。 Pin が接続されていない場合は、ストリームのプロパティセットを使用できないため、このメソッドが必要です。 ハードウェアプロパティセットは常に使用できます。

次の表に、video capture ミニドライバーによって使用される主なプロパティセットを示します。 また、プロパティセットがビデオキャプチャハードウェアまたは個々のビデオキャプチャストリームに影響を与えるかどうかも示します。 この一覧には、プロパティセットを実装するためにミニドライバーが必要かどうかも示されます。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>プロパティセット</th>
<th>ハードウェアプロパティセット</th>
<th>ビデオキャプチャのプロパティセット</th>
<th>必須かどうか</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="propsetid-allocator-control.md" data-raw-source="[PROPSETID_ALLOCATOR_CONTROL](propsetid-allocator-control.md)">PROPSETID_ALLOCATOR_CONTROL</a></p></td>
<td></td>
<td><p>Y</p></td>
<td></td>
</tr>
<tr class="even">
<td><p><a href="propsetid-tuner.md" data-raw-source="[PROPSETID_TUNER](propsetid-tuner.md)">PROPSETID_TUNER</a></p></td>
<td><p>Y</p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p><a href="propsetid-vidcap-cameracontrol.md" data-raw-source="[PROPSETID_VIDCAP_CAMERACONTROL](propsetid-vidcap-cameracontrol.md)">PROPSETID_VIDCAP_CAMERACONTROL</a></p></td>
<td><p>Y</p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p><a href="propsetid-vidcap-crossbar.md" data-raw-source="[PROPSETID_VIDCAP_CROSSBAR](propsetid-vidcap-crossbar.md)">PROPSETID_VIDCAP_CROSSBAR</a></p></td>
<td><p>Y</p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p><a href="propsetid-vidcap-droppedframes.md" data-raw-source="[PROPSETID_VIDCAP_DROPPEDFRAMES](propsetid-vidcap-droppedframes.md)">PROPSETID_VIDCAP_DROPPEDFRAMES</a></p></td>
<td></td>
<td><p>Y</p></td>
<td><p>Y</p></td>
</tr>
<tr class="even">
<td><p><a href="propsetid-vidcap-tvaudio.md" data-raw-source="[PROPSETID_VIDCAP_TVAUDIO](propsetid-vidcap-tvaudio.md)">PROPSETID_VIDCAP_TVAUDIO</a></p></td>
<td><p>Y</p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p><a href="propsetid-vidcap-videocompression.md" data-raw-source="[PROPSETID_VIDCAP_VIDEOCOMPRESSION](propsetid-vidcap-videocompression.md)">PROPSETID_VIDCAP_VIDEOCOMPRESSION</a></p></td>
<td><p>Y</p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p><a href="propsetid-vidcap-videocontrol.md" data-raw-source="[PROPSETID_VIDCAP_VIDEOCONTROL](propsetid-vidcap-videocontrol.md)">PROPSETID_VIDCAP_VIDEOCONTROL</a></p></td>
<td><p>Y</p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p><a href="propsetid-vidcap-videodecoder.md" data-raw-source="[PROPSETID_VIDCAP_VIDEODECODER](propsetid-vidcap-videodecoder.md)">PROPSETID_VIDCAP_VIDEODECODER</a></p></td>
<td><p>Y</p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p><a href="propsetid-vidcap-videoprocamp.md" data-raw-source="[PROPSETID_VIDCAP_VIDEOPROCAMP](propsetid-vidcap-videoprocamp.md)">PROPSETID_VIDCAP_VIDEOPROCAMP</a></p></td>
<td><p>Y</p></td>
<td></td>
<td></td>
</tr>
</tbody>
</table>

 

少なくとも、ミニドライバーは、上の表に示されているように、キャプチャ中に削除されたフレーム数を報告する必要があります。 その他のすべてのプロパティセットのサポートは、デバイスの機能によっては省略可能です。 カメラでは、キャプチャフレームレートの限られたセットのみを提供し、 [Propsetid\_VIDCAP\_VIDEOCONTROL](propsetid-vidcap-videocontrol.md)を実装して、ビデオ会議アプリケーションがシステム帯域幅を最適に使用できるようにすることを強くお勧めします。

### <a name="property-set-default-values-and-ranges"></a>プロパティ設定の既定値と範囲

プロパティは、既定値と範囲をサポートできます。 次の図に示すように、スライダーやスクロールバーなどのユーザーインターフェイス要素は、この情報を使用します。

![スライダーやスクロールバーなどのユーザーインターフェイス要素が既定値と範囲を使用する方法を示す [プロパティ] ダイアログボックスのスクリーンショット](images/vcuiprop.gif)

既定値と範囲の情報は、プロパティ定義の一部である[**Ksk プロパティ\_値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_values)の構造体で提供されます。 この構造体には、1つ以上の[**Ksk プロパティ\_memberslist**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_memberslist)構造体インスタンスで構成される静的テーブルへのポインターが含まれます。 ミニドライバーでは、KSK プロパティ\_MEMBERSLIST 構造体で、既定値または値の範囲のいずれかを指定できます。 値の範囲は、最小値、最大値、およびステップごとの値を使用して指定できます。 の**Membersflags**メンバーを[ **\_membersflags**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_membersheader)構造体を ksk プロパティ\_メンバー\_範囲の値に設定します。これにより、ksproperty\_membervalues 構造体が値の範囲であることを示します。 また、プロパティの既定値を指定するために、\_MEMBERSLIST 構造体を使用する KSK プロパティも使用されます。 これは、KSK プロパティの**Membersflags**メンバーを\_MEMBERSFLAGS に設定することにより、\_メンバー\_値の値に設定されます。

 

 




