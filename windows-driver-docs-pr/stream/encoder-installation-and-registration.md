---
title: エンコーダーのインストールと登録
description: エンコーダーのインストールと登録
ms.assetid: 6ce0c504-977a-4db5-b5ee-128b69ce8eba
keywords:
- カーネル ストリーミング カテゴリ WDK エンコーダー
- エンコーダー デバイス WDK AVStream
- AVStream WDK、エンコーダーのデバイス
- 非圧縮データ ストリームの WDK AVStream
- エンコードされたストリーム WDK AVStream
- オーディオ エンコーダー デバイス WDK AVStream
- ビデオ エンコーダー デバイス WDK AVStream
- INF ファイル WDK エンコーダー
- メタデータの WDK エンコーダー
- KS プロキシ WDK AVStream
- カーネル ストリーミング プロキシ WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 72e6352203196ace9a938e80eb20273d41c1c4ca
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528120"
---
# <a name="encoder-installation-and-registration"></a>エンコーダーのインストールと登録


エンコーダー フィルター ドライバーの INF ファイルには、以下を定義するエントリを含める必要があります。

-   追加のカーネル ストリーミング キャプチャ コンポーネント

-   COM インターフェイス KsProxy を公開する必要があります。

-   エンコーダーのフィルターの機能を記述するメタデータ値

-   フィルターのカーネルのカテゴリのストリーミング

### <a name="additional-kernel-streaming-capture-components"></a>**Capture コンポーネントの追加のカーネルのストリーミング**

エンコーダーのデバイスを参照する必要がありますのドライバーをインストールするために使用する INF ファイル*ks.inf*と*kscaptur.inf*でその\[DefaultInstall\]のためキャプチャ ドライバーとしてセクションこれらファイルは、エンコーダー コンポーネントのために必要なサポートを追加します。 次に、例を示します。

```INF
[DefaultInstall]
include=ks.inf,kscaptur.inf
needs=[Your driver's DDInstall section],KS.Registration,KSCAPTUR.Registration.NT
```

### <a name="which-com-interface-ksproxy-should-expose"></a>**どの COM インターフェイス KsProxy を公開する必要があります。**

**AddReg**セクション、ドライバーの INF ファイルの指定を COM インターフェイスを示すために次の 3 つの Guid のいずれかのプラグインの KsProxy (*encapi.dll*) クライアントに公開する必要があります。 COM インターフェイスは、エンコーダーのフィルターで実装したプロパティのサポートによって決定されます。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>インターフェイスの GUID</th>
<th>名前</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>{B43C4EEC-8C32-4791-9102-508ADA5EE8E7}</p></td>
<td><p><strong>CLSID_IVideoEncoderProxy</strong></p></td>
<td><p>KsProxy を公開するには、この GUID を指定、 <strong>IVideoEncoder</strong> (古い世代 Microsoft によって提供されるエンコーダー サポートの旧バージョンとの互換性) 用の COM インターフェイスです。 クライアントはこのインターフェイスから派生する必要があります、 <strong>IEncoderAPI</strong> COM インターフェイスです。</p></td>
</tr>
<tr class="even">
<td><p>{7FF0997A-1999-4286-A73C-622B8814E7EB}</p></td>
<td><p><strong>CLSID_ICodecAPIProxy</strong></p></td>
<td><p>KsProxy を公開するには、この GUID を指定、 <strong>ICodecAPI</strong> (オーディオ専用のエンコーダーなどないビデオ エンコード デバイス) の COM インターフェイスです。</p></td>
</tr>
<tr class="odd">
<td><p>{B05DABD9-56E5-4FDC-AFA4-8A47E91F1C9C}</p></td>
<td><p><strong>CLSID_IVideoEncoderCodecAPIProxy</strong></p></td>
<td><p>両方を公開する KsProxy させるには、この GUID を指定、 <strong>IVideoEncoder</strong>と<strong>ICodecAPI</strong> (下位互換性および上位互換性) 用の COM インターフェイスです。</p></td>
</tr>
</tbody>
</table>

 

次に、例を示します。

