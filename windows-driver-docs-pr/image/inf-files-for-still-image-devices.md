---
title: 静止画像デバイスの INF ファイル
description: 静止画像デバイスの INF ファイル
ms.assetid: f68ba904-9049-4f7e-9903-fdf6f413a1a5
ms.date: 07/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: d8f2db18b4d7e901bcce1e4164d88c548ef55c5d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536109"
---
# <a name="inf-files-for-still-image-devices"></a>静止画像デバイスの INF ファイル

既定クラスのインストーラーを静止画像デバイス、 *sti\_ci.dll*、INF ファイルのエントリの特殊なセットを認識します。 内でのデバイスの INF ファイル内でこれらのエントリを配置する必要があります[ **INF DDInstall セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547344)します。 エントリは、次の表で説明します。

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
<td><p><strong>StillImage</strong></p></td>
<td><p>必須</p></td>
</tr>
<tr class="even">
<td><p><strong>DeviceType</strong></p></td>
<td><p><strong>1</strong>スキャナー、 <strong>2</strong>カメラ、 <strong>3</strong>ビデオ デバイス</p></td>
<td><p>必須</p></td>
</tr>
<tr class="odd">
<td><p><strong>DeviceSubType</strong></p></td>
<td><p>ベンダー定義の値。</p></td>
<td><p>省略可能</p></td>
</tr>
<tr class="even">
<td><p><strong>接続</strong></p></td>
<td><p>これは、非 PnP デバイスのシリアル ポートまたはパラレル ポートに接続されている場合<strong>シリアル</strong>または<strong>並列</strong>ユーザーを制限する&#39;のインストール時にポートの s 選択します。</p></td>
<td><p>(省略可能)。 指定しない場合、ユーザーは、任意のシリアル ポートまたはパラレル ポートを選択できます。</p></td>
</tr>
<tr class="odd">
<td><p><strong>機能</strong></p></td>
<td><p>デバイスの機能を示すフラグをビットに変換される数を指定します。 これらのフラグは、レジストリに格納し、して Microsoft STI コンポーネントで使用できますが、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff548380" data-raw-source="[&lt;strong&gt;STI_DEV_CAPS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548380)"> <strong>STI_DEV_CAPS</strong> </a>構造体。</p>
<p>STI_DEV_CAPS 0 − セット/クリア STI_GENCAP_NOTIFICATIONS ビットします。</p>
<p>STI_DEV_CAPS 1 − セット/クリア STI_GENCAP_POLLING_NEEDED ビットします。</p>
<p>STI_DEV_CAPS 2 − セット/クリア STI_GENCAP_GENERATE_ARRIVALEVENT ビットします。</p>
<p>STI_DEV_CAPS 3 − セット/クリア STI_GENCAP_AUTO_PORTSELECT ビットします。</p></td>
<td><p>省略可能</p></td>
</tr>
<tr class="even">
<td><p><strong>プロパティ ページ</strong></p></td>
<td><p>カスタマイズを作成する DLL の名前とエントリ ポイントを識別する<a href="property-sheet-pages-for-still-image-devices.md" data-raw-source="[Property Sheet Pages for Still Image Devices](property-sheet-pages-for-still-image-devices.md)">静止画像デバイスのプロパティ シート ページ</a>します。</p>
<p>次の例は、DLL を識別<em>estp2cpl.dll</em>、だけでなく<strong>EnumStiPropPages</strong>この DLL 内のエントリ ポイント。 エントリ ポイント名は省略可能です。エントリ ポイントの既定値を省略した場合、 <strong>EnumStiPropPages</strong>します。</p>
<pre space="preserve"><code>PropertyPages = estp2cpl.dll, EnumStiPropPages</code></pre></td>
<td><p>省略可能</p></td>
</tr>
<tr class="odd">
<td><p><strong>DeviceData</strong></p></td>
<td><p>下のレジストリに格納される情報を格納しているベンダーから提供されたデータのセクションを識別、 <strong>DeviceData</strong>キー。 TWAIN でサポートされているデバイスでは、[データ] セクションを含める必要があります、 <strong>TwainDS</strong>エントリ (を参照してください<a href="registry-entries-for-still-image-devices.md#ddk-vendor-modifiable-registry-values-si" data-raw-source="[Vendor-Modifiable Registry Values](registry-entries-for-still-image-devices.md#ddk-vendor-modifiable-registry-values-si)">仕入先が変更可能なレジストリ値</a>)。</p></td>
<td><p>(省略可能)。 このエントリが必要です。<a href="creating-push-model-aware-applications.md" data-raw-source="[Creating Push-Model Aware Applications](creating-push-model-aware-applications.md)">プッシュ モデルの対応アプリケーションを作成する</a>、ただしします。</p></td>
</tr>
<tr class="even">
<td><p><strong>イベント</strong></p></td>
<td><p>静止画像デバイス イベントの一覧を表示するベンダーから提供されたデータのセクションを識別します。 このセクションでは、各エントリには、次の形式が必要です。</p>
<p><em>EventName</em><strong>=&quot;</strong><em>文字列</em><strong>&quot;、{</strong><em>GUID</em> <strong>}、</strong>アプリ</p>
<p><em>EventName</em>イベント&#39;の内部の名前、<em>文字列</em>イベントは、&#39;s 表示文字列、 <em>GUID</em>イベントは、&#39;s GUID (を参照してください<a href="still-image-device-events.md" data-raw-source="[Still Image Device Events](still-image-device-events.md)">イメージ デバイスでもイベント</a>)、および<em>アプリ</em>イベントの発生時に起動されるようにイメージング アプリケーションを指定します。 現在登録されているアプリケーションを起動するには、アスタリスクを使用して、(<strong>*</strong>) の<em>アプリ</em>します。</p></td>
<td><p>(省略可能)。 このエントリが必要です。<a href="creating-push-model-aware-applications.md" data-raw-source="[Creating Push-Model Aware Applications](creating-push-model-aware-applications.md)">プッシュ モデルの対応アプリケーションを作成する</a>、ただしします。</p></td>
</tr>
<tr class="odd">
<td><p><strong>UninstallSection</strong></p></td>
<td><p>通常を格納している INF セクションを指す<a href="https://msdn.microsoft.com/library/windows/hardware/ff547363" data-raw-source="[&lt;strong&gt;INF DelFiles directives&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff547363)"> <strong>INF DelFiles ディレクティブ</strong></a>と<a href="https://msdn.microsoft.com/library/windows/hardware/ff547374" data-raw-source="[&lt;strong&gt;INF DelReg directives&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff547374)"> <strong>INF してディレクティブ</strong></a>します。 このセクション内のエントリでは、次の形式があります。</p>
<p><strong>UninstallSection</strong><em>UninstallSectionName を =</em></p>
<p><em>UninstallSectionName</em>含んでいるセクションの名前を指定します<strong>Delfiles</strong>または<strong>して</strong>ディレクティブ。 注 Windows ファイル保護 (<a href="https://msdn.microsoft.com/library/windows/hardware/ff556347#wdkgloss-windows-file-protection--wfp-" data-raw-source="&lt;em&gt;Windows File Protection (WFP)&lt;/em&gt;"><em>Windows ファイル保護 (WFP)</em></a>) 可能性がありますを使用して指定されている場合でも、いくつかのファイルを削除してからユーザーを禁止<strong>DelFiles</strong>ディレクティブ。</p></td>
<td><p>(省略可能)。 このエントリは、Windows 2000 でのみ有効です。</p></td>
</tr>
</tbody>
</table>

