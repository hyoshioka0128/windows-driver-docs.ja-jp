---
title: WIA デバイスの INF ファイル
description: WIA デバイスの INF ファイル
ms.assetid: 65eac8b5-35d2-4537-8646-a35a1cf9aced
ms.date: 07/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: 1e488ae4be500658a291107d16475a6eda1c8e94
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840822"
---
# <a name="inf-files-for-wia-devices"></a>WIA デバイスの INF ファイル


静止イメージデバイスの既定のクラスインストーラーである*sti\_、ci .dll*は、特殊な一連の INF ファイルエントリを認識します。 INF ファイル内では、これらのエントリはデバイスの[**Inf DDInstall セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-section)内に配置する必要があります。 次の表で、エントリについて説明します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>INF ファイルのエントリ</th>
<th>Value</th>
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
<td><p>スキャナーの場合は1</p>
<p>2 (カメラの場合)</p>
<p>3ストリーミングビデオの場合</p></td>
<td><p>必須</p></td>
</tr>
<tr class="odd">
<td><p><strong>DeviceSubType</strong></p></td>
<td><p>ベンダー定義の値</p></td>
<td><p>省略可能</p></td>
</tr>
<tr class="even">
<td><p><strong>[接続]</strong></p></td>
<td><p>シリアルポートまたはパラレルポートに接続されている非プラグアンドプレイデバイスの場合、これは、インストール時にユーザーが選択できるポートを制限するために、シリアルまたは並列にすることができます。</p></td>
<td><p>省略可能</p>
<p>指定しない場合、ユーザーは任意のシリアルポートまたはパラレルポートを選択できます。</p></td>
</tr>
<tr class="odd">
<td><p><strong>機能</strong></p></td>
<td><p>デバイスの機能を識別するビットフラグに変換される数値を指定します。 これらのフラグはレジストリに格納され、STI_DEV_CAPS 構造体を使用して、STI コンポーネントで使用できます。</p>
<p>ビット 0: STI_DEV_CAPS の STI_GENCAP_NOTIFICATIONS を設定/クリアします。</p>
<p>ビット 1: STI_DEV_CAPS で STI_GENCAP_POLLING_NEEDED を設定/クリアします。</p>
<p>ビット 2: STI_DEV_CAPS の STI_GENCAP_GENERATE_ARRIVALEVENT を設定/クリアします。</p>
<p>ビット 3: STI_DEV_CAPS で STI_GENCAP_AUTO_PORTSELECT を設定/クリアします。</p>
<p>ビット 4: STI_DEV_CAPS で STI_GENCAP_WIA を設定/クリアします。</p>
<p>ビット 5: STI_DEV_CAPS で STI_GENCAP_SUBSET を設定/クリアします。</p></td>
<td><p>省略可能</p>
<p>ビット5は現在使用されていません。</p>
<p>スキャナーでのプッシュボタンイベントをサポートするには、INF ファイルのこのエントリを0x33 に設定します。</p></td>
</tr>
<tr class="even">
<td><p><strong>PropertyPages</strong></p></td>
<td><p>Windows 98 および Windows 2000 のみ</p>
<p>静止画像デバイス用にカスタマイズされたプロパティシートページを作成する DLL の名前とエントリポイントを識別します。</p>
<p><strong>PropertyPages</strong>エントリの詳細については、「<a href="inf-files-for-still-image-devices.md" data-raw-source="[INF Files for Still Image Devices](inf-files-for-still-image-devices.md)">イメージデバイス用の INF ファイル</a>」を参照してください。</p></td>
<td><p>省略可能</p>
<p>このエントリは、STI ドライバーによってのみ使用され、WIA ドライバーでは廃止されます。</p>
<p>WIA ドライバー開発者に関連するプロパティページの詳細については、この表の次の PropertyPages に関する<strong>メモ</strong>を参照してください。</p></td>
</tr>
<tr class="odd">
<td><p><strong>DeviceData</strong></p></td>
<td><p><strong>Devicedata</strong>キーの下にある、レジストリに格納される情報を含む、ベンダーが提供するデータセクションを識別します。 TWAIN でサポートされているデバイスの場合、data セクションには Tw: エントリが含まれている必要があります (「 <a href="registry-entries-for-wia-drivers.md" data-raw-source="[Registry Entries for WIA Drivers](registry-entries-for-wia-drivers.md)">WIA ドライバーのレジストリエントリ</a>」を参照してください)。</p></td>
<td><p>省略可能</p></td>
</tr>
<tr class="even">
<td><p><strong>イベント</strong></p></td>
<td><p>まだイメージデバイスイベントの一覧を示す、ベンダーから提供されたデータセクションを識別します。 このセクションの各エントリは、次の形式である必要があります。</p>
<p><em>EventName</em><strong>= "</strong><em>String</em><strong>"、{</strong><em>GUID</em><strong>}、</strong>アプリ</p>
<p><em>EventName</em>はイベントの内部名、<em>文字列</em>はイベントの表示文字列、 <em>guid</em>はイベントの guid、<em>アプリ</em>はイベントが発生したときに起動されるイメージングアプリケーションを指定します。 現在登録されているアプリケーションを起動するに<strong>*</strong>は、<em>アプリ</em>にアスタリスク () を使用します。</p></td>
<td><p>必須</p></td>
</tr>
<tr class="odd">
<td><p><strong>PortSelect</strong></p></td>
<td><p>デバイスのインストール時に [ポートの選択] ページが不要な場合は、値 "no" を指定すると、そのページがスキップされます。 この値により、 <strong>createfilename</strong>エントリ値も指定されます ( <strong>Createfilename</strong>の<strong>メモ</strong>を参照して、この表の下にある<strong>PORTSELECT</strong>を参照)、自動的に自動に設定されます。</p>
<p>値 Message1 を指定すると、システムによって提供されるメッセージが表示され、 <strong>Createfilename</strong>エントリ値が AUTO に設定されます。</p>
<p>手動インストールを必要とするスキャナーとカメラの両方に適用されます。</p></td>
<td><p>省略可能</p>
<p>プラグアンドプレイデバイスの場合、 <strong>Portselect</strong>は無視されますが、WIA がデバイスを読み込むためには、 <strong>createfilename</strong>エントリ値が AUTO に設定されている必要があります。 <a href="https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive" data-raw-source="[&lt;strong&gt;INF AddReg Directive&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)"><strong>Inf AddReg ディレクティブ</strong></a>を使用して、このエントリをデバイスの inf ファイルの<a href="https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-section" data-raw-source="[&lt;strong&gt;INF DDInstall Section&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-section)"><strong>Inf ddinstall セクション</strong></a>に追加します。</p></td>
</tr>
</tbody>
</table>

 

