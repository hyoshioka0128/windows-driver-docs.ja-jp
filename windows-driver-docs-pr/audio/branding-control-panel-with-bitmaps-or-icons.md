---
title: ビットマップまたはアイコンを使用してコントロール パネルをブランド化する
description: ビットマップまたはアイコンを使用してコントロール パネルをブランド化する
ms.assetid: 1520cf9e-6813-41aa-aa88-39a1a6c27f74
keywords:
- オーディオアダプター WDK、コントロールパネルのブランド化
- アダプタードライバー WDK オーディオ、コントロールパネルのブランド化
- ポートクラスオーディオアダプター WDK、コントロールパネルのブランド化
- コントロールパネルのブランド化 WDK オーディオ
- ブランドデバイスコントロール WDK オーディオ
- サードパーティブランドの WDK オーディオ
- ベンダブランド化 WDK オーディオ
- ロゴブランド WDK オーディオ
- アイコン WDK audio
- ビットマップブランド化 WDK オーディオ
- イメージブランド化 WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d38c1ad44a6afd6e938134011365e1fa545b46fe
ms.sourcegitcommit: 98930ca95b9adbb6e5e472f89e91ab084e67e31d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/08/2020
ms.locfileid: "82925609"
---
# <a name="branding-control-panel-with-bitmaps-or-icons"></a>ビットマップまたはアイコンを使用してコントロール パネルをブランド化する


## <span id="control_panel_branding_by_vendors"></span><span id="CONTROL_PANEL_BRANDING_BY_VENDORS"></span>


Windows XP 以降のバージョンの Windows では、コントロールパネルの [サウンド] アプリケーションで、オーディオデバイスコントロールのサードパーティブランドがサポートされています。 独立系ハードウェアベンダー (Ihv) は、オーディオデバイスのコントロールの横に次の項目を表示できます。

-   会社のロゴ

-   独自のデバイス名

デバイスドライバーをインストールする INF ファイルでは、コントロールパネルのカスタマイズデータもレジストリに読み込まれます。 会社のロゴのビットマップ画像は、インストールされているドライバーファイル自体に含まれています。

Windows XP では、次のプログラムの場所にあるユーザーにブランド情報が表示されます。

-   コントロールパネルの [**サウンドとオーディオデバイス**] アプリケーションの [**ボリューム**] ページ (mmsys .cpl)

-   SndVol32 プログラム (Sndvol32)

Windows Vista では、ブランド情報は、コントロールパネルの [*サウンド*] アプリケーションの [**再生**と**記録**] ページでユーザーに表示されます (mmsys .cpl)。

ブランド情報は、オーディオデバイスのルートキーの下にある**ブランド**化サブキーのレジストリに格納されます。これは、メディアクラスキーの下にあります。 **ブランド**化サブキーには、次の表に\_示す REG SZ 値を1つ以上含めることができます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">値の名前</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>icon</p></td>
<td align="left"><p>SndVol32 コントロールメニューで使用されるアイコンを含むファイルの名前。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ビットマップ</p></td>
<td align="left"><p>コントロールパネルの [<strong>サウンドとオーディオデバイス</strong>] アプリケーションの [<strong>ボリューム</strong>] ページに表示される 32/32 ビットマップを含むファイルの名前。</p></td>
</tr>
</tbody>
</table>

 

これらの値は、デバイスドライバーをインストールする INF ファイルのレジストリセクション ( [**Inf AddReg ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)を参照) 内のディレクティブによってレジストリに追加されます。 コントロールパネルでは、**ブランド**サブキーにないすべての値に既定値が使用されます。

**ボリューム**ページの上部にある専用デバイス名の左側に "ビットマップ" ロゴが表示されます。 SndVol32 コントロールメニューの左上隅に "icon" ロゴが表示されます。

前述のページに記載されている独自のデバイス名は、デバイスのフレンドリ名です。 このフレンドリ名は、デバイスをインストールする INF ファイルの [レジストリの追加] セクションのディレクティブで指定します。 このディレクティブには、 [**INF AddReg ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)の例に示すように、キーワード "FriendlyName" が含まれています。 Windows XP では、**ボリューム**ページと SndVol32 には名前文字列の最初の31文字のみが表示されます。 これより長い文字列は切り詰められます。 Windows Vista 以降のバージョンの Windows では、コントロールパネルにデバイス名を表示したときにこの31文字の制限が削除されます。 Windows Vista より前のバージョンの Windows でサポートされていた Api (たとえば[、\_MCI getdevcaps](https://docs.microsoft.com/windows/win32/multimedia/mci-getdevcaps)) を使用すると、api に対して指定したデバイス名に31文字の制限が適用されます。

**重要**   windows Vista 以降のバージョンの windows では、サードパーティブランドのビットマップイメージの使用はサポートされなくなりました。 オーディオデバイスコントロールをブランド化するサードパーティのオーディオドライバー開発者は、アイコンを使用する必要があります。 これらのアイコンに対してサポートされているピクセルディメンションは、32x32 または 48 x 48 です。

 

### <a name="span-idexample_1spanspan-idexample_1spanspan-idexample_1spanexample-1"></a><span id="Example_1"></span><span id="example_1"></span><span id="EXAMPLE_1"></span>例1

次の例では、ベンダーの INF ファイルの [レジストリの追加] セクションにある2つのディレクティブを示します。

```inf
  [XYZ-Audio-Device.AddReg]
  HKR,Branding,icon,,"foo.sys,102"
  HKR,Branding,bitmap,,"c:\mydir\myimage.bmp"
```

これらのディレクティブは、コントロールパネルのブランド情報をレジストリに追加します。 HKR は、レジストリ内のオーディオデバイスのルートキーを表します。**ブランド**サブキーは、ルートキーのパス名を基準にして指定されます。 **アイコン**または**ビットマップ**キーの文字列値は、"file, resourceid" または "イメージファイル" という2つの形式のいずれかで指定できます。 前の例の最初のディレクティブでは、"file, resourceid" 形式が使用されています。 ディレクティブは、ファイル名、foo、およびリソース ID 102 を含む文字列値を**アイコン**キーに割り当てます。 ファイル名とリソース ID はコンマで区切られます (スペースは含まれません)。 ファイル foo には、アイコンリソースが含まれています。 前の例の2番目のディレクティブでは、**ビットマップ**キーに "イメージ化" 形式の文字列を割り当てます。文字列には、ビットマップを含む .bmp ファイルの完全なパス名が含まれています。

**Icon**値の example ディレクティブは、"イメージファイル" 形式を使用するように変更できますが、この例では、文字列値に拡張子が .ico のファイルのパス名を含める必要があります。

"File, resourceid" 形式の場合、コントロールパネルソフトウェアは、同じ検索パスのリストを**LoadLibrary**関数として検索します (Microsoft Windows SDK のドキュメントを参照)。 このパスリストにファイルが含まれていない場合、ソフトウェアは drivers ディレクトリも検索します (「 [**INF DestinationDirs」セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-destinationdirs-section)を参照してください)。 この形式を使用すると、INF ファイルで絶対パス名を指定しなくても、イメージを簡単にドライバーファイル自体に格納できます。

### <a name="span-idexample_2spanspan-idexample_2span-example-2"></a><span id="example_2"></span><span id="EXAMPLE_2"></span> 例 2

次の例は、windows Vista 以降のバージョンの Windows に適用されます。 この例では、ベンダーの INF ファイルのレジストリの追加セクションからディレクティブを示します。 この例では、"イメージファイル" 形式を使用します。

```inf
[ABC-Audio-Device.AddReg]
  HKR,Branding,icon,,"c:\mydir\myicon.ico"
```

 

 




