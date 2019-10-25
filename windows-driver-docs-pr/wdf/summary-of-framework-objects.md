---
title: フレームワーク オブジェクトの要約
description: フレームワーク オブジェクトの要約
ms.assetid: 799284a5-91c0-47b0-8f20-75a5f8e2284d
keywords:
- フレームワークオブジェクト WDK KMDF、一覧
- フレームワークオブジェクト WDK KMDF、概要
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7e8f594a4f08b37538d9886b7de2b300425bfc8c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840461"
---
# <a name="summary-of-framework-objects"></a>フレームワーク オブジェクトの要約


次の表に、すべてのフレームワークオブジェクトの一覧と、各オブジェクトに関する基本的な情報を示します。 [モード] 列には、オブジェクトを KMDF および UMDF ドライバー (KMDF のみ) で使用できるかどうかが示されます。

コールバックとメソッドの一覧と適用可能なフレームワークについては、「 [WDF のコールバックとメソッドの概要](https://docs.microsoft.com/windows-hardware/drivers/ddi/_wdf/)」を参照してください。

|名前|ハンドル|目的|既定の親|ドライバーで既定の親を上書きできますか?|[モード]|辞書/リファレンス|
|--- |--- |--- |--- |--- |--- |--- |
|子リストオブジェクト|WDFCHILDLIST|親デバイスに接続されている子デバイスの一覧を表します。|デバイスオブジェクト|必須ではない|KM|[WDF の子リストオブジェクトの参照](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/)|
|コレクションオブジェクト|WDFCOLLECTION|オブジェクトコレクションを表します。|Driver オブジェクト|[はい]|KM/UM|[WDF Collection オブジェクトの参照](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfcollection/)|
|共通バッファーオブジェクト|WDFCOMMONBUFFER|共通バッファーを表します。|DMA イネーブラーオブジェクト|必須ではない|KM|[WDF 共通バッファーオブジェクトリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfcommonbuffer/)|
|デバイスオブジェクト|WDFDEVICE|デバイスを表します。|Driver オブジェクト|必須ではない|KM/UM|[WDF Device オブジェクトリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/)|
|DMA イネーブラーオブジェクト|WDFDMAENABLER|ドライバーがフレームワークの DMA 機能を使用できるようにします。|デバイスオブジェクト|[はい]|KM|[WDF DMA オブジェクトリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/)|
|DMA トランザクションオブジェクト|WDFDMATRANSACTION|DMA トランザクションを表します。|DMA イネーブラーオブジェクト|必須ではない|KM|[WDF DMA オブジェクトリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/)|
|DPC オブジェクト|WDFDPC|遅延プロシージャ呼び出しを表します。|なし|[はい]|KM|[WDF DPC オブジェクトリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdpc/)|
|Driver オブジェクト|WDFDRIVER|ドライバーを表します。|なし|必須ではない|KM/UM|[WDF Driver オブジェクトリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/)|
|ファイルオブジェクト|WDFFILEOBJECT|ファイルを表します。|デバイスオブジェクト|必須ではない|KM/UM|[WDF File オブジェクトリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffileobject/)|
|全般オブジェクト|WDFOBJECT|一般的なオブジェクトを表します。|Driver オブジェクト|[はい]|KM/UM|[WDF 一般オブジェクトリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/)|
|Interrupt オブジェクト|WDFINTERRUPT|ハードウェア割り込みリソースを表します。|デバイスオブジェクト|[はい]|KM/UM|[WDF Interrupt オブジェクトリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/)|
|I/o ターゲットオブジェクト|WDFIOTARGET|別のドライバーが i/o 要求を送信するドライバーを表します。|デバイスオブジェクト|[はい]|KM/UM|[WDF i/o ターゲットオブジェクトリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/)|
|ルックアサイドリストオブジェクト|WDFLOOKASIDE アサイド|ルックアサイドリストを表します。|Driver オブジェクト|[はい]|KM|[WDF Memory オブジェクトリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfmemory/)|
|Memory オブジェクト|WDFMEMORY|メモリバッファーを表します。|Driver オブジェクト|[はい]|KM/UM|[WDF Memory オブジェクトリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfmemory/)|
|Queue オブジェクト|WDFQUEUE|I/o 要求を受信する i/o キューを表します。|デバイスオブジェクト|[はい]|KM/UM|[WDF Queue オブジェクト参照](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/)|
|レジストリキーオブジェクト|WDFKEY|レジストリキーを表します。|Driver オブジェクト|[はい]|KM/UM|[WDF レジストリキーオブジェクトリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfregistry/)|
|要求オブジェクト|WDFREQUEST|I/o 要求を表します。|None (フレームワークによって作成された場合)。 ドライバーオブジェクト (ドライバーによって作成された場合)。|はい (ドライバーによって作成された場合)。|KM/UM|[WDF Request オブジェクトの参照](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/)|
|リソースリストオブジェクト|WDFCMRESLIST|リソースリストを表します。|Driver オブジェクト|必須ではない|KM/UM|[WDF リソースオブジェクトの参照](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfresource/)|
|リソース範囲リストオブジェクト|WDFIORESLIST|論理構成を表します。|リソース要件リストオブジェクト|必須ではない|KM|[WDF リソースオブジェクトの参照](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfresource/)|
|リソース要件リストオブジェクト|WDFIORESREQLIST|リソース要件の一覧を表します。|Driver オブジェクト|必須ではない|KM|[WDF リソースオブジェクトの参照](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfresource/)|
|スピンロックオブジェクト|WDFSPINLOCK ロック|スピンロックを表します。|Driver オブジェクト|[はい]|KM/UM|[WDF の同期方法](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfsync/)|
|String オブジェクト|WDFSTRING|Unicode 文字列を表します。|Driver オブジェクト|[はい]|KM/UM|[WDF String オブジェクトの参照](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfstring/)|
|Timer オブジェクト|WDFTIMER|タイマーを表します。|なし|[はい]|KM/UM|[WDF Timer オブジェクトリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdftimer/)|
|USB デバイスオブジェクト|WDFUSBDEVICE|USB に接続されているデバイスを表します。|デバイスオブジェクト|必須ではない|KM/UM|[WDF USB リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/)|
|USB インターフェイスオブジェクト|WDFUSBINTERFACE|USB デバイスインターフェイスを表します。|USB デバイスオブジェクト|必須ではない|KM/UM|[WDF USB リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/)|
|USB パイプオブジェクト|WDFUSBPIPE|USB デバイスパイプを表します。|USB インターフェイスオブジェクト|必須ではない|KM/UM|[WDF USB リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/)|
|Wait-オブジェクトのロック|WDFWAITLOCK|待機ロックを表します。|Driver オブジェクト|[はい]|KM/UM|[WDF の同期方法](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfsync/)|
|WMI インスタンスオブジェクト|WDFWMIINSTANCE|WMI データブロックのインスタンスを表します。|WMI プロバイダーオブジェクト|必須ではない|KM|[WDF WMI リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfwmi/)|
|WMI プロバイダーオブジェクト|WDFWMIPROVIDER|WMI データブロックを表します。|デバイスオブジェクト|必須ではない|KM|[WDF WMI リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfwmi/)|
|作業項目オブジェクト|WDFWORKITEM|作業項目を表します。|なし|[はい]|KM/UM|[WDF 作業項目オブジェクトの参照](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfworkitem/)|


 

 

 