**注**   デバイスと通信するには、ユーザーモードのクライアント (ミニドライバー) が WIA サービスにデバイスのファイル名と、作成または開くオブジェクトの名前を指定する文字列を要求する必要があります。 (ファイル名は、ディスクファイルの名前である必要はありません)。このようなクエリに応答すると、WIA サービスは**Createfilename**レジストリエントリからデバイスのファイル名を取得します。 (クラスインストーラーと同様に、 *usbscan .sys*ドライバーと*scsiscan*カーネルモードドライバーはこのエントリを作成します)。ミニドライバーは、 [**Istidevicecontrol:: GetMyDevicePortName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istidevicecontrol-getmydeviceportname)メソッドを呼び出すことによって、このファイル名を受け取ります。 ミニドライバーは、このファイル名を使用して、(Microsoft Windows SDK のドキュメントで説明されている) [**CreateFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)関数を呼び出して、デバイスへのハンドルを開くことができます。
デバイスが手動でインストールされている場合は、クラスインストーラーによって**Createfilename**エントリが作成されます。このエントリの値は、[ポートの選択] ページのユーザーの選択に応じて、[COM*x*]、[LPT*x*]、または [自動] に設定されます。 手動でインストールされたデバイス (ネットワークスキャナーなど) によっては、ポートを必要としないものがあります。 このような場合、結果の [ポートの選択] ダイアログボックスでユーザーが混乱する可能性があります。 このダイアログボックスが表示されないようにするには、デバイスの INF ファイルの[**Inf DDInstall セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-section)に次のエントリを追加します。

 

