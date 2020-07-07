---
title: Windows Me と Windows XP のドキュメントフィーダーサポートの追加
description: Windows Me と Windows XP のドキュメントフィーダーサポートの追加
ms.assetid: f3be94fa-6fb7-45de-a3ce-f3d173e802cf
ms.date: 07/06/2020
ms.localizationpriority: medium
ms.openlocfilehash: 32297a343a2340b6152892b83bca603834cdf18c
ms.sourcegitcommit: 40d7d538756767d26bbda636589f614f85a6fab3
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "86020073"
---
# <a name="adding-document-feeder-support"></a>ドキュメントフィーダーサポートの追加

ドキュメントフィーダーは、スキャナーに関連付けられているか、スキャナーに組み込まれているユニットで、スキャンする位置に用紙ドキュメントを自動的にフィードします。 ドキュメントフィーダーを備えたスキャナーでは、次の一覧に示すプロパティを追加することによって機能が公開され、制御されます。 Windows Me と Windows XP では、次のプロパティがルート項目に配置されています。

- [**WIA \_ DPS \_ 横 \_ シート \_ フィード \_ サイズ**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-horizontal-sheet-feed-size)

- [**WIA \_ DPS の \_ 垂直 \_ シートの \_ フィード \_ サイズ**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-vertical-sheet-feed-size)

- [**WIA \_ DPS \_ 最小 \_ \_ シート \_ フィード \_ サイズ**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-min-horizontal-sheet-feed-size)

- [**WIA \_ DPS \_ 最小の \_ 垂直 \_ シートの \_ フィード \_ サイズ**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-min-vertical-sheet-feed-size)

- [**WIA \_ DPS \_ シート \_ フィーダーの \_ 登録**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-sheet-feeder-registration)

- [**WIA \_ DPS \_ ドキュメント \_ 処理 \_ 機能**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-document-handling-capabilities)

- [**WIA \_ DPS \_ ドキュメント \_ 処理の \_ 状態**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-document-handling-status)

- [**WIA \_ DPS \_ ドキュメント \_ 処理の \_ 選択**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-document-handling-select)

- [**WIA \_ DPS \_ ページ**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-pages)

Windows Me と Windows XP では、次のオプションのドキュメントフィーダーのプロパティが子項目に配置されています。

- [**WIA \_ DPS \_ ページ \_ サイズ**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-page-size)

- [**WIA \_ DPS \_ ページの \_ 幅**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-page-width)

- [**WIA \_ DPS \_ ページの \_ 高さ**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-page-height)

- [**WIA \_ IP の \_ 向き**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-orientation)

デバイスにフラットベッド、ドキュメントフィーダー、および両面印刷装置がある場合、ドライバーは WIA \_ DPS \_ ドキュメント \_ 処理機能プロパティをとして報告し \_ `FEED | FLAT | DUP` ます。 WIA \_ DPS ドキュメント処理の選択の有効な \_ 値 \_ \_ が正しく設定されていることを確認します。

たとえば、アプリケーションがドキュメントフィーダーから3ページの両面スキャンを実行するとします。 これを実現するために、アプリケーションでは、WIA \_ DPS \_ ドキュメント \_ 処理の \_ SELECT プロパティを (フィーダー |) に設定します。[半二重]) を設定し、[WIA \_ DPS \_ ページ] プロパティを3に設定します。 アプリケーションで最初にページの先頭をスキャンする場合は、WIA \_ DPS \_ ドキュメント \_ 処理の \_ 選択プロパティをに設定する必要があり `FEEDER | DUPLEX | FRONT\_FIRST` ます。 この処理が完了すると、アプリケーションは、データ転送を要求する子項目に移動する必要があります。 ミニドライバーは、フィーダー内の最初のページの前をページ1、ページ2として、フィーダーの2ページ目をページ3として報告します。

デバイスがドキュメントフィーダーを持っている場合は、ドキュメントフィーダーのプロパティをサポートしている必要があることに注意してください。

## <a name="acquiring-data-from-a-document-feeder"></a>ドキュメントフィーダーからデータを取得する

スキャナーがドキュメントフィーダーからイメージを取得する場合、 [**IWiaMiniDrv::D rvacquireitemdata**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata)メソッドの実装にはいくつかの変更を加える必要があります。

