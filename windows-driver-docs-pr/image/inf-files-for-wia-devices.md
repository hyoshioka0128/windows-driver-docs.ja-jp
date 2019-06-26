---
title: WIA デバイスの INF ファイル
description: WIA デバイスの INF ファイル
ms.assetid: 65eac8b5-35d2-4537-8646-a35a1cf9aced
ms.date: 07/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: 072cde1e6e71a124032d2e7ec074d7622e91ecfb
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67391416"
---
# <a name="inf-files-for-wia-devices"></a>WIA デバイスの INF ファイル


既定クラスのインストーラーを静止画像デバイス、 *sti\_ci.dll*、INF ファイルのエントリの特殊なセットを認識します。 内でのデバイスの INF ファイル内でこれらのエントリを配置する必要があります[ **INF DDInstall セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-section)します。 エントリは、次の表で説明します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>INF ファイルのエントリ</th>
<th>[値]</th>
<th>コメント</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>サブクラス</strong></p></td>
<td><p>StillImage</p></td>
<td><p>必須</p></td>
</tr>
<tr class="even">
<td><p><strong>DeviceType</strong></p></td>
<td><p>スキャナーの場合は 1</p>
<p>カメラの 2</p>
<p>ビデオのストリーミング 3</p></td>
<td><p>必須</p></td>
</tr>
<tr class="odd">
<td><p><strong>DeviceSubType</strong></p></td>
<td><p>ベンダー定義の値</p></td>
<td><p>省略可能</p></td>
</tr>
<tr class="even">
<td><p><strong>[接続]</strong></p></td>
<td><p>プラグ アンド プレイ デバイスのシリアル ポートまたはパラレル ポートに接続されている場合は、インストール時にポートのユーザーの選択を制限するには、シリアルまたは並列このできます。</p></td>
<td><p>省略可能</p>
<p>指定しない場合、ユーザーは、任意のシリアル ポートまたはパラレル ポートを選択できます。</p></td>
</tr>
<tr class="odd">
<td><p><strong>機能</strong></p></td>
<td><p>デバイスの機能を示すフラグをビットに変換される数を指定します。 これらのフラグは、レジストリに格納されて、STI_DEV_CAPS 構造体を使用して STI コンポーネントで使用できます。</p>
<p>STI_DEV_CAPS 0 − セット/クリア STI_GENCAP_NOTIFICATIONS ビットします。</p>
<p>STI_DEV_CAPS 1 − セット/クリア STI_GENCAP_POLLING_NEEDED ビットします。</p>
<p>STI_DEV_CAPS 2 − セット/クリア STI_GENCAP_GENERATE_ARRIVALEVENT ビットします。</p>
<p>STI_DEV_CAPS 3 − セット/クリア STI_GENCAP_AUTO_PORTSELECT ビットします。</p>
<p>STI_DEV_CAPS 4 − セット/クリア STI_GENCAP_WIA ビットします。</p>
<p>STI_DEV_CAPS 5 − セット/クリア STI_GENCAP_SUBSET ビットします。</p></td>
<td><p>省略可能</p>
<p>5 ビットは現在使用できません。</p>
<p>0x33、スキャナーにプッシュ ボタンのイベントをサポートするために、INF ファイルでは、このエントリを設定します。</p></td>
</tr>
<tr class="even">
<td><p><strong>プロパティ ページ</strong></p></td>
<td><p>Windows 98 および Windows 2000 のみ</p>
<p>デバイスをまだイメージのカスタマイズされたプロパティ シートのページを作成する DLL の名前とエントリ ポイントを識別します。</p>
<p>詳細については、<strong>プロパティ ページ</strong>エントリを参照してください<a href="inf-files-for-still-image-devices.md" data-raw-source="[INF Files for Still Image Devices](inf-files-for-still-image-devices.md)">静止画像デバイスの INF ファイル</a>します。</p></td>
<td><p>省略可能</p>
<p>このエントリは STI ドライバーによってのみ使用するためは WIA ドライバーの廃止されています。</p>
<p>WIA ドライバー開発者向けに関連するプロパティ ページについては、次を参照してください。、<strong>注</strong>プロパティ ページの次の表の後にします。</p></td>
</tr>
<tr class="odd">
<td><p><strong>DeviceData</strong></p></td>
<td><p>下のレジストリに格納される情報を格納しているベンダーから提供されたデータのセクションを識別、 <strong>DeviceData</strong>キー。 TWAIN でサポートされているデバイスでは、[データ] セクションが TwainDS エントリを含める必要があります (を参照してください<a href="registry-entries-for-wia-drivers.md" data-raw-source="[Registry Entries for WIA Drivers](registry-entries-for-wia-drivers.md)">WIA ドライバーのレジストリ エントリ</a>)。</p></td>
<td><p>省略可能</p></td>
</tr>
<tr class="even">
<td><p><strong>イベント</strong></p></td>
<td><p>静止画像デバイス イベントの一覧を表示するベンダーから提供されたデータのセクションを識別します。 このセクションでは、各エントリには、次の形式が必要です。</p>
<p><em>EventName</em><strong>="</strong><em>文字列</em><strong>"、{</strong><em>GUID</em><strong>}、</strong>アプリ</p>
<p><em>EventName</em>イベントの内部名は、<em>文字列</em>は、イベントの表示文字列、 <em>GUID</em>イベントの guid をおよび<em>アプリ</em>がイメージの作成を指定しますイベントの発生時に起動するアプリケーション。 現在登録されているアプリケーションを起動するには、アスタリスクを使用して、(<strong>*</strong>) の<em>アプリ</em>します。</p></td>
<td><p>必須</p></td>
</tr>
<tr class="odd">
<td><p><strong>PortSelect</strong></p></td>
<td><p>デバイスのインストールにポートの選択 ページが必要としない場合はスキップするには、そのページと、"no"の値。 この値はまた、 <strong>CreateFileName</strong>エントリの値 (を参照してください、<strong>注</strong>で<strong>CreateFileName</strong>と<strong>PortSelect</strong>次の表の後) を AUTO に自動的に設定します。</p>
<p>Message1 原因がシステム提供のメッセージが表示されます、およびセットの値、 <strong>CreateFileName</strong>エントリの値を AUTO にします。</p>
<p>スキャナーとカメラを手動でインストールを必要とする両方に適用されます。</p></td>
<td><p>省略可能</p>
<p>プラグ アンド プレイ デバイスの場合は、注意してください<strong>PortSelect</strong>は無視されます、デバイスが引き続き必要がありますが、 <strong>CreateFileName</strong> WIA をデバイスを読み込むために、エントリの値が自動に設定します。 使用して、 <a href="https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive" data-raw-source="[&lt;strong&gt;INF AddReg Directive&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)"> <strong>INF AddReg ディレクティブ</strong></a>にこのエントリを追加する、 <a href="https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-section" data-raw-source="[&lt;strong&gt;INF DDInstall Section&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-section)"> <strong>INF DDInstall セクション</strong></a>のデバイスの INF ファイル。</p></td>
</tr>
</tbody>
</table>

 

