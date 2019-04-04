---
title: ビデオ キャプチャ プロパティ セット
description: ビデオ キャプチャ プロパティ セット
ms.assetid: 23f61735-ae04-4143-8bd5-b713a2ab0e90
keywords:
- WDK AVStream ビデオ キャプチャは、プロパティを設定します。
- ビデオの WDK AVStream をキャプチャするには、プロパティを設定します。
- プロパティは、WDK のビデオ キャプチャを設定します。
- ハードウェア プロパティは、WDK のビデオ キャプチャを設定します。
- ストリーム プロパティは、WDK のビデオ キャプチャを設定します。
- 範囲の WDK ビデオのキャプチャ
- 既定のビデオ キャプチャ プロパティは、WDK AVStream を設定します。
- プロパティ セットの WDK ビデオのキャプチャのキャプチャします。
ms.date: 06/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: e3f0fecbe54d01fbb80b6aa6a60e632ee47e4cbb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527690"
---
# <a name="video-capture-property-sets"></a>ビデオ キャプチャ プロパティ セット


ビデオ キャプチャ プロパティ セットのグループに関連するデバイスとストリームのプロパティを指定します。 可能であれば、ミニドライバーがで定義されている標準的なプロパティ セットを実装する必要があります、 *ksmedia.h*ヘッダー ファイルなど、 [KSPROPSETID\_Pin](kspropsetid-pin.md)と[PROPSETID\_アロケーター\_コントロール](propsetid-allocator-control.md)します。 ミニドライバーは、標準的なプロパティのいずれかは、同じ機能を提供します。 場合、新しいプロパティのセットを定義することを避ける必要があります。

通常、ユーザー モード アプリケーションは、プロパティの設定を制御する COM インターフェイスを呼び出します。 Win32 ミニドライバーにアダプターのプロパティを設定し、COM インターフェイス: 送信し、ストリームを受信する**DeviceIoControl** API。 各プロパティ セットのリファレンス ページには、そのセットのプロパティをストリーミングするカーネルを制御するユーザー モード アプリケーションを呼び出す COM インターフェイスについて説明します。

(AVStream または Stream クラス)、カーネルによって、ミニドライバーのストリーミング インターフェイスを使用する、ミニドライバーは、異なる方法でサポートしているビデオ キャプチャ プロパティの設定を指定します。 など、ミニドライバー AVStream インターフェイスを使用する場合そのプロパティを指定でカプセル化されている再帰型階層、 [ **KSPROPERTY\_設定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksproperty_set)構造体。 かどうか、ミニドライバーは、Stream クラス インターフェイスを使用して、そのプロパティを指定します、 [ **HW\_ストリーム\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/ns-strmini-_hw_stream_header)構造体。 Microsoft では、ストリーミング インターフェイスのミニドライバーを使用して、カーネルに関係なく、ミニドライバーでサポートされるプロパティを指定するドライバー開発者が使用できるいくつかのマクロを定義します。

ミニドライバーは AVStream インターフェイスを使用している場合、プロパティおよびプロパティ セットをサポートする方法の詳細については、次を参照してください、 [AVStream フィルターを中心としたシミュレートされたキャプチャ ドライバー (Avssamp)](https://github.com/Microsoft/Windows-driver-samples/tree/master/avstream/avssamp)と[AVStream のシミュレート。ハードウェア サンプル ドライバー (AVSHwS)](https://github.com/Microsoft/Windows-driver-samples/tree/master/avstream/avshws)ミニドライバーで GitHub の Windows ドライバーのサンプル リポジトリのサンプルです。

ミニドライバーは、Stream クラス インターフェイスを使用している場合、プロパティおよびプロパティ セットをサポートする方法の詳細については、[プロパティの設定をサポートしている](supporting-property-sets.md)を参照してください。

### <a name="hardware-and-stream-property-sets"></a>ハードウェアと Stream プロパティ セット

プロパティ セットは、ハードウェアのいずれかに属するものとして、または特定のストリームに分類されます。 ハードウェア プロパティのセットは、すべてのデバイスに適用され、すべてのストリームに影響を与えます。 たとえば、 [PROPSETID\_しました\_CAMERACONTROL](propsetid-vidcap-cameracontrol.md)カメラの位置に使用されるすべての出力ストリームに影響し、そのため、ハードウェア プロパティのセットとして分類されています。 などのいくつかのプロパティ セット[PROPSETID\_しました\_VIDEOCOMPRESSION](propsetid-vidcap-videocompression.md)が含まれるハードウェア プロパティのセットとして実装されますが、1 つの出力ストリームの圧縮動作を制御します。特定のストリーム インデックス。 Pin が接続されていないストリーム プロパティ セットは利用できないために、このメソッドが必要です。 ハードウェア プロパティのセットでは、使用可能な常にします。

次の表は、ビデオ キャプチャ ミニドライバーで使用されるプライマリ プロパティ セットを一覧表示します。 プロパティは設定に影響するかどうかも示しますビデオ キャプチャ ハードウェア、または個々 のビデオ キャプチャ ストリーム。 この一覧は、ミニドライバーがプロパティ セットを実装するために必要かどうかも示します。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>プロパティ セット</th>
<th>ハードウェアのプロパティ セット</th>
<th>ビデオ キャプチャ プロパティ セット</th>
<th>必須</th>
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

 

少なくとも、ミニドライバーは、上記の表で説明したように、キャプチャ中にドロップしたフレームの数を報告する必要があります。 他のすべてのプロパティ セットのサポートは、デバイスの機能に応じて、省略可能です。 フレーム レートのキャプチャの制限のセットのみを提供のカメラが実装することを強くお勧め、 [PROPSETID\_しました\_VIDEOCONTROL](propsetid-vidcap-videocontrol.md)に最適なビデオ会議アプリケーションを許可するにはシステムの帯域幅の使用。

### <a name="property-set-default-values-and-ranges"></a>プロパティは、既定値と範囲を設定

プロパティには、既定値と範囲をサポートできます。 スクロール バー、スライダーなどのユーザー インターフェイス要素は、次の図のように、この情報を使用します。

![スクロール バー、スライダーなどのユーザー インターフェイス要素が既定値と範囲を使用する方法を示すプロパティ ダイアログ ボックスのスクリーン ショット](images/vcuiprop.gif)

既定値と範囲情報が表示されます、 [ **KSPROPERTY\_値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksproperty_values)プロパティ定義の一部を表す構造体します。 この構造体には、1 つまたは複数で構成される静的なテーブルへのポインターが含まれています。 [ **KSPROPERTY\_MEMBERSLIST** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksproperty_memberslist)インスタンス構造体。 KSPROPERTY 内\_MEMBERSLIST 構造体、ミニドライバーは、既定値または値の範囲のいずれかを指定できます。 値の範囲は、最小、最大、およびステップ実行の値を使用して指定できます。 設定、 **MembersFlags**のメンバー、 [ **KSPROPERTY\_MEMBERSHEADER** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksproperty_membersheader)構造体を KSPROPERTY\_メンバー\_いることを示す値の範囲は、KSPROPERTY\_MEMBERSLIST 構造体は値の範囲。 KSPROPERTY\_MEMBERSLIST 構造は、プロパティの既定値を指定するも使用されます。 これは、設定で、 **MembersFlags** 、KSPROPERTY のメンバー\_、KSPROPERTY に MEMBERSHEADER\_メンバー\_値を追加します。

 

 