1. アプリケーションは、WIA \_ DPS ドキュメント処理機能プロパティを読み取って、 \_ \_ \_ スキャナーがドキュメントフィーダーを使用したスキャンをサポートしているかどうかを判断します。

1. アプリケーションは、WIA DPS ドキュメント処理の選択プロパティを読み取って、 \_ \_ \_ \_ スキャナーがドキュメントフィーダーを使用してスキャンするように構成されているかどうかを判断します。

1. アプリケーションは、WIA DPS ドキュメント処理の状態を読み取って、ドキュメントフィーダーに用紙があるかどうかを判断し \_ \_ \_ \_ ます。 フィーダーに用紙が存在しない場合は、WIA \_ DPS \_ ドキュメントの \_ 処理 \_ 状態を適切な状態コードに設定し \_ 、 \_ \_ 取得が行われた直後に**IWiaMiniDrv::d rvacquireitemdata**から、wia エラーを返します。

1. スキャンの動作を決定するには、[WIA \_ DPS \_ ページのプロパティを確認します。 このプロパティが0の場合は、フィーダーが空になるまですべてのページをスキャンします。 正の値の場合は、WIA DPS pages プロパティに格納されている値によって示されるページ数だけをスキャンし \_ \_ ます。

1. [**IWiaMiniDrvCallBack:: MiniDrvCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrvcallback-minidrvcallback)メソッドを呼び出すことにより、ループを制御し、継続的にスキャンし、WIA アプリケーションにデータを送信することで、要求された数のページをスキャンします。 これがどのように機能するかを次のコード例に示します。

    ```cpp
    for(int x=1; x=Pagecount; x++)
    {
        \\ Tell scanner to scan an image.
        \\ Receive image data from scanner.
        \\ Send the just-scanned image to the registered application.
    }
    ```

1. [**WIA \_ IPA \_ tymed**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-tymed)が tymed \_ callback または tymed マルチページコールバックに設定されている場合 \_ \_ 、 \_ \_ \_ 1 ページがスキャンされた後、次のページがスキャンされる前に、追加のメッセージ (メッセージの新しいページ) を送信する必要があります。 これを行うには、 [**Wiassendendofpage**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiassendendofpage)の WIA サービスユーティリティ関数を呼び出します。

ドキュメントフィーダードライバーが返すページ数は、[WIA DPS ページ] プロパティの設定によって異なり \_ \_ ます。

## <a name="if-wia_dps_pages-is-zero"></a>WIA \_ DPS \_ ページがゼロの場合

1. スキャナーが最初のページをスキャンできない場合は、すぐにエラーコードを返します。 これには、紙詰まりや、スキャナーの用紙が不足している場合も含まれます。

1. スキャナーが最初のページを正常にスキャンし、スキャンを続行できても、用紙が不足している場合は、成功コード「WIA \_ STATUS \_ MEDIA の終了」を返し \_ \_ ます。 これは、転送が成功したことをアプリケーションに通知しますが、スキャナーの用紙が不足しています。 一部のアプリケーション \_ \_ \_ は、 \_ メディアの wia ステータスの終了と同じように、空の wia エラー用紙に応答し \_ \_ \_ ます。

1. スキャナーが最初のページを正常にスキャンし、スキャンを続行できても、データの損失が発生しないというエラーが発生する場合は、 \_ \_ メディアの WIA ステータスの終了を返し \_ \_ ます。 これにより、アプリケーションは、エラーが発生する前にスキャンされたすべてのページを回復し、保存することができます。 その後のスキャンでは、スキャナーがエラーから正常に回復するまで、エラーコードを直ちに返します。

1. スキャナーが最初のページを正常にスキャンし、スキャンを続行できても、データ損失の原因となるエラーが発生した場合は、直ちにエラーコードを返します。

## <a name="if-wia_dps_pages-is-positive"></a>WIA \_ DPS \_ ページが正の場合

1. WIA \_ DPS ページが0のすべてのルール \_ が適用されます。

1. 要求された数のページがスキャンされる前にスキャナーの用紙が不足している場合は、WIA \_ \_ の状態の終了メディアを返し \_ \_ ます。 これにより、アプリケーションはスキャンセッションを終了し、既に正常にスキャンされているページの数を保持することができます。 一部のアプリケーションは \_ \_ \_ 、 \_ メディアの wia ステータスの終了と同じ方法で、wia エラー用紙に応答し \_ \_ \_ ます。