**注**  デバイスを通信するために、ユーザー モードのクライアント (、ミニドライバー) は、デバイスのファイル名を作成したり開いたりするオブジェクトの名前を指定する文字列 WIA サービスを問い合わせる必要があります。 (ファイル名がディスク ファイルの名前になります。)このようなクエリに応答して、WIA サービスの取得から、デバイスのファイル名、 **CreateFileName**レジストリ エントリ。 (、 *Usbscan.sys*と*scsiscan.sys*クラスのインストーラーとカーネル モード ドライバーが、このエントリを作成します)。ミニドライバーは、呼び出すことによってこのファイル名を受け取る、 [ **IStiDeviceControl::GetMyDevicePortName** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istidevicecontrol-getmydeviceportname)メソッド。 呼び出すときに、ミニドライバーはこのファイル名を使用してできます、 [ **CreateFile** ](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)関数 (Microsoft Windows SDK のドキュメントで説明) をデバイスを識別するハンドルを開きます。
クラスのインストーラーを作成、デバイスを手動でインストールする場合、 **CreateFileName**エントリがポートの選択 ページで、ユーザーの選択に依存するいずれかの値を設定します。COM*X*、LPT*X*、または AUTO です。 手動でインストールされている一部のデバイス (ネットワーク スキャナーの例) では、ポートは必要ありません。 このような場合、結果として得られるポートの選択 ダイアログ ユーザーが混乱することができます。 このダイアログ ボックスを次のエントリを追加してが表示されないようにすることができます、 [ **INF DDInstall セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-section)のデバイスの INF ファイル。

 