既定クラスのインストーラーを静止画像デバイス標準をサポートする[ **INF CopyFiles ディレクティブ**](https://msdn.microsoft.com/library/windows/hardware/ff546346)します。 インストーラーは、アンインストール操作中にいくつかのデバイスで共有されるファイルが途中で削除されないようにコンポーネントのファイルの内部参照カウンターを使用します。

まだのイメージのデバイスの既定の INF ファイル*sti.inf*デバイスの種類ごとに 2 つのインストール セクションを次のように定義します。

- [ **INF DDInstall セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547344)、内で参照されている必要があります、 *DDInstall*のベンダーから提供された INF ファイルの次の表に示すようにします。

    <table>
    <colgroup>
    <col width="33%" />
    <col width="33%" />
    <col width="33%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>USB デバイス</th>
    <th>SCSI デバイス</th>
    <th>シリアル デバイス</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><pre space="preserve"><code>Include=sti.inf</code></pre>
    <pre space="preserve"><code>Needs=STI.USBSection</code></pre></td>
    <td><pre space="preserve"><code>Include=sti.inf</code></pre>
    <pre space="preserve"><code>Needs=STI.SCSISection</code></pre></td>
    <td><pre space="preserve"><code>Include=sti.inf</code></pre>
    <pre space="preserve"><code>Needs=STI.SerialSection</code></pre></td>
    </tr>
    </tbody>
    </table>

- [ **INF DDInstall.Services セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547349)、内で参照されている必要があります、 *DDInstall*.**サービス**のベンダーから提供された INF ファイルの次の表に示すようにします。

    <table>
    <colgroup>
    <col width="33%" />
    <col width="33%" />
    <col width="33%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>USB デバイス</th>
    <th>SCSI デバイス</th>
    <th>シリアル デバイス</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><pre space="preserve"><code>Include=sti.inf</code></pre>
    <pre space="preserve"><code>Needs=STI.USBSection.Services</code></pre></td>
    <td><pre space="preserve"><code>Include=sti.inf</code></pre>
    <pre space="preserve"><code>Needs=STI.SCSISection.Services</code></pre></td>
    <td><pre space="preserve"><code>Include=sti.inf</code></pre>
    <pre space="preserve"><code>Needs=STI.SerialSection.Services</code></pre></td>
    </tr>
    </tbody>
    </table>

また場合[イメージの取得 Api のデバイスに固有のコンポーネントを作成する](creating-device-specific-components-for-image-acquisition-apis.md)、INF ファイルでこれらのコンポーネントのファイル名を含めるは通常。

静止画像デバイスの INF ファイルを作成する追加のガイダンスについては、エントリが含まれている Windows で提供される任意の INF ファイルを表示できる"サブクラス StillImage ="。

## <a name="remarks"></a>注釈

スキャナー、INF ファイルを開発するときに使用できます[Microsoft OS ディスクリプター](https://msdn.microsoft.com/library/windows/hardware/gg463179.aspx)互換性 ID 機能を有効にします。 これを行う場合は、複数のスキャナー モデルと互換性がある 1 つのスキャナー ドライバーを許可します。
