---
title: エンコーダーの実装とサポート
description: エンコーダーの実装とサポート
ms.assetid: 6ba97ff8-815b-490f-920b-6ede4f730e98
keywords:
- エンコーダーデバイス WDK AVStream
- AVStream WDK、エンコーダーデバイス
- 非圧縮データストリーム WDK AVStream
- エンコードされたストリーム WDK AVStream
- オーディオエンコーダーデバイス WDK AVStream
- ビデオエンコーダーデバイス WDK AVStream
- プロパティ設定 WDK encoder
- ENCAPIPARAM_BITRATE_MODE
- ENCAPIPARAM_BITRATE
- ENCAPIPARAM_PEAK_BITRATE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ddaaeb62464f1170a481d62a0ca4f4d3eff90b62
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834477"
---
# <a name="encoder-implementation-and-support"></a>エンコーダーの実装とサポート

Windows XP Service Pack 1 では、ビデオのみのエンコーダーデバイスをサポートするために、Microsoft によって、3つのカーネルストリーミングプロパティセットと、 *ksmedia. h*内の1つの列挙が定義されています。 各プロパティセットには、1つのプロパティが含まれます。 言い換えると、各プロパティは独自のプロパティセットを受け取ります。 ドライバーで*get*プロパティまたは*set*プロパティの呼び出しを行う場合は、 [**Ksk プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)構造体の**set**メンバーでプロパティセットの GUID を指定し*ます (ksk*で定義されているように) 。次の呼び出しが実行されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>プロパティ セット</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/encapiparam-bitrate" data-raw-source="[ENCAPIPARAM_BITRATE](https://docs.microsoft.com/windows-hardware/drivers/stream/encapiparam-bitrate)">ENCAPIPARAM_BITRATE</a></td>
<td><p>エンコーダーデバイスでサポートされるエンコーディングビットレートを指定するには、このプロパティを設定します。 詳細については、「<a href="encoder-code-examples.md" data-raw-source="[Encoder Code Examples](encoder-code-examples.md)">エンコーダーのコード例</a>」を参照してください。</p></td>
</tr>
<tr class="even">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/encapiparam-bitrate-mode" data-raw-source="[ENCAPIPARAM_BITRATE_MODE](https://docs.microsoft.com/windows-hardware/drivers/stream/encapiparam-bitrate-mode)">ENCAPIPARAM_BITRATE_MODE</a></td>
<td><p>デバイスでサポートされているエンコードモードを指定するには、このプロパティを設定します。 このプロパティセットは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-videoencoder_bitrate_mode" data-raw-source="[&lt;strong&gt;VIDEOENCODER_BITRATE_MODE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-videoencoder_bitrate_mode)"><strong>VIDEOENCODER_BITRATE_MODE</strong></a>列挙体を使用して、サポートされているモードを指定します。 詳細については、「<a href="encoder-code-examples.md" data-raw-source="[Encoder Code Examples](encoder-code-examples.md)">エンコーダーのコード例</a>」を参照してください。</p></td>
</tr>
<tr class="odd">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/encapiparam-peak-bitrate" data-raw-source="[ENCAPIPARAM_PEAK_BITRATE](https://docs.microsoft.com/windows-hardware/drivers/stream/encapiparam-peak-bitrate)">ENCAPIPARAM_PEAK_BITRATE</a></td>
<td><p>デバイスのエンコードビットレートの最大値を指定するには、このプロパティを設定します。</p></td>
</tr>
</tbody>
</table>

クライアントは、 **IEncoderAPI** com インターフェイス (Windows Software Development KIT (SDK) のドキュメントで説明されています) から**ivideoencoder** com インターフェイスを派生させることによって、これらのプロパティにアクセスします。

ミニドライバーでは、ENCAPIPARAM\_*Xxx*の各プロパティに既定値を指定する必要があります。 「[エンコーダーのコード例](encoder-code-examples.md)」では、既定のプロパティ値を指定する方法を示しています。 エンコーダーフィルターの開発時およびデバッグ時に、ENCAPIPARAM\_ビットレートプロパティセットをサポートするミニドライバーから現在のプロパティページをトリガーできます。

DirectX 9.0 では、6つの追加のプロパティセットと1つのイベントセットが*ksmedia. h*で定義されています。これにより、オーディオ専用エンコーダーを含むさまざまなエンコーダーのサポートが向上します。 ENCAPIPARAM\_*Xxx*プロパティと同様に、各プロパティは独自のプロパティセットを受け取ります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>プロパティ セット</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/codecapi-video-encoder" data-raw-source="[CODECAPI_VIDEO_ENCODER](https://docs.microsoft.com/windows-hardware/drivers/stream/codecapi-video-encoder)">CODECAPI_VIDEO_ENCODER</a></td>
<td><p>デバイスがビデオストリームのエンコード (TV オーディオなどの補助オーディオを含む) をサポートしている場合は、このプロパティセットのサポートを実装します。</p></td>
</tr>
<tr class="even">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/codecapi-audio-encoder" data-raw-source="[CODECAPI_AUDIO_ENCODER](https://docs.microsoft.com/windows-hardware/drivers/stream/codecapi-audio-encoder)">CODECAPI_AUDIO_ENCODER</a></td>
<td><p>デバイスがオーディオ専用エンコーダーの場合は、CODECAPI_VIDEO_ENCODER ではなく、このプロパティセットのサポートを実装します。</p></td>
</tr>
<tr class="odd">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/codecapi-setalldefaults" data-raw-source="[CODECAPI_SETALLDEFAULTS](https://docs.microsoft.com/windows-hardware/drivers/stream/codecapi-setalldefaults)">CODECAPI_SETALLDEFAULTS</a></td>
<td><p>このプロパティセットを実装して、エンコーディングのビットレートやエンコードモードなどのすべてのエンコーダーデバイスの内部設定を既定値にリセットします。</p></td>
</tr>
<tr class="even">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/codecapi-allsettings" data-raw-source="[CODECAPI_ALLSETTINGS](https://docs.microsoft.com/windows-hardware/drivers/stream/codecapi-allsettings)">CODECAPI_ALLSETTINGS</a></td>
<td><p>エンコーダーデバイスの現在の設定を伝達するには、このプロパティセットを実装します。 このプロパティセットは、クライアントとの通信に使用されます。</p></td>
</tr>
<tr class="odd">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/codecapi-supportsevents" data-raw-source="[CODECAPI_SUPPORTSEVENTS](https://docs.microsoft.com/windows-hardware/drivers/stream/codecapi-supportsevents)">CODECAPI_SUPPORTSEVENTS</a></td>
<td><p>エンコードモードやビットレートなどの設定を変更する場合など、ユーザーモードからのイベントがデバイスでサポートされている場合は、このプロパティセットを実装します。 このプロパティセットを実装する場合は、CODECAPI_CHANGELISTS イベントのサポートも実装する必要があります。</p></td>
</tr>
<tr class="even">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/codecapi-currentchangelist" data-raw-source="[CODECAPI_CURRENTCHANGELIST](https://docs.microsoft.com/windows-hardware/drivers/stream/codecapi-currentchangelist)">CODECAPI_CURRENTCHANGELIST</a></td>
<td><p>このプロパティを設定して、前の呼び出しで変更されたエンコーダーパラメーターを特定し、1つ以上のエンコーダープロパティを設定します。</p></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>イベントセット</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/codecapi-changelists" data-raw-source="[CODECAPI_CHANGELISTS](https://docs.microsoft.com/windows-hardware/drivers/stream/codecapi-changelists)">CODECAPI_CHANGELISTS</a></p></td>
<td><p>デバイスが CODECAPI_SUPPORTSEVENTS プロパティセットを使用してユーザーモードイベントへの応答をサポートしている場合は、このイベントセットを実装して、クライアントの以前の<em>セット</em>プロパティ呼び出しの結果として変更されたエンコーダー設定の一覧を返します。CODECAPI_SETALLDEFAULTS または CODECAPI_ALLSETTINGS。</p></td>
</tr>
</tbody>
</table>

クライアントは、 **ICodecAPI** COM インターフェイス (Windows SDK のドキュメントで説明) を使用してこれらのプロパティにアクセスします。 COM インターフェイスの詳細については、「[エンコーダーのインストールと登録](encoder-installation-and-registration.md)」を参照してください。これには、ksk プロキシで公開する必要があるインターフェイスを指定する方法も含まれます。

ミニドライバーは、基本の*get*プロパティクエリのサポートを実装する必要があります。 「[エンコーダーのコード例](encoder-code-examples.md)」では、 *get*プロパティクエリをサポートする方法を示しています。

エンコーダーフィルターを開発するときに、エンコード機能をビデオキャプチャフィルターから別のフィルターに移動します。 独自のプライベートメディアを定義して、グラフビルダーがエンコーダーとキャプチャフィルターを正しく接続できるようにします。 ハードウェアが、エンコードされていないコンテンツをバスマスタリングできる場合は、パブリックメディアを公開することもできます。 パブリックとプライベートの両方のメディアを実装する場合は、グラフの構築時間が短縮されるため、プライベートメディアを最初にリストします。フィルターグラフを作成するときに、適切なフィルターを検索します。

複数のフィルター (個別のフィルターグラフ) のメディアおよび複数インスタンスの使用の詳細については[、「メディアとカテゴリ](mediums-and-categories.md)」を参照してください。
