---
title: ビットマップまたはアイコンを使用してコントロール パネルをブランド化する
description: ビットマップまたはアイコンを使用してコントロール パネルをブランド化する
ms.assetid: 1520cf9e-6813-41aa-aa88-39a1a6c27f74
keywords:
- オーディオ アダプター WDK、コントロール パネルのブランド化
- アダプターのドライバー WDK オーディオ、コントロール パネルのブランド化
- ポート クラス オーディオ アダプター WDK、コントロール パネルのブランド化
- コントロール パネルのブランド化 WDK オーディオ
- ブランド化デバイス コントロールの WDK オーディオ
- 場合サードパーティ ブランドの WDK オーディオ
- ベンダーのブランド化 WDK オーディオ
- ロゴ ブランド化の WDK オーディオ
- アイコンの WDK オーディオ
- ビットマップのブランド化の WDK オーディオ
- WDK オーディオのブランド イメージ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1270c27fa33320da4e67627a07d9051f0de356e2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333895"
---
# <a name="branding-control-panel-with-bitmaps-or-icons"></a>ビットマップまたはアイコンを使用してコントロール パネルをブランド化する


## <span id="control_panel_branding_by_vendors"></span><span id="CONTROL_PANEL_BRANDING_BY_VENDORS"></span>


Windows XP と Windows の以降のバージョンでは、コントロール パネルの サウンドのアプリケーションは、サード パーティ製のオーディオ デバイス コントロールのブランド化をサポートします。 独立系ハードウェア ベンダー (Ihv) は、オーディオ デバイスのコントロールの横にある次の項目を表示できます。

-   会社のロゴ

-   独自のデバイス名

デバイス ドライバーをインストールする INF ファイルは、レジストリにも、コントロール パネルのカスタマイズのデータを読み込みます。 インストールされているドライバー ファイル自体は、会社のロゴのビットマップ イメージに格納されます。

Windows xp の場合、ブランド情報は、プログラムの次の場所でユーザーに表示されます。

-   **ボリューム**のページ、**サウンドとオーディオ デバイス**コントロール パネル (Mmsys.cpl)

-   SndVol32 プログラム (Sndvol32.exe)

Windows Vista では、ブランド情報でユーザーに表示されて、**再生**と**記録**のページ、*サウンド*コントロール パネル (Mmsys.cpl)。

ブランド化の情報がレジストリに格納されている、**ブランド**media クラス キーの下にある、オーディオ デバイスのルート キーの下のサブキー。 **ブランド**サブキーは、1 つ以上の登録に含めることができます\_次の表に示す SZ 値。

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
<td align="left"><p>アイコン●あいこん○</p></td>
<td align="left"><p>SndVol32 コントロールのメニューで使用されるアイコンを含むファイルの名前。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ビットマップ</p></td>
<td align="left"><p>表示される、32 ~ 32 でビットマップを含むファイルの名前、<strong>ボリューム</strong>のページ、<strong>サウンドとオーディオ デバイス</strong>コントロール パネルの アプリケーション。</p></td>
</tr>
</tbody>
</table>

 

