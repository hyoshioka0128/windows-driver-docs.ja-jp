---
title: 静止画像デバイスのレジストリ エントリ
description: 静止画像デバイスのレジストリ エントリ
ms.assetid: cedc8afc-54c4-485e-989c-481fe30d899b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f120ca40fcee1610b2c87269e4619c955b421788
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374287"
---
# <a name="registry-entries-for-still-image-devices"></a>静止画像デバイスのレジストリ エントリ





Microsoft STI のうちいくつかはベンダーから提供されたコンポーネントで変更できる、いくつかのレジストリ エントリを使用します。

### <a href="" id="ddk-vendor-modifiable-registry-values-si"></a>仕入先が変更可能なレジストリ値

次の表は、定義済みのレジストリ値の名前とその意味を示します。 定数で定義されて*stireg.h*します。 値は、デバイスは、静止画像をサポートしている場合、"TwainDS"に割り当てる必要があります[プッシュ モデル](creating-push-model-aware-applications.md)します。 その他の名前の値は省略可能です。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>定数</th>
<th>値名の文字列</th>
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
<td><p>"Epson.pxn"などのデバイスのイシス ドライバー名を含む REG_SZ 型。</p></td>
</tr>
<tr class="odd">
<td><p>STI_DEVICE_VALUE_TIMEOUT</p></td>
<td><p>"PollTimeout"</p></td>
<td><p>デバイスをポーリングするときに使用されるミリ秒単位のタイムアウト値を表す REG_DWORD 型。 既定値は 1000 (1 秒) です。</p></td>
</tr>
<tr class="even">
<td><p>STI_DEVICE_VALUE_TWAIN_NAME</p></td>
<td><p>"TwainDS"</p></td>
<td><p>"HP PictureScan 3.0"などのデバイスの TWAIN データ ソースの表示可能な名前を含む REG_SZ 型。</p></td>
</tr>
</tbody>
</table>

 

クライアント、 **StillImage** COM インターフェイスを呼び出す必要があります[ **IStillImage::SetDeviceValue** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff543801(v=vs.85))と[ **IStillImage::GetDeviceValue** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff543786(v=vs.85))レジストリを参照します。 イメージのミニドライバーが Win32 レジストリ ミニドライバーが受信したレジストリ キーを指定する API を呼び出すことができますも[ **IStiUSD::Initialize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-initialize)メソッド。 内から定義済みのレジストリ エントリの値を設定することも[INF ファイル](inf-files-for-still-image-devices.md)します。

### <a name="customized-registry-values"></a>カスタマイズされたレジストリ値

アプリケーションの静止画像し、ミニドライバーが、カスタマイズされた、デバイスに固有の値をレジストリに保存することもできます。 たとえば、カスタマイズされたプロパティ シートのページから取得したユーザーの選択は、"UserSettings"サブキーの下に格納できます。

カスタマイズされたレジストリ エントリの値を設定して、内からさらに、 [INF ファイル](inf-files-for-still-image-devices.md)を含めることによって、 **DeviceData**エントリ。

### <a href="" id="ddk-non-modifiable-registry-entries-si"></a>変更不可能なレジストリ エントリ

次の表は、ベンダーのソフトウェアでは変更しないでくださいレジストリ エントリを一覧表示します。

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
<td><p>ベンダーによって生成されたメッセージが静止画像のログ ファイルに記述されたを指定します。 次のビットマスクの任意の組み合わせを指定できます。</p>
<p>0x1 - 情報メッセージ</p>
<p>0x2 - 警告メッセージ</p>
<p>0x4 - エラー メッセージ</p>
<p>参照してください<a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff543807(v=vs.85)" data-raw-source="[&lt;strong&gt;IStillImage::WriteToErrorLog&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff543807(v=vs.85))"> <strong>IStillImage::WriteToErrorLog</strong></a>します。</p></td>
</tr>
<tr class="even">
<td><p><strong>HKLM\SYSTEM\CurrentControlSet\Control\StillImage\Logging\STIMON</strong></p></td>
<td><p>どのイベント メッセージの監視が静止画像のログ ファイルに書き込まれるを指定します。 次のビットマスクの任意の組み合わせを指定できます。</p>
<p>0x1 - 情報メッセージ</p>
<p>0x2 - 警告メッセージ</p>
<p>0x4 - エラー メッセージ</p></td>
</tr>
<tr class="odd">
<td><p><strong>HKLM\SYSTEM\CurrentControlSet\Control\Class{6BDD1FC6-810F-11D0-BEC7-08002BE2092F}</strong></p></td>
<td><p>インストールされているデバイスの静止画像に関する情報が含まれています。</p></td>
</tr>
<tr class="even">
<td><p><strong>HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\StillImage\Registered Applications</strong></p></td>
<td><p>登録済みのイメージング アプリケーションの一覧が含まれています。</p></td>
</tr>
<tr class="odd">
<td><p><strong>HKLM\SYSTEM\CurrentControlSet\Control\DeviceClass{6bdd1fc6-810f-11d0-bec7-08002be2092f}</strong></p></td>
<td><p>インストール済みの静止画像デバイス インターフェイスに関する情報が含まれています。</p></td>
</tr>
</tbody>
</table>

 

 

 