```INF
[Your driver's AddReg section]
HKR,Interfaces\{B43C4EEC-8C32-4791-9102-508ADA5EE8E7},,,
```

これが原因でのみを公開する KsProxy、 **IVideoEncoder** (**CLSID\_IVideoEncoderProxy**) COM インターフェイスです。

これらの COM インターフェイスは、DirectX 9 と Windows Sdk for Windows XP SP1 以降の DirectShow セクションに記載されています。

### <a href="" id="metadata-values-that-advertise-the-encoder-filter-s-capabilities"></a>**エンコーダー フィルターの機能を提供するメタデータ値**

内のメタデータ値を指定することができます、*デバイス パラメーター\\機能*エンコーダーの INF ファイルで、レジストリの領域。 アプリケーションでは、実装、またはユーザーに公開するのにには、どのような機能を決定するのに、これらのメタデータ値を使用できます。

次に、例を示します。

```INF
[Your driver's AddReg section]
HKR,Capabilities,,,
HKR,Capabilities,"{12345678-1234-1234-1234-12345678abcd}",,guid1
```

これは、ように、メタデータ項目が作成"{12345678-1234-1234-1234-12345678abcd} guid1 を ="で、*デバイス パラメーター\\機能*エンコーダーのレジストリ設定の領域。 空の行は、存在しない場合は、レジストリ キーを作成する必要があります。

エンコーダー フィルターは、アプリケーションで使用するための INF ファイルでこのような静的メタデータを指定できます。 たとえば、Windows XP Media Center Edition は、Windows XP Media Center Edition-対応していることを示すエンコーダーをチェックします。

### <a href="" id="the-filter-s-kernel-streaming-category"></a>**フィルターのカーネルのカテゴリのストリーミング**

カーネル ストリーム フィルターには、カーネルが属するカテゴリのストリーミングを指定しなければなりません。 Microsoft では、エンコーダーのフィルター、マルチプレクサー (マルチプレクサー) フィルターなどの一般的なカテゴリの Guid を定義します。

フィルター内の Guid に次の 1 つ以上を指定することで、それぞれのカテゴリを示すため、 **AddInterface**ミニドライバーの INF ファイルのフィルターのセクションのディレクティブ。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>カーネル ストリーミング カテゴリ GUID</th>
<th>名前</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>{19689BF6-C384-48FD-AD51-90E58C79F70B}</p></td>
<td><p>KSCATEGORY_ENCODER</p></td>
<td><p>エンコーダーのフィルターには、この GUID を指定します。</p></td>
</tr>
<tr class="even">
<td><p>{7A5DE1D3-01A1-452C-B481-4FA2B96271E8}</p></td>
<td><p>KSCATEGORY_MULTIPLEXER</p></td>
<td><p>Mux フィルターには、この GUID を指定します。</p></td>
</tr>
</tbody>
</table>

 

エンコーダー フィルターを登録するには、指定、KSCATEGORY\_、ドライバーのエンコーダー GUID *DDInstall*.**インターフェイス**INF ファイルのセクション。 次に、例を示します。

```INF
[Your Driver's DDInstall.Interface section]
AddInterface=%KSCATEGORY_ENCODER%,%KSNAME_Filter%,MyEncoderDevice.AddInterface

[MyEncoderDevice.AddInterface]
AddReg=MyEncoderDevice.AddReg

[MyEncoderDevice.AddReg]
HKR,,CLSID,,%KSProxy.CLSID%
HKR,,FriendlyName,,%MyEncoderDeviceFriendlyName%

[Strings]
KSCATEGORY_ENCODER="{19689BF6-C384-48FD-AD51-90E58C79F70B}"
KSNAME_Filter="{9B365890-165F-11D0-A195-0020AFD156E4}"
KSProxy.CLSID="17CCA71B-ECD7-11D0-B908-00A0C9223196"
MyEncoderDeviceFriendlyName="My Encoder Device"
```

**注:** 指定された GUID *KSNAME\_フィルター*と一致する必要があります、 **ReferenceGuid**で指定されたメンバー、 [ **KSFILTER\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff562553)フィルターを記述する構造体。

 

 