これらの値は、追加レジストリ セクション内のディレクティブで、レジストリに追加されます (を参照してください[ **INF AddReg ディレクティブ**](https://msdn.microsoft.com/library/windows/hardware/ff546320)) のデバイス ドライバーをインストールする INF ファイル。 コントロール パネルの不足している任意の値の既定値を使用して、**ブランド**サブキー。

上部にある独自のデバイス名の左側に"bitmap"ロゴが表示される、**ボリューム**ページ。 SndVol32 コントロール メニューの左上隅にある「アイコン」ロゴが表示されます。

前に説明したページに表示される独自のデバイス名とは、デバイスのフレンドリ名です。 このフレンドリ名は、追加のレジストリのセクションで、デバイスをインストールする INF ファイルのディレクティブによって指定されます。 例で示すように、このディレクティブが"FriendlyName"キーワードを含む[ **INF AddReg ディレクティブ**](https://msdn.microsoft.com/library/windows/hardware/ff546320)します。 Windows xp の場合、**ボリューム**ページと SndVol32 名の文字列の最初の 31 文字のみを表示します。 長い文字列は切り捨てられます。 Windows Vista および Windows の以降のバージョンでは、コントロール パネルの デバイス名が表示されるときにこの 31 文字に制限が削除されます。 たとえば、Windows Vista より前のバージョンの Windows でサポートされていた Api を使用すると[MCI\_GetDevCaps](https://go.microsoft.com/fwlink/p/?linkid=149692)、31 文字の制限がまだ API に指定したデバイス名に適用します。

**重要な**  で Windows Vista と以降のバージョンの Windows での使用のビットマップ画像を保存のサード パーティ製のブランド化はサポートされていません。 サード パーティ製のオーディオ ドライバー開発者が、オーディオ デバイスのコントロールをブランド化する場合は、アイコンを使用する必要があります。 これらのアイコンのサポートされているピクセル寸法とは、32 x 32 または 48 x 48 です。

 

### <a name="span-idexample1spanspan-idexample1spanspan-idexample1spanexample-1"></a><span id="Example_1"></span><span id="example_1"></span><span id="EXAMPLE_1"></span>例 1

次の例では、いくつかの追加-レジストリのセクションから仕入先の INF ファイルのディレクティブを示します。

```inf
  [XYZ-Audio-Device.AddReg]
  HKR,Branding,icon,,"foo.sys,102"
  HKR,Branding,bitmap,,"c:\mydir\myimage.bmp"
```

これらのディレクティブは、コントロール パネルのブランド情報をレジストリに追加します。 HKR がレジストリでのオーディオ デバイスのルート キーを表します**ブランド**ルート キーのパス名を基準としたサブキーが指定されています。 文字列値、**アイコン**または**ビットマップ**キーは 2 つの形式のいずれかで指定できます。"ファイル, resourceid"または"イメージ ファイル"。 前の例では、最初のディレクティブは、「ファイル, resourceid」の形式を使用します。 ディレクティブに割り当てます、**アイコン**キー ファイル名、foo.sys、および 102 のリソース ID を含む文字列値。 ファイル名とリソース ID は、(スペースなし) をコンマで区切られます。 ファイル foo.sys には、アイコン リソースが含まれています。 "Imagefile"への文字列を書式設定前の例の割り当てで 2 つ目のディレクティブ、**ビットマップ**キーは、文字列には、ビットマップを含む .bmp ファイルの完全なパス名が含まれています。

例のディレクティブを**アイコン**"imagefile"の形式を使用する値を変更できますが、ここでは、文字列値は .ico ファイル名拡張子の付いたファイルのパス名を含める必要があります。

コントロール パネルのソフトウェアが同じとして検索パスの一覧を検索する「ファイル, resourceid」の形式の場合、 **LoadLibrary**関数 (Microsoft Windows SDK のドキュメントで説明)。 ソフトウェアでは、ドライバーのディレクトリを検索もこのパスの一覧にファイルが含まれていない場合 (を参照してください[ **INF DestinationDirs セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547383))。 この形式は、ドライバー ファイル自体を INF ファイルの絶対パス名を指定することを必要とせずに簡単に格納されるイメージをできます。

### <a name="span-idexample2spanspan-idexample2span-example-2"></a><span id="example_2"></span><span id="EXAMPLE_2"></span> 例 2

次の例は、Windows Vista 以降のバージョンの Windows に適用されます。 この例では、追加のレジストリのセクションから仕入先の INF ファイルのディレクティブを使用します。 この例では、"イメージのファイル"形式を使用します。

```inf
[ABC-Audio-Device.AddReg]
  HKR,Branding,icon,,"c:\mydir\myicon.ico"
```

 

 




