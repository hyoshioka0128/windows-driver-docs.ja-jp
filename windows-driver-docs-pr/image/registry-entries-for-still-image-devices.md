---
title: 静止イメージデバイスのレジストリエントリ
description: 静止イメージデバイスのレジストリエントリ
ms.assetid: cedc8afc-54c4-485e-989c-481fe30d899b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e6534f3acdd55c0f4d7fa029b4367bb3344ce6f4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840756"
---
# <a name="registry-entries-for-still-image-devices"></a>静止イメージデバイスのレジストリエントリ





Microsoft STI ではいくつかのレジストリエントリを使用しますが、その一部はベンダーが提供するコンポーネントによって変更できます。

### <a href="" id="ddk-vendor-modifiable-registry-values-si"></a>ベンダーが変更可能なレジストリ値

次の表に、定義済みのレジストリ値の名前とその意味を示します。 定数は、その*中に定義*されています。 デバイスで静止イメージ[プッシュモデル](creating-push-model-aware-applications.md)がサポートされている場合は、値を "tw" に割り当てる必要があります。 他の名前の値は省略可能です。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>常時</th>
<th>値の名前文字列</th>
<th>定義</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>STI_DEVICE_VALUE_ICM_PROFILE</p></td>
<td><p>"ICMProfile"</p></td>
<td><p>デバイスの ICM プロファイルの名前を含む REG_MULTI_SZ 型。</p></td>
</tr>
<tr class="even">
<td><p>STI_DEVICE_VALUE_ISIS_NAME</p></td>
<td><p>"ISISDriverName"</p></td>
<td><p>"Pxn" など、デバイスの ISIS ドライバー名を含む REG_SZ 型。</p></td>
</tr>
<tr class="odd">
<td><p>STI_DEVICE_VALUE_TIMEOUT</p></td>
<td><p>"PollTimeout"</p></td>
<td><p>デバイスをポーリングするときに使用するタイムアウト値をミリ秒単位で表す REG_DWORD 型。 既定値は 1000 (1 秒) です。</p></td>
</tr>
<tr class="even">
<td><p>STI_DEVICE_VALUE_TWAIN_NAME</p></td>
<td><p>"Tw"</p></td>
<td><p>"HP PictureScan 3.0" など、デバイスの TWAIN データソースの名前が付いた REG_SZ 型。</p></td>
</tr>
</tbody>
</table>

 

**StillImage** COM インターフェイスのクライアントは、 [**IStillImage:: setdevicevalue**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff543801(v=vs.85))と[**IStillImage:: getdevicevalue**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff543786(v=vs.85))を呼び出してレジストリを参照する必要があります。 静止画像ミニドライバーは、ミニドライバーの[**i:: Initialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-initialize)メソッドによって受信されたレジストリキーを指定して、WIN32 registry API を呼び出すことができます。 定義済みのレジストリエントリの値は[、INF ファイル](inf-files-for-still-image-devices.md)内から設定することもできます。

### <a name="customized-registry-values"></a>カスタマイズされたレジストリ値

静止画像アプリケーションとミニドライバーは、カスタマイズされたデバイス固有の値をレジストリに格納することもできます。 たとえば、カスタマイズされたプロパティシートページから取得したユーザー選択は、"UserSettings" サブキーの下に格納される可能性があります。

また、カスタマイズされたレジストリエントリの値は、 **Devicedata**エントリを含めることによって、 [INF ファイル](inf-files-for-still-image-devices.md)内から設定できます。

### <a href="" id="ddk-non-modifiable-registry-entries-si"></a>不変のレジストリエントリ

次の表に、ベンダーソフトウェアによって変更されないレジストリエントリを示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>レジストリ キー</th>
<th>定義</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>HKLM\SYSTEM\CurrentControlSet\Control\StillImage\Logging\STICLI</strong></p></td>
<td><p>どのベンダが生成したメッセージを静止画像ログファイルに書き込むかを指定します。 次のビットマスクの任意の組み合わせを指定できます。</p>
<p>0x1-情報メッセージ</p>
<p>0x2-警告メッセージ</p>
<p>0x4-エラーメッセージ</p>
<p>「 <a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff543807(v=vs.85)" data-raw-source="[&lt;strong&gt;IStillImage::WriteToErrorLog&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff543807(v=vs.85))"><strong>IStillImage:: WriteToErrorLog ログ</strong></a>」を参照してください。</p></td>
</tr>
<tr class="even">
<td><p><strong>HKLM\SYSTEM\CurrentControlSet\Control\StillImage\Logging\STIMON</strong></p></td>
<td><p>静止画像ログファイルに書き込むイベントモニタメッセージを指定します。 次のビットマスクの任意の組み合わせを指定できます。</p>
<p>0x1-情報メッセージ</p>
<p>0x2-警告メッセージ</p>
<p>0x4-エラーメッセージ</p></td>
</tr>
<tr class="odd">
<td><p><strong>HKLM\SYSTEM\CurrentControlSet\Control\Class{6BDD1FC6-810F-11D0-BEC7-08002BE2092F}</strong></p></td>
<td><p>インストールされている静止イメージデバイスに関する情報が含まれています。</p></td>
</tr>
<tr class="even">
<td><p><strong>HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\StillImage\Registered アプリケーション</strong></p></td>
<td><p>登録済みのイメージングアプリケーションの一覧が含まれています。</p></td>
</tr>
<tr class="odd">
<td><p><strong>HKLM\SYSTEM\CurrentControlSet\Control\DeviceClass{6bdd1fc6-810f-11d0-bec7-08002be2092f}</strong></p></td>
<td><p>インストールされている静止イメージデバイスインターフェイスについて説明します。</p></td>
</tr>
</tbody>
</table>

 

 

 




