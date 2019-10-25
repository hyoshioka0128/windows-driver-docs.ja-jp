---
title: Windows Me および Windows XP のドキュメント フィーダー サポートの追加
description: Windows Me および Windows XP のドキュメント フィーダー サポートの追加
ms.assetid: f3be94fa-6fb7-45de-a3ce-f3d173e802cf
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6aa09bef818282a8a0ca8b298b6327e8beedeecf
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840910"
---
# <a name="adding-document-feeder-support"></a>ドキュメントフィーダーサポートの追加

ドキュメントフィーダーは、スキャナーに関連付けられているか、スキャナーに組み込まれているユニットで、スキャンする位置に用紙ドキュメントを自動的にフィードします。 ドキュメントフィーダーを備えたスキャナーでは、次の一覧に示すプロパティを追加することによって機能が公開され、制御されます。 Windows Me と Windows XP では、次のプロパティがルート項目に配置されています。

- [**WIA\_DPS\_横\_シート\_フィード\_サイズ**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-horizontal-sheet-feed-size)
- [**WIA\_DPS\_垂直\_シート\_フィード\_サイズ**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-vertical-sheet-feed-size)
- [**WIA\_DPS\_最小\_横\_シート\_フィード\_サイズ**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-min-horizontal-sheet-feed-size)
- [**WIA\_DPS\_最小\_垂直\_シート\_フィード\_サイズ**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-min-vertical-sheet-feed-size)
- [**WIA\_DPS\_シート\_フィーダー\_登録**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-sheet-feeder-registration)
- [**WIA\_DPS\_ドキュメント\_処理\_機能**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-document-handling-capabilities)
- [**WIA\_DPS\_ドキュメント\_\_の状態を処理する**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-document-handling-status)
- [**WIA\_DPS\_ドキュメント\_処理\_選択**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-document-handling-select)
- [**WIA\_DPS\_ページ**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-pages)

Windows Me と Windows XP では、次のオプションのドキュメントフィーダーのプロパティが子項目に配置されています。

- [**WIA\_DPS\_ページ\_サイズ**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-page-size)
- [**WIA\_DPS\_ページ\_幅**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-page-width)
- [**WIA\_DPS\_ページ\_の高さ**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-page-height)
- [**WIA\_IP\_方向**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-orientation)

デバイスにフラットベッド、ドキュメントフィーダー、および両面印刷装置が搭載されている場合、ドライバーは\_機能のプロパティを処理する\_\_ドキュメントを\_します。FLAT |DUP)。 WIA\_DPS\_ドキュメント\_処理\_選択の有効な値が正しく設定されていることを確認します。

たとえば、アプリケーションがドキュメントフィーダーから3ページの両面スキャンを実行するとします。 これを実現するために、アプリケーションは\_SELECT プロパティを処理\_、\_ドキュメントに対して、WIA\_DPS を設定します。また、[WIA\_DPS\_ページ] プロパティを3に設定します。 アプリケーションで最初にページの先頭をスキャンする場合は、WIA\_DPS\_ドキュメント\_処理\_SELECT プロパティを設定する必要があります (フィーダー |両面 |FRONT\_最初)。 この処理が完了すると、アプリケーションは、データ転送を要求する子項目に移動する必要があります。 ミニドライバーは、フィーダー内の最初のページの前をページ1、ページ2として、フィーダーの2ページ目をページ3として報告します。

デバイスがドキュメントフィーダーを持っている場合は、ドキュメントフィーダーのプロパティをサポートしている必要があることに注意してください。

## <a name="acquiring-data-from-a-document-feeder"></a>ドキュメントフィーダーからデータを取得する

スキャナーがドキュメントフィーダーからイメージを取得する場合、 [**IWiaMiniDrv::D rvacquireitemdata**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata)メソッドの実装にはいくつかの変更を加える必要があります。

