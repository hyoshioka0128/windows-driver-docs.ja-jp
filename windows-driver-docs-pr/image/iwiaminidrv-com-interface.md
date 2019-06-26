---
title: IWiaMiniDrv COM インターフェイス
ms.assetid: a4bd0dee-fb40-42d4-a235-9dab3bc84017
description: このトピックで IWiaMiniDrv COM インターフェイスの使用に関する詳細なガイダンスを提供します
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2bab076da873671ca8d32a45ae0cdfc6c59932af
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378880"
---
# <a name="iwiaminidrv-com-interface"></a>IWiaMiniDrv COM インターフェイス

イメージング アプリケーションでは、ライター実装ミニドライバーを介してデバイス ミニドライバーと通信してさらに WIA サービスに対して要求を行う[IWiaMiniDrv インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nn-wiamindr_lh-iwiaminidrv)します。 アプリケーションは、通常要求を行います。

- [作成して、項目の初期化](#creating-and-initializing-items)
- [項目の削除](#deleting-items)
- [デバイスの機能を列挙します。](#enumerating-device-capabilities)
- [形式のイメージを列挙します。](#enumerating-image-formats)
- [デバイス コマンドの発行](#issuing-device-commands)
- [ロックと、デバイスをロック解除](#locking-and-unlocking-a-device)
- [イベントのデバイスへの通知](#notifying-a-device-of-an-event)
- [デバイスのエラー文字列を取得します。](#obtaining-device-error-strings)
- [読み取りと、アイテムのプロパティを格納します。](#reading-and-storing-item-properties)
- [データを転送します。](#transferring-data)

アプリケーションでは、WIA アプリケーション プログラミング インターフェイス (API) を通じて WIA サービスに要求を行います。 このインターフェイスの詳細については、Microsoft Windows SDK のドキュメントを参照してください。

**IWiaMiniDrv**インターフェイスには、デバイスを制御、WIA サービスについては、次の表に示すように、エントリ ポイントが用意されています。 WIA ミニドライバーを実装する必要がありますすべて**IWiaMiniDrv**メソッド。 これらのエントリ ポイントは、次で定義されて**IWiaMiniDrv**メソッド。

## <a name="creating-and-initializing-items"></a>作成して、項目の初期化

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvanalyzeitem" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvAnalyzeItem&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvanalyzeitem)"><strong>IWiaMiniDrv::drvAnalyzeItem</strong></a></p></td>
<td><p>項目を検査し、必要に応じて、サブ項目を作成します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvinitializewia" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvInitializeWia&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvinitializewia)"><strong>IWiaMiniDrv::drvInitializeWia</strong></a></p></td>
<td><p>WIA ミニドライバーを初期化します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvinititemproperties" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvInitItemProperties&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvinititemproperties)"><strong>IWiaMiniDrv::drvInitItemProperties</strong></a></p></td>
<td><p>ドライバー アプリケーション項目のツリー内の各項目の項目のプロパティを初期化します。</p></td>
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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvdeleteitem" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvDeleteItem&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvdeleteitem)"><strong>IWiaMiniDrv::drvDeleteItem</strong></a></p></td>
<td><p>ドライバーの項目を削除します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvfreedrvitemcontext" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvFreeDrvItemContext&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvfreedrvitemcontext)"><strong>IWiaMiniDrv::drvFreeDrvItemContext</strong></a></p></td>
<td><p>デバイス固有のコンテキストを解放します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvuninitializewia" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvUnInitializeWia&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvuninitializewia)"><strong>IWiaMiniDrv::drvUnInitializeWia</strong></a></p></td>
<td><p>アプリケーション項目のツリーに関連付けられているデバイスのリソースを解放します。</p></td>
</tr>
</tbody>
</table>

## <a name="enumerating-device-capabilities"></a>デバイスの機能を列挙します。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvgetcapabilities" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvGetCapabilities&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvgetcapabilities)"><strong>IWiaMiniDrv::drvGetCapabilities</strong></a></p></td>
<td><p>WIA ミニドライバーでサポートされるコマンドとイベントを報告します。</p></td>
</tr>
</tbody>
</table>

## <a name="enumerating-image-formats"></a>形式のイメージを列挙します。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvgetwiaformatinfo" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvGetWiaFormatInfo&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvgetwiaformatinfo)"><strong>IWiaMiniDrv::drvGetWiaFormatInfo</strong></a></p></td>
<td><p>取得には、形式とメディアの種類のデバイスがサポートされています。</p></td>
</tr>
</tbody>
</table>

## <a name="issuing-device-commands"></a>デバイス コマンドの発行

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvdevicecommand" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvDeviceCommand&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvdevicecommand)"><strong>IWiaMiniDrv::drvDeviceCommand</strong></a></p></td>
<td><p>イメージングのデバイスにコマンドを発行します。</p></td>
</tr>
</tbody>
</table>

## <a name="locking-and-unlocking-a-device"></a>ロックと、デバイスをロック解除

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvlockwiadevice" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvLockWiaDevice&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvlockwiadevice)"><strong>IWiaMiniDrv::drvLockWiaDevice</strong></a></p></td>
<td><p>イメージング デバイスへのアクセスをロックします。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvunlockwiadevice" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvUnLockWiaDevice&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvunlockwiadevice)"><strong>IWiaMiniDrv::drvUnLockWiaDevice</strong></a></p></td>
<td><p>イメージング デバイスへのアクセスのロックを解除します。</p></td>
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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvnotifypnpevent" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvNotifyPnPEvent&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvnotifypnpevent)"><strong>IWiaMiniDrv::drvNotifyPnPEvent</strong></a></p></td>
<td><p>プラグ アンド プレイのイベントに WIA ミニドライバーの応答を示します。</p></td>
</tr>
</tbody>
</table>

## <a name="obtaining-device-error-strings"></a>デバイスのエラー文字列を取得します。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvgetdeviceerrorstr" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvGetDeviceErrorStr&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvgetdeviceerrorstr)"><strong>IWiaMiniDrv::drvGetDeviceErrorStr</strong></a></p></td>
<td><p>デバイスのエラー値を文字列にマップします。</p></td>
</tr>
</tbody>
</table>

## <a name="reading-and-storing-item-properties"></a>読み取りと、アイテムのプロパティを格納します。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvreaditemproperties" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvReadItemProperties&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvreaditemproperties)"><strong>IWiaMiniDrv::drvReadItemProperties</strong></a></p></td>
<td><p>ドライバーの項目のプロパティを読み取ります。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvvalidateitemproperties" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvValidateItemProperties&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvvalidateitemproperties)"><strong>IWiaMiniDrv::drvValidateItemProperties</strong></a></p></td>
<td><p>ドライバーの項目のプロパティを検証します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvwriteitemproperties" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvWriteItemProperties&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvwriteitemproperties)"><strong>IWiaMiniDrv::drvWriteItemProperties</strong></a></p></td>
<td><p>(必要な) 場合、ドライバーの項目のプロパティをデバイスに書き込みます。</p></td>
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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvAcquireItemData&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata)"><strong>IWiaMiniDrv::drvAcquireItemData</strong></a></p></td>
<td><p>ドライバーの項目から WIA サービスにデータを転送します。</p></td>
</tr>
</tbody>
</table>
