---
title: エンコーダーの実装とサポート
description: エンコーダーの実装とサポート
ms.assetid: 6ba97ff8-815b-490f-920b-6ede4f730e98
keywords:
- エンコーダー デバイス WDK AVStream
- AVStream WDK、エンコーダーのデバイス
- 非圧縮データ ストリームの WDK AVStream
- エンコードされたストリーム WDK AVStream
- オーディオ エンコーダー デバイス WDK AVStream
- ビデオ エンコーダー デバイス WDK AVStream
- プロパティ セットの WDK エンコーダー
- ENCAPIPARAM_BITRATE_MODE
- ENCAPIPARAM_BITRATE
- ENCAPIPARAM_PEAK_BITRATE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cd29935e2de3aae94f170c5b0fe3aaa64aa37f75
ms.sourcegitcommit: 56599ec634b3a731f2d13dff686be3b7b95390e4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2019
ms.locfileid: "58419566"
---
# <a name="encoder-implementation-and-support"></a>エンコーダーの実装とサポート

Windows XP Service Pack 1 で、Microsoft では、3 つのカーネル ストリーミング プロパティ セットとに 1 つの列挙が定義されている*ksmedia.h*ビデオのみのエンコーダーのデバイスをサポートします。 各プロパティ セットには、1 つのプロパティが含まれています。 つまり、各プロパティは、独自のプロパティ セットを受け取ります。 場合は、ドライバーによって*取得*-プロパティまたは*設定*-プロパティの呼び出し、プロパティ セットの GUID を指定し (で定義されている*ksmedia.h*) で、 **設定**のメンバー、 [ **KSPROPERTY** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)で 0 構造体であり、 **Id**メンバーの呼び出しを設定する場合。

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
<td><a href="https://msdn.microsoft.com/library/windows/hardware/ff559520" data-raw-source="[ENCAPIPARAM_BITRATE](https://msdn.microsoft.com/library/windows/hardware/ff559520)">ENCAPIPARAM_BITRATE</a></td>
<td><p>実装する、エンコーディングを指定するには、このプロパティ セットのビット レートのエンコーダーのデバイスでサポートされています。 参照してください<a href="encoder-code-examples.md" data-raw-source="[Encoder Code Examples](encoder-code-examples.md)">エンコーダーのコード例</a>の詳細。</p></td>
</tr>
<tr class="even">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/ff559524" data-raw-source="[ENCAPIPARAM_BITRATE_MODE](https://msdn.microsoft.com/library/windows/hardware/ff559524)">ENCAPIPARAM_BITRATE_MODE</a></td>
<td><p>このプロパティを設定すると、デバイスでサポートされているエンコード モードを実装します。 このプロパティの設定は、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff568695" data-raw-source="[&lt;strong&gt;VIDEOENCODER_BITRATE_MODE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568695)"> <strong>VIDEOENCODER_BITRATE_MODE</strong> </a>サポートされているモードを指定する列挙体。 参照してください<a href="encoder-code-examples.md" data-raw-source="[Encoder Code Examples](encoder-code-examples.md)">エンコーダーのコード例</a>の詳細。</p></td>
</tr>
<tr class="odd">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/ff559529" data-raw-source="[ENCAPIPARAM_PEAK_BITRATE](https://msdn.microsoft.com/library/windows/hardware/ff559529)">ENCAPIPARAM_PEAK_BITRATE</a></td>
<td><p>このプロパティを設定すると、デバイスの最大のエンコード ビット レートを実装します。</p></td>
</tr>
</tbody>
</table>

クライアントが派生することによってこれらのプロパティをアクセス、 **IVideoEncoder**から COM インターフェイス、 **IEncoderAPI** (、Windows ソフトウェア開発キット (SDK) ドキュメントに記載) COM インターフェイスです。

各、ENCAPIPARAM の既定値を指定する必要があります、ミニドライバー\_*Xxx*プロパティ。 トピック[エンコーダーのコード例](encoder-code-examples.md)既定のプロパティ値を指定する方法を示します。 開発とエンコーダー フィルターのデバッグ中に現在のプロパティ ページをサポートしている、ENCAPIPARAM ミニドライバーからトリガーできる\_ビットレート プロパティのセット。

DirectX 9.0、6 つの追加のプロパティ セットと 1 つのイベントのセットがで定義された*ksmedia.h*エンコーダー、オーディオのみのエンコーダーなどの各種の優れたサポートを提供します。 ENCAPIPARAM と同様\_*Xxx*プロパティ、各プロパティは、独自のプロパティ セットを受信します。

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
<td><a href="https://msdn.microsoft.com/library/windows/hardware/ff557705" data-raw-source="[CODECAPI_VIDEO_ENCODER](https://msdn.microsoft.com/library/windows/hardware/ff557705)">CODECAPI_VIDEO_ENCODER</a></td>
<td><p>デバイスは、エンコード ビデオ ストリーミングを (テレビ オーディオなどの補助的なオーディオを含む) をサポートしている場合は、このプロパティ セットのサポートを実装します。</p></td>
</tr>
<tr class="even">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/ff557693" data-raw-source="[CODECAPI_AUDIO_ENCODER](https://msdn.microsoft.com/library/windows/hardware/ff557693)">CODECAPI_AUDIO_ENCODER</a></td>
<td><p>デバイスがエンコーダーをオーディオのみの場合は、CODECAPI_VIDEO_ENCODER ではなく、このプロパティのサポートを実装します。</p></td>
</tr>
<tr class="odd">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/ff557702" data-raw-source="[CODECAPI_SETALLDEFAULTS](https://msdn.microsoft.com/library/windows/hardware/ff557702)">CODECAPI_SETALLDEFAULTS</a></td>
<td><p>このプロパティのエンコード ビット レートとモードを既定値をエンコードするなど、すべてのエンコーダー デバイスの内部設定をリセットする設定を実装します。</p></td>
</tr>
<tr class="even">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/ff557691" data-raw-source="[CODECAPI_ALLSETTINGS](https://msdn.microsoft.com/library/windows/hardware/ff557691)">CODECAPI_ALLSETTINGS</a></td>
<td><p>エンコーダーのデバイスの現在の設定を通信するためにこのプロパティを実装します。 このプロパティ セットは、クライアントとの間の通信に使用されます。</p></td>
</tr>
<tr class="odd">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/ff557703" data-raw-source="[CODECAPI_SUPPORTSEVENTS](https://msdn.microsoft.com/library/windows/hardware/ff557703)">CODECAPI_SUPPORTSEVENTS</a></td>
<td><p>デバイスは、エンコード モード、ビット レート、またはその他の設定を変更するなど、ユーザー モード - からイベントをサポートする場合は、このプロパティのセットを実装します。 このプロパティのセットを実装する場合、CODECAPI_CHANGELISTS イベントのサポートも実装する必要があります。</p></td>
</tr>
<tr class="even">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/ff557700" data-raw-source="[CODECAPI_CURRENTCHANGELIST](https://msdn.microsoft.com/library/windows/hardware/ff557700)">CODECAPI_CURRENTCHANGELIST</a></td>
<td><p>このプロパティがどのエンコーダー パラメーターが 1 つまたは複数のエンコーダーのプロパティを設定する前の呼び出しで変更されたかを決定する設定を実装します。</p></td>
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
<th>イベントのセット</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff557696" data-raw-source="[CODECAPI_CHANGELISTS](https://msdn.microsoft.com/library/windows/hardware/ff557696)">CODECAPI_CHANGELISTS</a></p></td>
<td><p>デバイスは、CODECAPI_SUPPORTSEVENTS プロパティ セットをユーザー モード イベントへの応答をサポートする場合は、このイベントがクライアントの結果の前と変更されたエンコーダーの設定の一覧を返すように設定を実装し、<em>設定</em>-プロパティの CODECAPI_SETALLDEFAULTS または CODECAPI_ALLSETTINGS のいずれかの呼び出しです。</p></td>
</tr>
</tbody>
</table>

クライアント アクセスのこれらのプロパティを**ICodecAPI** (Windows SDK のドキュメントで説明) COM インターフェイスです。 参照してください[エンコーダーのインストールと登録](encoder-installation-and-registration.md)COM インターフェイスの詳細については、どのインターフェイス KsProxy を公開する必要がありますを指定する方法を含むです。

Basic のサポートを実装する必要があります、ミニドライバー*取得*-プロパティのクエリ。 トピック[エンコーダーのコード例](encoder-code-examples.md)をサポートする方法を示します*取得*-プロパティのクエリ。

エンコーダー フィルターを開発する場合は、ビデオ キャプチャ フィルターから別のフィルターにエンコード機能を移動します。 グラフ ビルダーが正しくエンコーダーを接続してフィルターをキャプチャできるように、独自のプライベート メディアを定義します。 ハードウェアがエンコードされていないコンテンツをマスターするバスの対応の場合は、パブリック メディアも公開できます。 パブリックとプライベート両方のメディアを実装する場合、最初に表示プライベート メディア グラフの作成に時間が減るため、フィルターのグラフを作成するときに、適切なフィルターが見つかりません。

(別個のフィルターのグラフ) でのメディアとフィルターの複数のインスタンスの使用の詳細については、次を参照してください。[メディアとカテゴリ](mediums-and-categories.md)します。