```INF
     PortSelect=NO
```

**注**  このエントリの値の副作用は、 **CreateFileName**エントリが AUTO に設定します。 正確にいる場合、ミニドライバーは、ファイル名の自動を受け取るがありますが通信するデバイスを独自に判断できません。

**注**  のプロパティ ページ、WIA ドライバーする必要がありますを使用して、さまざまな機能拡張メカニズム プロパティ ページを追加するには。 独自の GUID を追加する必要がありますも、 **UI クラス ID**の INF ファイル内のエントリと、特定の UI 拡張機能の登録を提供する必要があります (を参照してください[ユーザー インターフェイスの拡張機能のレジストリ エントリ](user-interface-extension-registry-entries.md)) UI コンポーネントのなど、一般的なダイアログは、置換、またはコンテキスト メニューとプロパティ ページなど、追加されます。 WIA ドライバーでは、コンポーネント自体の UI 拡張機能の登録も用意する必要があります。

 

 

### <a name="additional-inf-file-entries"></a>追加の INF ファイルのエントリ

次の表に、エントリは、デバイスのによって示されるセクション内に配置する必要があります[ **INF AddReg ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive):

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>INF ファイルのエントリ</th>
<th>[値]</th>
<th>コメント</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>HardwareConfig</strong></p></td>
<td><p>デバイスを使用して接続の種類を示します。</p>
<p>1, 1 − 汎用 WDM デバイス</p>
<p>1, 2 − SCSI デバイス</p>
<p>1\.4 − USB デバイス</p>
<p>1,8 − シリアル デバイス</p>
<p>1,16 − 並列デバイス</p></td>
<td><p>省略可能</p></td>
</tr>
<tr class="even">
<td><p><strong>USDClass</strong></p></td>
<td><p>ミニドライバーの GUID を示します。</p></td>
<td><p>任意。</p>
<p>内の GUID、 <strong>USDClass</strong>と<strong>CLSID</strong>エントリで使用されている GUID が一致する必要があります、 <strong>DllGetClassObject</strong>ミニドライバーの関数。 Microdriver を記述する場合、値が BB6CF8E2-1511-40bd-91BA-80D43C53064E にあります。 を使用して、新しい GUID を、生成する必要がありますそれ以外の場合、 <em>genguid.exe</em>します。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CLSID</strong></p></td>
<td><p>ミニドライバーの GUID を示します。</p></td>
<td><p>任意。</p>
<p>直前のコメントを参照してください、 <strong>USDClass</strong>エントリ。</p></td>
</tr>
</tbody>
</table>

 

既定クラスのインストーラーを静止画像デバイス標準をサポートする[ **INF CopyFiles ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-copyfiles-directive)します。

まだのイメージのデバイスの既定の INF ファイル*sti.inf*デバイスの種類ごとに 2 つのインストール セクションを次のように定義します。

-   [ **INF DDInstall セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-section)、内で参照されている必要があります、 *DDInstall*のベンダーから提供された INF ファイルの次の表に示すようにします。

    <table>
    <colgroup>
    <col width="33%" />
    <col width="33%" />
    <col width="33%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>デバイスの種類</th>
    <th>Include</th>
    <th>必要があります。</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>IEEE 1394/SBP2</p></td>
    <td><p>Include=sti.inf</p></td>
    <td><p>必要な STI を = です。SBP2Section</p></td>
    </tr>
    <tr class="even">
    <td><p>USB</p></td>
    <td><p>Include=sti.inf</p></td>
    <td><p>必要な STI を = です。USBSection</p></td>
    </tr>
    <tr class="odd">
    <td><p>SCSI</p></td>
    <td><p>Include=sti.inf</p></td>
    <td><p>必要な STI を = です。SCSISection</p></td>
    </tr>
    <tr class="even">
    <td><p>シリアル</p></td>
    <td><p>Include=sti.inf</p></td>
    <td><p>必要な STI を = です。SerialSection</p></td>
    </tr>
    </tbody>
    </table>

     

