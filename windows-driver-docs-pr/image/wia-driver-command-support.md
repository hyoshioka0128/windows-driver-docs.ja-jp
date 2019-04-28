---
title: WIA ドライバー コマンドのサポート
description: WIA ドライバー コマンドのサポート
ms.assetid: 9c552316-7dd6-4102-88d3-fab9732d1e5d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1b9346832723f38f7bbf10784807153abe7cc0cf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366918"
---
# <a name="wia-driver-command-support"></a>WIA ドライバー コマンドのサポート





WIA デバイス コマンドは、WIA ミニドライバーは、特定のアクションを実行するように指示する (イメージング アプリケーション) に代わって、WIA サービスによって送信される要求です。

WIA デバイス コマンドを発行すると、ミニドライバーの一覧を次には。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>コマンド</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WIA_CMD_CHANGE_DOCUMENT</p></td>
<td><p>次のドキュメント (複数ドキュメントのみをスキャナーに発行された) に変更します。</p></td>
</tr>
<tr class="even">
<td><p>WIA_CMD_DELETE_ALL_ITEMS</p></td>
<td><p>ドライバーの項目のツリーを削除します。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_CMD_DIAGNOSTIC</p></td>
<td><p>Microsoft によって予約されています。</p></td>
</tr>
<tr class="even">
<td><p>WIA_CMD_SYNCHRONIZE</p></td>
<td><p>ドライバーの項目のツリーを再構築します。 すべてのミニドライバーは、このコマンドをサポートする必要があります。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_CMD_TAKE_PICTURE</p></td>
<td><p>(カメラのみを発行) を撮影します。</p></td>
</tr>
<tr class="even">
<td><p>WIA_CMD_UNLOAD_DOCUMENT</p></td>
<td><p>(複数ドキュメントのみをスキャナーに発行された) 現在のドキュメントをアンロードします。</p></td>
</tr>
</tbody>
</table>

 

WIA\_CMD\_XXX コマンドが、Microsoft Windows SDK ドキュメントに記載されています。 コマンドの独自のカスタム リストを含めることができます。

### <a name="adding-device-command-support"></a>デバイス コマンドのサポートを追加します。

To device コマンドのレポート、WIA ミニドライバーを正しく設定するには、レポートでサポートされているコマンドの配列、 [ **IWiaMiniDrv::drvGetCapabilities** ](https://msdn.microsoft.com/library/windows/hardware/ff543977)メソッド。 実装例については、 **IWiaMiniDrv::drvGetCapabilities**メソッドを参照してください[中断イベントのサポートを追加する](adding-interrupt-event-support.md)します。

### <a name="implementing-the-iwiaminidrvdrvdevicecommand-method"></a>IWiaMiniDrv::drvDeviceCommand メソッドを実装します。

WIA サービスの呼び出し、 [ **IWiaMiniDrv::drvDeviceCommand** ](https://msdn.microsoft.com/library/windows/hardware/ff543967)メソッドへのアプリケーションの呼び出しに応答、 **IWiaItem::DeviceCommand**メソッド (で説明されている、Microsoft Windows SDK のドキュメント)。 **IWiaMiniDrv::drvDeviceCommand**メソッドは、次のタスクを実行する必要があります。

1.  送信されたコマンドがサポートされているコマンドであるかどうかを確認します。

2.  コマンドの要求を処理します。

WIA ドライバーを使用して、デバイス コマンドを受信する WIA アイテムを確認する必要があります、 *pWiasContext*ポインター。 さらに、WIA ドライバーは、受信 WIA 項目を対象とした受信デバイス コマンドを処理する必要があります。 サポートされていない、WIA ドライバーに送信される任意のコマンドは、E で失敗する必要があります\_INVALIDARG エラー コード。

実装例については、 **IWiaMiniDrv::drvDeviceCommand**メソッドを参照してください[、アプリケーションのアイテム ツリーの変更を通知](informing-an-application-of-item-tree-changes.md)します。
