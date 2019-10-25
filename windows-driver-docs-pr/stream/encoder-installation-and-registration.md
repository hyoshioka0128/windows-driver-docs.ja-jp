---
title: エンコーダーのインストールと登録
description: エンコーダーのインストールと登録
ms.assetid: 6ce0c504-977a-4db5-b5ee-128b69ce8eba
keywords:
- カーネルストリーミングカテゴリ WDK エンコーダー
- エンコーダーデバイス WDK AVStream
- AVStream WDK、エンコーダーデバイス
- 非圧縮データストリーム WDK AVStream
- エンコードされたストリーム WDK AVStream
- オーディオエンコーダーデバイス WDK AVStream
- ビデオエンコーダーデバイス WDK AVStream
- INF ファイル WDK エンコーダー
- メタデータ WDK エンコーダー
- KS プロキシ WDK AVStream
- カーネルストリーミングプロキシ WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ab5542fd5b9fd72244ebdc491049391e33f1fdc6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834429"
---
# <a name="encoder-installation-and-registration"></a>エンコーダーのインストールと登録


エンコーダーフィルターが適用されたドライバーの INF ファイルには、次の項目を定義するエントリが含まれている必要があります。

-   その他のカーネルストリーミングキャプチャコンポーネント

-   COM インターフェイス Ksk プロキシで公開する必要があるもの

-   エンコーダーフィルターの機能を記述するメタデータ値

-   フィルターのカーネルストリーミングカテゴリ

### <a name="additional-kernel-streaming-capture-components"></a>**その他のカーネルストリーミングキャプチャコンポーネント**

エンコーダーデバイス用のドライバーをインストールするために使用する INF ファイルでは、\[DefaultInstall\] セクションの*ks*と*kscaptur*をキャプチャドライバーとして参照する必要があります。これらのファイルでは、エンコーダーコンポーネントに必要なサポートが追加されるためです。 次に、例を示します。

```INF
[DefaultInstall]
include=ks.inf,kscaptur.inf
needs=[Your driver's DDInstall section],KS.Registration,KSCAPTUR.Registration.NT
```

### <a name="which-com-interface-ksproxy-should-expose"></a>**COM インターフェイス Ksk プロキシで公開する必要があるもの**

ドライバーの INF ファイルの**AddReg**セクションで、次の3つの guid のいずれかを指定して、ksk プロキシプラグイン (*encapi .dll*) がクライアントに公開する COM インターフェイスを示します。 COM インターフェイスは、エンコーダーフィルターで実装したプロパティサポートによって決定されます。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>インターフェイス GUID</th>
<th>名前</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>{B43C4EEC-8C32-4791-9102-508ADA5EE8E7}</p></td>
<td><p><strong>CLSID_IVideoEncoderProxy</strong></p></td>
<td><p>この GUID を指定すると、Ksk プロキシが<strong>Ivideoencoder</strong> COM インターフェイスを公開するようになります (Microsoft が提供する以前の世代のエンコーダーサポートとの下位互換性のため)。 クライアントは、 <strong>IEncoderAPI</strong> COM インターフェイスからこのインターフェイスを派生させる必要があります。</p></td>
</tr>
<tr class="even">
<td><p>{7FF0997A-1999-4286-A73C-622B88 14E7EB}</p></td>
<td><p><strong>CLSID_ICodecAPIProxy</strong></p></td>
<td><p>この GUID を指定すると、Ksk プロキシで<strong>ICodecAPI</strong> COM インターフェイスが公開されます (オーディオ専用エンコーダーなどのビデオ以外のエンコードデバイスの場合)。</p></td>
</tr>
<tr class="odd">
<td><p>{B05DABD9-56E5-4FDC-AFA4-8A47E91F1C9C}</p></td>
<td><p><strong>CLSID_IVideoEncoderCodecAPIProxy</strong></p></td>
<td><p>この GUID を指定すると、KsProxy は<strong>Ivideoencoder</strong>インターフェイスと<strong>ICodecAPI</strong> COM インターフェイスの両方を公開します (後方互換性のために)。</p></td>
</tr>
</tbody>
</table>

 

次に、例を示します。

```INF
[Your driver's AddReg section]
HKR,Interfaces\{B43C4EEC-8C32-4791-9102-508ADA5EE8E7},,,
```

これにより、KsProxy は**Ivideoencoder** (**CLSID\_IVideoEncoderProxy**) COM インターフェイスのみを公開するようになります。

これらの COM インターフェイスについては、DirectX 9 の DirectShow セクションと Windows XP SP1 以降の Windows Sdk に記載されています。

### <a href="" id="metadata-values-that-advertise-the-encoder-filter-s-capabilities"></a>**エンコーダーフィルターの機能を提供するメタデータ値**

エンコーダーの INF ファイルのレジストリの [*デバイスパラメーター\\機能*] 領域で、メタデータ値を指定できます。 アプリケーションでは、これらのメタデータ値を使用して、ユーザーに実装または公開する機能を決定できます。

次に、例を示します。

```INF
[Your driver's AddReg section]
HKR,Capabilities,,,
HKR,Capabilities,"{12345678-1234-1234-1234-12345678abcd}",,guid1
```

これにより、エンコーダーのレジストリ設定の [*デバイスパラメーター\\機能*] 領域にメタデータ項目 "{12345678-1234-1234-1234-12345678abcd} = guid1" が作成されます。 レジストリキーが存在しない場合は、空の行を作成する必要があります。

エンコーダーフィルターでは、アプリケーションで使用するためにそのような静的メタデータを INF ファイルに指定できます。 たとえば、Windows XP Media Center Edition では、Windows XP Media Center エディションに準拠していることを示すエンコーダーが確認されます。

### <a href="" id="the-filter-s-kernel-streaming-category"></a>**フィルターのカーネルストリーミングカテゴリ**

カーネルストリーミングフィルターでは、それらが属するカーネルストリーミングカテゴリを指定する必要があります。 Microsoft では、エンコーダーフィルターやマルチプレクサー (mux) フィルターなど、一般的なカテゴリの Guid を定義しています。

フィルターはそれぞれのカテゴリを示します。そのためには、ミニドライバーの INF ファイルのフィルターのセクションの**Addinterface**ディレクティブで、次の guid を1つ以上指定します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>カーネルストリーミングカテゴリ GUID</th>
<th>名前</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>{19689BF6-C384-48FD-AD51-90E58C79F70B}</p></td>
<td><p>KSCATEGORY_ENCODER</p></td>
<td><p>エンコーダーフィルターにこの GUID を指定します。</p></td>
</tr>
<tr class="even">
<td><p>{7A5DE1D3-01A1-452C-B481-4FA2B96271E8}</p></td>
<td><p>KSCATEGORY_MULTIPLEXER</p></td>
<td><p>Mux フィルターにこの GUID を指定します。</p></td>
</tr>
</tbody>
</table>

 

エンコーダーフィルターを登録するには、ドライバーの*Ddinstall*で KSCATEGORY\_encoder GUID を指定します。**インターフェイス**INF ファイルセクション。 次に、例を示します。

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

**注:** *Ksk 名\_フィルター*に指定する guid は、フィルターを記述する[**KSK フィルター\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksfilter_descriptor)の構造体で指定した**referenceguid**メンバーと一致している必要があります。

 

 