<!-- -->

-   内で参照する必要があります INF DDInstall サービス セクションを[ **INF DDInstall.Services セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-services-section)のベンダーから提供された INF ファイルの次の表に示すようにします。

    <table>
    <colgroup>
    <col width="33%" />
    <col width="33%" />
    <col width="33%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>デバイスの種類</th>
    <th>Include</th>
    <th>必要があります。</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>1394/SBP2</p></td>
    <td><p>Include=sti.inf</p></td>
    <td><p>必要な STI を = です。SBP2Section.Services</p></td>
    </tr>
    <tr class="even">
    <td><p>USB</p></td>
    <td><p>Include=sti.inf</p></td>
    <td><p>必要な STI を = です。USBSection.Services</p></td>
    </tr>
    <tr class="odd">
    <td><p>SCSI</p></td>
    <td><p>Include=sti.inf</p></td>
    <td><p>必要な STI を = です。SCSISection.Services</p></td>
    </tr>
    <tr class="even">
    <td><p>シリアル</p></td>
    <td><p>Include=sti.inf</p></td>
    <td><p>必要な STI を = です。SerialSection.Services</p></td>
    </tr>
    </tbody>
    </table>

     

静止画像デバイスの INF ファイルを作成する追加のガイダンスについては、サブクラスのエントリを含む Windows で提供される任意の INF ファイルを表示できる StillImage を = です。

WIA デバイスとして、デバイスを指定するには、ミニドライバー INF ファイルが配置内で、次の値を含める必要があります、 *DeviceData*ベンダーから提供された INF ファイルのセクション。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>INF ファイルのエントリ</th>
<th>[値]</th>
<th>コメント</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>[サーバー]</strong></p></td>
<td><p>ローカル</p></td>
<td><p>ローカルのデバイスとしては、デバイスを指定します。 これは省略可能と仕入先がエントリの値を指定しない場合、デバイスをローカルと見なされます。 つまり、WIA_DIP_SERVER_NAME プロパティは、ローカルに設定されます。</p></td>
</tr>
<tr class="even">
<td><p><strong>MicroDriver</strong></p></td>
<td><p>ベンダーから提供された<em>.dll</em>ファイル名</p></td>
<td><p>このエントリは、WIA microdriver を実装するベンダーから提供された DLL の名前に設定する必要があります。</p></td>
</tr>
<tr class="odd">
<td><p><strong>UI の DLL</strong></p></td>
<td><p>ベンダーから提供された<em>.dll</em>ファイル名</p></td>
<td><p>古い形式と使用されることはありません。 以前は、このエントリには、ベンダーから提供されたユーザー インターフェイスの DLL ファイルの名前が示されます。</p></td>
</tr>
<tr class="even">
<td><p><strong>UI のクラス ID</strong></p></td>
<td><p>デバイスのベンダーから提供されたクラスの識別子</p></td>
<td><p>デバイスのベンダーから提供されたクラスのユーザー インターフェイスがサポートできることを示します。 これは省略可能ですし、WIA が GUID_ を WIA UI を使用する既定の WIA_DIP_UI_CLSID プロパティを設定する仕入先がエントリの値を指定しない場合。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ICMProfiles</strong></p></td>
<td><p>ベンダーから提供されたカラー プロファイルの値</p></td>
<td><p>WIA_IPA_ICM_PROFILE_NAME プロパティに値を指定します。 値が指定されていない場合、標準の sRGB プロファイル<em>sRGB 色空間 Profile.icm</em>使用されます。</p></td>
</tr>
</tbody>
</table>

 

**MicroDriver**仕入先が供給 WIA microdriver 場合にのみエントリが必要です。

ユーザー インターフェイス (UI) のエントリが、ベンダー、イメージング デバイスのカスタム ユーザー インターフェイスを提供している場合にのみ必要です。

**注釈**

スキャナー、INF ファイルを開発するときに使用できます[Microsoft OS ディスクリプター](https://docs.microsoft.com/previous-versions/gg463179(v=msdn.10))互換性 ID 機能を有効にします。 これを行う場合は、複数のスキャナー モデルと互換性がある 1 つのスキャナー ドライバーを許可します。

 

 




