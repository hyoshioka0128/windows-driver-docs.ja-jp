---
title: IWiaMiniDrv COM インターフェイス
ms.assetid: a4bd0dee-fb40-42d4-a235-9dab3bc84017
description: このトピックでは、IWiaMiniDrv COM インターフェイスの使用に関する詳細なガイダンスを提供します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ffb62890d59f1650b51a7be457cb4083bfd0b218
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840796"
---
# <a name="iwiaminidrv-com-interface"></a>IWiaMiniDrv COM インターフェイス

イメージングアプリケーションは、ミニドライバー writer で実装された[IWiaMiniDrv インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nn-wiamindr_lh-iwiaminidrv)を介してデバイスミニドライバーと通信する WIA サービスに対して要求を行います。 通常、アプリケーションは次の要求を行います。

- [項目の作成と初期化](#creating-and-initializing-items)
- [項目の削除](#deleting-items)
- [デバイスの機能を列挙する](#enumerating-device-capabilities)
- [画像形式の列挙](#enumerating-image-formats)
- [デバイスコマンドの発行](#issuing-device-commands)
- [デバイスのロックとロック解除](#locking-and-unlocking-a-device)
- [イベントのデバイスへの通知](#notifying-a-device-of-an-event)
- [デバイスエラー文字列の取得](#obtaining-device-error-strings)
- [項目のプロパティの読み取りと格納](#reading-and-storing-item-properties)
- [データの転送](#transferring-data)

アプリケーションは、WIA アプリケーションプログラミングインターフェイス (API) を使用して、WIA サービスに要求を行います。 このインターフェイスの詳細については、Microsoft Windows SDK のドキュメントを参照してください。

**IWiaMiniDrv**インターフェイスは、WIA サービスがデバイスを制御するための次の表に示すエントリポイントを提供します。 WIA ミニドライバーは、すべての**IWiaMiniDrv**メソッドを実装する必要があります。 これらのエントリポイントは、次の**IWiaMiniDrv**メソッドを使用して定義されます。

## <a name="creating-and-initializing-items"></a>項目の作成と初期化

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>メソッド</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvanalyzeitem" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvAnalyzeItem&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvanalyzeitem)"><strong>IWiaMiniDrv::d rvAnalyzeItem</strong></a></p></td>
<td><p>項目を検査し、必要に応じてサブ項目を作成します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvinitializewia" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvInitializeWia&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvinitializewia)"><strong>IWiaMiniDrv::d rvInitializeWia</strong></a></p></td>
<td><p>WIA ミニドライバーを初期化します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvinititemproperties" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvInitItemProperties&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvinititemproperties)"><strong>IWiaMiniDrv::d rvInitItemProperties</strong></a></p></td>
<td><p>アプリケーション項目ツリー内の各項目のドライバー項目のプロパティを初期化します。</p></td>
</tr>
</tbody>
</table>

## <a name="deleting-items"></a>項目の削除

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>メソッド</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvdeleteitem" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvDeleteItem&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvdeleteitem)"><strong>IWiaMiniDrv::d rvDeleteItem</strong></a></p></td>
<td><p>ドライバー項目を削除します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvfreedrvitemcontext" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvFreeDrvItemContext&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvfreedrvitemcontext)"><strong>IWiaMiniDrv::d rvFreeDrvItemContext</strong></a></p></td>
<td><p>デバイス固有のコンテキストを解放します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvuninitializewia" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvUnInitializeWia&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvuninitializewia)"><strong>IWiaMiniDrv::d rvUnInitializeWia</strong></a></p></td>
<td><p>アプリケーション項目ツリーに関連付けられているデバイスリソースを解放します。</p></td>
</tr>
</tbody>
</table>

## <a name="enumerating-device-capabilities"></a>デバイスの機能を列挙する

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>メソッド</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvgetcapabilities" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvGetCapabilities&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvgetcapabilities)"><strong>IWiaMiniDrv::d rvGetCapabilities</strong></a></p></td>
<td><p>WIA ミニドライバーでサポートされているイベントとコマンドを報告します。</p></td>
</tr>
</tbody>
</table>

## <a name="enumerating-image-formats"></a>画像形式の列挙

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>メソッド</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvgetwiaformatinfo" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvGetWiaFormatInfo&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvgetwiaformatinfo)"><strong>IWiaMiniDrv::d rvGetWiaFormatInfo</strong></a></p></td>
<td><p>サポートされているデバイス形式とメディアの種類を取得します。</p></td>
</tr>
</tbody>
</table>

## <a name="issuing-device-commands"></a>デバイスコマンドの発行

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>メソッド</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvdevicecommand" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvDeviceCommand&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvdevicecommand)"><strong>IWiaMiniDrv::d rvDeviceCommand</strong></a></p></td>
<td><p>イメージングデバイスにコマンドを発行します。</p></td>
</tr>
</tbody>
</table>

## <a name="locking-and-unlocking-a-device"></a>デバイスのロックとロック解除

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>メソッド</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvlockwiadevice" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvLockWiaDevice&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvlockwiadevice)"><strong>IWiaMiniDrv::d rvLockWiaDevice</strong></a></p></td>
<td><p>イメージングデバイスへのアクセスをロックします。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvunlockwiadevice" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvUnLockWiaDevice&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvunlockwiadevice)"><strong>IWiaMiniDrv::d rvUnLockWiaDevice</strong></a></p></td>
<td><p>イメージングデバイスへのアクセスのロックを解除します。</p></td>
</tr>
</tbody>
</table>

## <a name="notifying-a-device-of-an-event"></a>イベントのデバイスへの通知

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>メソッド</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvnotifypnpevent" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvNotifyPnPEvent&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvnotifypnpevent)"><strong>IWiaMiniDrv::d rvNotifyPnPEvent</strong></a></p></td>
<td><p>プラグアンドプレイイベントに対する WIA ミニドライバーの応答を示します。</p></td>
</tr>
</tbody>
</table>

## <a name="obtaining-device-error-strings"></a>デバイスエラー文字列の取得

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>メソッド</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvgetdeviceerrorstr" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvGetDeviceErrorStr&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvgetdeviceerrorstr)"><strong>IWiaMiniDrv::d rvGetDeviceErrorStr</strong></a></p></td>
<td><p>デバイスエラー値を文字列にマップします。</p></td>
</tr>
</tbody>
</table>

## <a name="reading-and-storing-item-properties"></a>項目のプロパティの読み取りと格納

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>メソッド</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvreaditemproperties" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvReadItemProperties&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvreaditemproperties)"><strong>IWiaMiniDrv::d rvReadItemProperties</strong></a></p></td>
<td><p>ドライバー項目のプロパティを読み取ります。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvvalidateitemproperties" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvValidateItemProperties&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvvalidateitemproperties)"><strong>IWiaMiniDrv::d rvValidateItemProperties</strong></a></p></td>
<td><p>ドライバー項目のプロパティを検証します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvwriteitemproperties" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvWriteItemProperties&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvwriteitemproperties)"><strong>IWiaMiniDrv::d rvWriteItemProperties</strong></a></p></td>
<td><p>必要に応じて、ドライバー項目のプロパティをデバイスに書き込みます。</p></td>
</tr>
</tbody>
</table>

## <a name="transferring-data"></a>データの転送

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>メソッド</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvAcquireItemData&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata)"><strong>IWiaMiniDrv::d rvAcquireItemData</strong></a></p></td>
<td><p>ドライバー項目から WIA サービスにデータを転送します。</p></td>
</tr>
</tbody>
</table>
