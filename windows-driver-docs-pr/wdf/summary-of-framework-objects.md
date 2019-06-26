---
title: フレームワーク オブジェクトの要約
description: フレームワーク オブジェクトの要約
ms.assetid: 799284a5-91c0-47b0-8f20-75a5f8e2284d
keywords:
- 一覧表示されたフレームワーク オブジェクト WDK KMDF、
- framework オブジェクト WDK KMDF、概要
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c9f43075b3090469d023b942d1b9d36fd51d5935
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368086"
---
# <a name="summary-of-framework-objects"></a>フレームワーク オブジェクトの要約


次の表では、framework のオブジェクトのすべてを一覧表示し、各オブジェクトに関する基本的な情報を提供します。 モードの列は、オブジェクトを使用できるかどうかを示す KMDF と UMDF ドライバーまたは KMDF のみです。

一連のコールバックとメソッド、およびどのフレームワークに適用されます、次を参照してください。 [WDF のコールバックの概要とメソッド](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_wdf/)します。

|名前|ハンドル|目的|既定の親|ドライバーは既定の親をオーバーライドできますか。|Mode|リファレンス|
|--- |--- |--- |--- |--- |--- |--- |
|子リスト オブジェクト|WDFCHILDLIST|親デバイスに接続されている子デバイスの一覧を表します。|デバイス オブジェクト|X|KM|[WDF の子リスト オブジェクトの参照](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfchildlist/)|
|コレクション オブジェクト|WDFCOLLECTION|オブジェクトのコレクションを表します。|ドライバー オブジェクト|〇|KM/UM|[WDF のコレクション オブジェクトの参照](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfcollection/)|
|共通のバッファー オブジェクト|WDFCOMMONBUFFER|一般的なバッファーを表します。|DMA イネーブラー オブジェクト|X|KM|[一般的なバッファー オブジェクトの参照の WDF](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfcommonbuffer/)|
|デバイス オブジェクト|WDFDEVICE|デバイスを表します。|ドライバー オブジェクト|X|KM/UM|[WDF デバイス オブジェクトの参照](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/)|
|DMA イネーブラー オブジェクト|WDFDMAENABLER|フレームワークの DMA の機能を使用するためのドライバーを有効にします。|デバイス オブジェクト|〇|KM|[WDF DMA オブジェクト参照](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmaenabler/)|
|DMA トランザクション オブジェクト|WDFDMATRANSACTION|DMA トランザクションを表します。|DMA イネーブラー オブジェクト|X|KM|[WDF DMA オブジェクト参照](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmaenabler/)|
|DPC オブジェクト|WDFDPC|遅延プロシージャ呼び出しを表します。|なし|〇|KM|[WDF DPC オブジェクト参照](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdpc/)|
|ドライバー オブジェクト|WDFDRIVER|ドライバーを表します。|なし|X|KM/UM|[WDF ドライバー オブジェクト リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/)|
|ファイル オブジェクト|WDFFILEOBJECT|ファイルを表します。|デバイス オブジェクト|X|KM/UM|[WDF ファイル オブジェクトの参照](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffileobject/)|
|一般的なオブジェクト|WDFOBJECT|一般的なオブジェクトを表します。|ドライバー オブジェクト|〇|KM/UM|[WDF の一般的なオブジェクトの参照](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/)|
|オブジェクトを中断します。|WDFINTERRUPT|ハードウェア割り込みのリソースを表します。|デバイス オブジェクト|〇|KM/UM|[WDF のオブジェクト参照を中断します。](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/)|
|I/O ターゲット オブジェクト|WDFIOTARGET|別のドライバーが I/O 要求を送信するドライバーを表します。|デバイス オブジェクト|〇|KM/UM|[WDF I/O ターゲット オブジェクトの参照](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/)|
|ルック アサイド リスト オブジェクト|WDFLOOKASIDE|ルック アサイド リストを表します。|ドライバー オブジェクト|〇|KM|[WDF メモリ オブジェクトの参照](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/)|
|メモリ オブジェクト|WDFMEMORY|メモリ バッファーを表します。|ドライバー オブジェクト|〇|KM/UM|[WDF メモリ オブジェクトの参照](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/)|
|キュー オブジェクト|WDFQUEUE|I/O 要求を受信する I/O キューを表します。|デバイス オブジェクト|〇|KM/UM|[WDF のキュー オブジェクトの参照](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/)|
|レジストリ キー オブジェクト|WDFKEY|レジストリ キーを表します。|ドライバー オブジェクト|〇|KM/UM|[WDF のレジストリ キー オブジェクトの参照](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfregistry/)|
|オブジェクトを要求します。|WDFREQUEST|I/O 要求を表します。|None、framework によって作成された場合。 ドライバーによって作成された場合は、ドライバー オブジェクト。|はい、ドライバーによって作成された場合です。|KM/UM|[WDF 要求オブジェクトの参照](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/)|
|リソース リスト オブジェクト|WDFCMRESLIST|リソースの一覧を表します。|ドライバー オブジェクト|X|KM/UM|[WDF のリソース オブジェクトの参照](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfresource/)|
|リソースの範囲のリスト オブジェクト|WDFIORESLIST|論理構成を表します。|リソース要件のリスト オブジェクト|X|KM|[WDF のリソース オブジェクトの参照](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfresource/)|
|リソース要件のリスト オブジェクト|WDFIORESREQLIST|リソース要件の一覧を表します。|ドライバー オブジェクト|X|KM|[WDF のリソース オブジェクトの参照](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfresource/)|
|スピン ロック オブジェクト|WDFSPINLOCK|スピン ロックを表します。|ドライバー オブジェクト|〇|KM/UM|[WDF の同期方法](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfsync/)|
|文字列オブジェクト|WDFSTRING|Unicode 文字列を表します。|ドライバー オブジェクト|〇|KM/UM|[WDF 文字列オブジェクトの参照](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfstring/)|
|タイマー オブジェクト|WDFTIMER|タイマーを表します。|なし|〇|KM/UM|[WDF タイマー オブジェクトの参照](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdftimer/)|
|USB デバイス オブジェクト|WDFUSBDEVICE|USB に接続されているデバイスを表します。|デバイス オブジェクト|X|KM/UM|[WDF の USB の参照](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/)|
|USB インターフェイス オブジェクト|WDFUSBINTERFACE|USB デバイスのインターフェイスを表します。|USB デバイス オブジェクト|X|KM/UM|[WDF の USB の参照](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/)|
|USB パイプ オブジェクト|WDFUSBPIPE|USB デバイスのパイプを表します。|USB インターフェイス オブジェクト|X|KM/UM|[WDF の USB の参照](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/)|
|待機ロック オブジェクト|WDFWAITLOCK|待機のロックを表します。|ドライバー オブジェクト|〇|KM/UM|[WDF の同期方法](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfsync/)|
|WMI インスタンス オブジェクト|WDFWMIINSTANCE|WMI データ ブロックのインスタンスを表します。|WMI プロバイダー オブジェクト|X|KM|[WDF WMI リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfwmi/)|
|WMI プロバイダー オブジェクト|WDFWMIPROVIDER|WMI データ ブロックを表します。|デバイス オブジェクト|X|KM|[WDF WMI リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfwmi/)|
|作業項目オブジェクト|WDFWORKITEM|作業項目を表します。|なし|〇|KM/UM|[WDF の作業項目のオブジェクト参照](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfworkitem/)|


 

 

 





