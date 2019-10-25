---
title: WIA ドライバー コマンドのサポート
description: WIA ドライバー コマンドのサポート
ms.assetid: 9c552316-7dd6-4102-88d3-fab9732d1e5d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7784bb3fdcfc8eac3e76203a9abdde545a4de086
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840712"
---
# <a name="wia-driver-command-support"></a>WIA ドライバー コマンドのサポート





WIA デバイスコマンドは、(イメージングアプリケーションに代わって) wia サービスによって WIA ミニドライバーに送信される要求であり、特定のアクションを実行するように指示します。

ミニドライバーに発行できる WIA デバイスコマンドの一覧を次に示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>コマンド</th>
<th>意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WIA_CMD_CHANGE_DOCUMENT</p></td>
<td><p>次のドキュメントに移動します (multidocument スキャナーのみに発行されます)。</p></td>
</tr>
<tr class="even">
<td><p>WIA_CMD_DELETE_ALL_ITEMS</p></td>
<td><p>ドライバーの項目ツリーを削除します。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_CMD_DIAGNOSTIC</p></td>
<td><p>Microsoft によって予約されています。</p></td>
</tr>
<tr class="even">
<td><p>WIA_CMD_SYNCHRONIZE</p></td>
<td><p>ドライバーの項目ツリーを再構築します。 すべてのミニドライバーがこのコマンドをサポートする必要があります。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_CMD_TAKE_PICTURE</p></td>
<td><p>画像を撮影します (カメラにのみ発行されます)。</p></td>
</tr>
<tr class="even">
<td><p>WIA_CMD_UNLOAD_DOCUMENT</p></td>
<td><p>現在のドキュメントをアンロードします (multidocument スキャナーのみに発行されます)。</p></td>
</tr>
</tbody>
</table>

 

WIA\_CMD\_XXX コマンドについては、Microsoft Windows SDK のドキュメントを参照してください。 コマンドの独自のカスタムリストを含めることができます。

### <a name="adding-device-command-support"></a>デバイスコマンドサポートの追加

デバイスコマンドを報告するように WIA ミニドライバーを適切に設定するには、 [**IWiaMiniDrv::D rvgetcapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvgetcapabilities)メソッドでサポートされているコマンドの配列を報告します。 **IWiaMiniDrv::D rvgetcapabilities**メソッドの実装例については、「[割り込みイベントのサポートの追加](adding-interrupt-event-support.md)」を参照してください。

### <a name="implementing-the-iwiaminidrvdrvdevicecommand-method"></a>IWiaMiniDrv::d rvDeviceCommand メソッドの実装

WIA サービスは、アプリケーションの**Iwiaitem::D evicecommand**メソッドへの呼び出しに応答して[**IWiaMiniDrv::d rvdevicecommand**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvdevicecommand)メソッドを呼び出します (Microsoft Windows SDK のドキュメントを参照)。 **IWiaMiniDrv::D rvdevicecommand**メソッドでは、次のタスクを実行する必要があります。

1.  送信されたコマンドがサポートされているコマンドであるかどうかを判断します。

2.  コマンド要求を処理します。

WIA ドライバーは、 *Pwiascontext*ポインターを使用して、デバイスコマンドを受信する wia 項目を決定する必要があります。 その後、WIA ドライバーは、受信した WIA 項目を対象とした受信デバイスコマンドを処理する必要があります。 サポートされていない WIA ドライバーに送信されたコマンドは、E\_INVALIDARG エラーコードで失敗する必要があります。

**IWiaMiniDrv::D rvdevicecommand**メソッドの実装例については、「[項目ツリーの変更をアプリケーションに通知](informing-an-application-of-item-tree-changes.md)する」を参照してください。