```INF
     PortSelect=NO
```

このエントリ値の副作用  、 **Createfilename**エントリが AUTO に設定されていることに**注意**してください。 ミニドライバーがファイル名に対して AUTO を受け取る場合は、通信する必要があるデバイスを特定できる必要があることに注意してください。

PropertyPages の場合、WIA ドライバーでは、プロパティページを追加するために別の拡張メカニズムを使用する必要があります **。  ** また、独自の GUID をその INF ファイルの**Ui クラス ID**エントリに追加し、特定の ui 機能拡張登録を提供する必要があります (「[ユーザーインターフェイス拡張レジストリエントリ](user-interface-extension-registry-entries.md)」を参照してください)。コンテキストメニューやプロパティページなど。 また、WIA ドライバーは、コンポーネント自体の UI 拡張登録も提供する必要があります。

 

 

### <a name="additional-inf-file-entries"></a>追加の INF ファイルエントリ

次の表のエントリは、デバイスの[**INF AddReg ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)が指すセクション内に配置する必要があります。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>INF ファイルのエントリ</th>
<th>Value</th>
<th>コメント</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>ハードウェアの構成</strong></p></td>
<td><p>デバイスが使用している接続の種類を示します。</p>
<p>1, 1 −汎用 WDM デバイス</p>
<p>1、2− SCSI デバイス</p>
<p>1、4: USB デバイス</p>
<p>1、8: シリアルデバイス</p>
<p>1、16-パラレルデバイス</p></td>
<td><p>省略可能</p></td>
</tr>
<tr class="even">
<td><p><strong>USDClass</strong></p></td>
<td><p>ミニドライバーの GUID を示します。</p></td>
<td><p>(省略可能)。</p>
<p><strong>Usdclass</strong>および<strong>CLSID</strong>エントリの guid は、ミニドライバーの<strong>DllGetClassObject</strong>関数で使用されている guid と一致する必要があります。 マイクロドライバを作成する場合、値は BB6CF8E2-1511-40bd-91BA-80D43C53064E にする必要があります。 それ以外の場合は、を使用して新しい GUID を生成する必要があります (例、 <em>genguid .exe</em>)。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CLSID</strong></p></td>
<td><p>ミニドライバーの GUID を示します。</p></td>
<td><p>(省略可能)。</p>
<p><strong>Usdclass</strong>エントリの直前のコメントを確認します。</p></td>
</tr>
</tbody>
</table>

 

静止イメージデバイスの既定のクラスインストーラーでは、標準の[**INF CopyFiles ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-copyfiles-directive)がサポートされています。

引き続きイメージデバイス (sti) の既定の INF ファイルでは、デバイスの種類ごとに次の2つのインストールセクションが定義されて*います*。

-   次の表に示すように、ベンダが提供する INF ファイルの*Ddinstall*セクション内で参照する必要がある[**Inf ddinstall セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-section)。

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
    <th>要望</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>IEEE 1394/SBP2</p></td>
    <td><p>Include = sti</p></td>
    <td><p>必要 = STI。SBP2Section</p></td>
    </tr>
    <tr class="even">
    <td><p>USB</p></td>
    <td><p>Include = sti</p></td>
    <td><p>必要 = STI。USBSection</p></td>
    </tr>
    <tr class="odd">
    <td><p>SCSI</p></td>
    <td><p>Include = sti</p></td>
    <td><p>必要 = STI。SCSISection</p></td>
    </tr>
    <tr class="even">
    <td><p>シリアル</p></td>
    <td><p>Include = sti</p></td>
    <td><p>必要 = STI。SerialSection</p></td>
    </tr>
    </tbody>
    </table>

     

