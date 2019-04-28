---
title: IWiaMiniDrv COM インターフェイス
ms.assetid: a4bd0dee-fb40-42d4-a235-9dab3bc84017
description: このトピックで IWiaMiniDrv COM インターフェイスの使用に関する詳細なガイダンスを提供します
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c50ca3271d97ba61cf381660e414438bc85f07d4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63381812"
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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543958" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvAnalyzeItem&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543958)"><strong>IWiaMiniDrv::drvAnalyzeItem</strong></a></p></td>
<td><p>項目を検査し、必要に応じて、サブ項目を作成します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff544986" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvInitializeWia&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544986)"><strong>IWiaMiniDrv::drvInitializeWia</strong></a></p></td>
<td><p>WIA ミニドライバーを初期化します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff544989" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvInitItemProperties&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544989)"><strong>IWiaMiniDrv::drvInitItemProperties</strong></a></p></td>
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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543961" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvDeleteItem&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543961)"><strong>IWiaMiniDrv::drvDeleteItem</strong></a></p></td>
<td><p>ドライバーの項目を削除します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543972" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvFreeDrvItemContext&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543972)"><strong>IWiaMiniDrv::drvFreeDrvItemContext</strong></a></p></td>
<td><p>デバイス固有のコンテキストを解放します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff545010" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvUnInitializeWia&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545010)"><strong>IWiaMiniDrv::drvUnInitializeWia</strong></a></p></td>
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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543977" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvGetCapabilities&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543977)"><strong>IWiaMiniDrv::drvGetCapabilities</strong></a></p></td>
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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543986" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvGetWiaFormatInfo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543986)"><strong>IWiaMiniDrv::drvGetWiaFormatInfo</strong></a></p></td>
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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543967" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvDeviceCommand&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543967)"><strong>IWiaMiniDrv::drvDeviceCommand</strong></a></p></td>
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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff544995" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvLockWiaDevice&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544995)"><strong>IWiaMiniDrv::drvLockWiaDevice</strong></a></p></td>
<td><p>イメージング デバイスへのアクセスをロックします。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff545012" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvUnLockWiaDevice&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545012)"><strong>IWiaMiniDrv::drvUnLockWiaDevice</strong></a></p></td>
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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff544998" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvNotifyPnPEvent&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544998)"><strong>IWiaMiniDrv::drvNotifyPnPEvent</strong></a></p></td>
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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543982" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvGetDeviceErrorStr&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543982)"><strong>IWiaMiniDrv::drvGetDeviceErrorStr</strong></a></p></td>
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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff545005" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvReadItemProperties&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545005)"><strong>IWiaMiniDrv::drvReadItemProperties</strong></a></p></td>
<td><p>ドライバーの項目のプロパティを読み取ります。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff545017" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvValidateItemProperties&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545017)"><strong>IWiaMiniDrv::drvValidateItemProperties</strong></a></p></td>
<td><p>ドライバーの項目のプロパティを検証します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff545020" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvWriteItemProperties&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545020)"><strong>IWiaMiniDrv::drvWriteItemProperties</strong></a></p></td>
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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543956" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvAcquireItemData&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543956)"><strong>IWiaMiniDrv::drvAcquireItemData</strong></a></p></td>
<td><p>ドライバーの項目から WIA サービスにデータを転送します。</p></td>
</tr>
</tbody>
</table>