1. アプリケーションは、ドキュメントフィーダーを使用したスキャンがスキャナーでサポートされているかどうかを判断するために、\_機能プロパティを処理する WIA\_DPS\_ドキュメント\_読み取ります。
1. アプリケーションは、\_SELECT プロパティを処理\_WIA\_DPS\_ドキュメントを読み取り、スキャナーがドキュメントフィーダーを使用してスキャンするように構成されているかどうかを判断します。
1. アプリケーションは、WIA\_DPS\_ドキュメント\_\_の状態を読み取ることによって、ドキュメントフィーダーに用紙があるかどうかを判断します。 フィーダーに用紙がない場合は、WIA\_DPS\_ドキュメント\_\_の状態を適切な状態コードに設定し、WIA\_エラーを返します\_用紙は IWiaMiniDrv から空で\_ **:** 取得が行われた直後に rvacquireitemdata を:d します。
1. スキャン動作を決定するには、WIA\_DPS\_ページのプロパティを確認します。 このプロパティが0の場合は、フィーダーが空になるまですべてのページをスキャンします。 正の値の場合は、[WIA\_DPS\_ページ] プロパティに含まれている値によって示されたページ数だけをスキャンします。
1. [**IWiaMiniDrvCallBack:: MiniDrvCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrvcallback-minidrvcallback)メソッドを呼び出すことにより、ループを制御し、継続的にスキャンし、WIA アプリケーションにデータを送信することで、要求された数のページをスキャンします。 これがどのように機能するかを次のコード例に示します。

    ```cpp
    for(int x=1; x=Pagecount; x++)
    {
        \\ Tell scanner to scan an image.
        \\ Receive image data from scanner.
        \\ Send the just-scanned image to the registered application.
    }
    ```

1. [**WIA\_IPA\_tymed**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-tymed)が tymed\_callback または tymed\_マルチページ\_コールバックに設定されている場合、1つのページがスキャンされた後、追加のメッセージ (メッセージ\_新しい\_ページ) を送信する必要があります。次のものをスキャンする前。 これを行うには、 [**Wiassendendofpage**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiassendendofpage)の WIA サービスユーティリティ関数を呼び出します。

ドキュメントフィーダードライバーが返すページ数は、WIA の\_DPS\_ページ プロパティの設定によって異なります。

## <a name="if-wia_dps_pages-is-zero"></a>WIA\_DPS\_ページがゼロの場合

1. スキャナーが最初のページをスキャンできない場合は、すぐにエラーコードを返します。 これには、紙詰まりや、スキャナーの用紙が不足している場合も含まれます。
1. スキャナーが最初のページを正常にスキャンし、スキャンを続行できても、用紙が不足している場合は、成功コード WIA\_STATUS\_\_メディアの終了\_を返します。 これは、転送が成功したことをアプリケーションに通知しますが、スキャナーの用紙が不足しています。 一部のアプリケーションでは、wia\_ステータス\_\_メディアの終了\_と同じように、wia\_エラー\_用紙\_空になることがあります。
1. スキャナーが最初のページを正常にスキャンし、スキャンを続行できても、データの損失を発生させないエラーが発生した場合は、WIA\_の状態を返して\_メディアの\_を終了\_ます。 これにより、アプリケーションは、エラーが発生する前にスキャンされたすべてのページを回復し、保存することができます。 その後のスキャンでは、スキャナーがエラーから正常に回復するまで、エラーコードを直ちに返します。
1. スキャナーが最初のページを正常にスキャンし、スキャンを続行できても、データ損失の原因となるエラーが発生した場合は、直ちにエラーコードを返します。

## <a name="if-wia_dps_pages-is-positive"></a>WIA\_DPS\_ページが正の場合

1. WIA\_DPS\_ページのすべてのルールが0になります。
1. 要求された数のページがスキャンされる前にスキャナーの用紙が不足している場合は、WIA\_の状態を返して\_メディアの\_を終了\_ます。 これにより、アプリケーションはスキャンセッションを終了し、既に正常にスキャンされているページの数を保持することができます。 一部のアプリケーションでは、wia\_エラー\_用紙\_、\_メディアの終了\_を WIA\_ステータス\_する場合と同じように、空になることがあります。