<!-- -->

-   次の表に示すように、ベンダが提供する INF ファイルの[**Inf ddinstall. Services セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-services-section)内で参照する必要がある Inf Ddinstall Services セクション。

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
    <th>要望</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>1394/SBP2</p></td>
    <td><p>Include = sti</p></td>
    <td><p>必要 = STI。SBP2Section</p></td>
    </tr>
    <tr class="even">
    <td><p>USB</p></td>
    <td><p>Include = sti</p></td>
    <td><p>必要 = STI。USBSection. Services</p></td>
    </tr>
    <tr class="odd">
    <td><p>SCSI</p></td>
    <td><p>Include = sti</p></td>
    <td><p>必要 = STI。SCSISection</p></td>
    </tr>
    <tr class="even">
    <td><p>シリアル</p></td>
    <td><p>Include = sti</p></td>
    <td><p>必要 = STI。SerialSection</p></td>
    </tr>
    </tbody>
    </table>

     

静止イメージデバイス用の INF ファイルの作成に関するその他のガイダンスについては、Windows で提供されている、サブクラス = StillImage というエントリを含む任意の INF ファイルを参照してください。

デバイスを WIA デバイスとして指定するには、ミニドライバー INF ファイルに、ベンダーから提供されている INF ファイルの*Devicedata*セクション内に配置されている次の値が含まれている必要があります。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>INF ファイルのエントリ</th>
<th>Value</th>
<th>コメント</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>[サーバー]</strong></p></td>
<td><p>ローカル</p></td>
<td><p>デバイスをローカルデバイスとして指定します。 これはオプションであり、ベンダーがエントリ値を指定していない場合、デバイスはローカルであると見なされます。 つまり、WIA_DIP_SERVER_NAME プロパティは Local に設定されます。</p></td>
</tr>
<tr class="even">
<td><p><strong>マイクロドライバー</strong></p></td>
<td><p>ベンダが提供する<em>.dll</em>ファイル名</p></td>
<td><p>このエントリは、WIA マイクロドライバを実装するベンダー提供の DLL の名前に設定する必要があります。</p></td>
</tr>
<tr class="odd">
<td><p><strong>UI DLL</strong></p></td>
<td><p>ベンダが提供する<em>.dll</em>ファイル名</p></td>
<td><p>廃止され、使用されませんでした。 以前は、このエントリには、ベンダーから提供されたユーザーインターフェイス DLL ファイルの名前が示されていました。</p></td>
</tr>
<tr class="even">
<td><p><strong>UI クラス ID</strong></p></td>
<td><p>ベンダ提供のデバイスクラス識別子</p></td>
<td><p>ベンダーから提供されたユーザーインターフェイスがサポートできるデバイスクラスを示します。 これは省略可能であり、ベンダーがエントリ値を指定していない場合、WIA は WIA_DIP_UI_CLSID プロパティを GUID_NULL に設定し、既定の WIA UI が使用されます。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ICMProfiles</strong></p></td>
<td><p>ベンダーが指定したカラープロファイル値</p></td>
<td><p>WIA_IPA_ICM_PROFILE_NAME プロパティに格納する値を指定します。 値が指定されていない場合は、標準の sRGB プロファイル<em>Srgb カラースペースプロファイル. icm</em>が使用されます。</p></td>
</tr>
</tbody>
</table>

 

**マイクロドライバ**エントリは、ベンダが WIA マイクロドライバを提供する場合にのみ必要です。

ユーザーインターフェイス (UI) のエントリは、ベンダーがイメージングデバイス用のカスタムユーザーインターフェイスを提供している場合にのみ必要です。

**注釈**

スキャナー用の INF ファイルを開発している場合は、 [MICROSOFT OS 記述子](https://docs.microsoft.com/previous-versions/gg463179(v=msdn.10))を使用して互換性 ID 機能を有効にすることができます。 これを行うと、1つのスキャナードライバーに複数のスキャナーモデルとの互換性を持たせることができます。

 

 




