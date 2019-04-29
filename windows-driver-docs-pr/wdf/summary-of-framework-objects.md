---
title: フレームワーク オブジェクトの要約
description: フレームワーク オブジェクトの要約
ms.assetid: 799284a5-91c0-47b0-8f20-75a5f8e2284d
keywords:
- 一覧表示されたフレームワーク オブジェクト WDK KMDF、
- framework オブジェクト WDK KMDF、概要
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 50ffe55ce414c9455d0af212a6dead96b9950060
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325117"
---
# <a name="summary-of-framework-objects"></a>フレームワーク オブジェクトの要約


次の表では、framework のオブジェクトのすべてを一覧表示し、各オブジェクトに関する基本的な情報を提供します。 モードの列は、オブジェクトを使用できるかどうかを示す KMDF と UMDF ドライバーまたは KMDF のみです。

一連のコールバックとメソッド、およびどのフレームワークに適用されます、次を参照してください。 [WDF のコールバックの概要とメソッド](https://msdn.microsoft.com/library/windows/hardware/dn265591)します。

|名前|ハンドル|目的|既定の親|ドライバーは既定の親をオーバーライドできますか。|Mode|リファレンス|
|--- |--- |--- |--- |--- |--- |--- |
|子リスト オブジェクト|WDFCHILDLIST|親デバイスに接続されている子デバイスの一覧を表します。|デバイス オブジェクト|X|KM|[WDF の子リスト オブジェクトの参照](https://msdn.microsoft.com/library/windows/hardware/dn265624)|
|コレクション オブジェクト|WDFCOLLECTION|オブジェクトのコレクションを表します。|ドライバー オブジェクト|〇|KM/UM|[WDF のコレクション オブジェクトの参照](https://msdn.microsoft.com/library/windows/hardware/dn265626)|
|共通のバッファー オブジェクト|WDFCOMMONBUFFER|一般的なバッファーを表します。|DMA イネーブラー オブジェクト|X|KM|[一般的なバッファー オブジェクトの参照の WDF](https://msdn.microsoft.com/library/windows/hardware/dn265627)|
|デバイス オブジェクト|WDFDEVICE|デバイスを表します。|ドライバー オブジェクト|X|KM/UM|[WDF デバイス オブジェクトの参照](https://msdn.microsoft.com/library/windows/hardware/dn265631)|
|DMA イネーブラー オブジェクト|WDFDMAENABLER|フレームワークの DMA の機能を使用するためのドライバーを有効にします。|デバイス オブジェクト|〇|KM|[WDF DMA オブジェクト参照](https://msdn.microsoft.com/library/windows/hardware/dn265634)|
|DMA トランザクション オブジェクト|WDFDMATRANSACTION|DMA トランザクションを表します。|DMA イネーブラー オブジェクト|X|KM|[WDF DMA オブジェクト参照](https://msdn.microsoft.com/library/windows/hardware/dn265634)|
|DPC オブジェクト|WDFDPC|遅延プロシージャ呼び出しを表します。|なし|〇|KM|[WDF DPC オブジェクト参照](https://msdn.microsoft.com/library/windows/hardware/dn265635)|
|ドライバー オブジェクト|WDFDRIVER|ドライバーを表します。|なし|X|KM/UM|[WDF ドライバー オブジェクト リファレンス](https://msdn.microsoft.com/library/windows/hardware/dn265636)|
|ファイル オブジェクト|WDFFILEOBJECT|ファイルを表します。|デバイス オブジェクト|X|KM/UM|[WDF ファイル オブジェクトの参照](https://msdn.microsoft.com/library/windows/hardware/dn265638)|
|一般的なオブジェクト|WDFOBJECT|一般的なオブジェクトを表します。|ドライバー オブジェクト|〇|KM/UM|[WDF の一般的なオブジェクトの参照](https://msdn.microsoft.com/library/windows/hardware/dn265639)|
|オブジェクトを中断します。|WDFINTERRUPT|ハードウェア割り込みのリソースを表します。|デバイス オブジェクト|〇|KM/UM|[WDF のオブジェクト参照を中断します。](https://msdn.microsoft.com/library/windows/hardware/dn265640)|
|I/O ターゲット オブジェクト|WDFIOTARGET|別のドライバーが I/O 要求を送信するドライバーを表します。|デバイス オブジェクト|〇|KM/UM|[WDF I/O ターゲット オブジェクトの参照](https://msdn.microsoft.com/library/windows/hardware/dn265644)|
|ルック アサイド リスト オブジェクト|WDFLOOKASIDE|ルック アサイド リストを表します。|ドライバー オブジェクト|〇|KM|[WDF メモリ オブジェクトの参照](https://msdn.microsoft.com/library/windows/hardware/dn265645)|
|メモリ オブジェクト|WDFMEMORY|メモリ バッファーを表します。|ドライバー オブジェクト|〇|KM/UM|[WDF メモリ オブジェクトの参照](https://msdn.microsoft.com/library/windows/hardware/dn265645)|
|キュー オブジェクト|WDFQUEUE|I/O 要求を受信する I/O キューを表します。|デバイス オブジェクト|〇|KM/UM|[WDF のキュー オブジェクトの参照](https://msdn.microsoft.com/library/windows/hardware/dn265647)|
|レジストリ キー オブジェクト|WDFKEY|レジストリ キーを表します。|ドライバー オブジェクト|〇|KM/UM|[WDF のレジストリ キー オブジェクトの参照](https://msdn.microsoft.com/library/windows/hardware/dn265663)|
|オブジェクトを要求します。|WDFREQUEST|I/O 要求を表します。|None、framework によって作成された場合。 ドライバーによって作成された場合は、ドライバー オブジェクト。|はい、ドライバーによって作成された場合です。|KM/UM|[WDF 要求オブジェクトの参照](https://msdn.microsoft.com/library/windows/hardware/dn265664)|
|リソース リスト オブジェクト|WDFCMRESLIST|リソースの一覧を表します。|ドライバー オブジェクト|X|KM/UM|[WDF のリソース オブジェクトの参照](https://msdn.microsoft.com/library/windows/hardware/dn265665)|
|リソースの範囲のリスト オブジェクト|WDFIORESLIST|論理構成を表します。|リソース要件のリスト オブジェクト|X|KM|[WDF のリソース オブジェクトの参照](https://msdn.microsoft.com/library/windows/hardware/dn265665)|
|リソース要件のリスト オブジェクト|WDFIORESREQLIST|リソース要件の一覧を表します。|ドライバー オブジェクト|X|KM|[WDF のリソース オブジェクトの参照](https://msdn.microsoft.com/library/windows/hardware/dn265665)|
|スピン ロック オブジェクト|WDFSPINLOCK|スピン ロックを表します。|ドライバー オブジェクト|〇|KM/UM|[WDF の同期方法](https://msdn.microsoft.com/library/windows/hardware/dn265669)|
|文字列オブジェクト|WDFSTRING|Unicode 文字列を表します。|ドライバー オブジェクト|〇|KM/UM|[WDF 文字列オブジェクトの参照](https://msdn.microsoft.com/library/windows/hardware/dn265667)|
|タイマー オブジェクト|WDFTIMER|タイマーを表します。|なし|〇|KM/UM|[WDF タイマー オブジェクトの参照](https://msdn.microsoft.com/library/windows/hardware/dn265670)|
|USB デバイス オブジェクト|WDFUSBDEVICE|USB に接続されているデバイスを表します。|デバイス オブジェクト|X|KM/UM|[WDF の USB の参照](https://msdn.microsoft.com/library/windows/hardware/dn265671)|
|USB インターフェイス オブジェクト|WDFUSBINTERFACE|USB デバイスのインターフェイスを表します。|USB デバイス オブジェクト|X|KM/UM|[WDF の USB の参照](https://msdn.microsoft.com/library/windows/hardware/dn265671)|
|USB パイプ オブジェクト|WDFUSBPIPE|USB デバイスのパイプを表します。|USB インターフェイス オブジェクト|X|KM/UM|[WDF の USB の参照](https://msdn.microsoft.com/library/windows/hardware/dn265671)|
|待機ロック オブジェクト|WDFWAITLOCK|待機のロックを表します。|ドライバー オブジェクト|〇|KM/UM|[WDF の同期方法](https://msdn.microsoft.com/library/windows/hardware/dn265669)|
|WMI インスタンス オブジェクト|WDFWMIINSTANCE|WMI データ ブロックのインスタンスを表します。|WMI プロバイダー オブジェクト|X|KM|[WDF WMI リファレンス](https://msdn.microsoft.com/library/windows/hardware/dn265672)|
|WMI プロバイダー オブジェクト|WDFWMIPROVIDER|WMI データ ブロックを表します。|デバイス オブジェクト|X|KM|[WDF WMI リファレンス](https://msdn.microsoft.com/library/windows/hardware/dn265672)|
|作業項目オブジェクト|WDFWORKITEM|作業項目を表します。|なし|〇|KM/UM|[WDF の作業項目のオブジェクト参照](https://msdn.microsoft.com/library/windows/hardware/dn265673)|


 

 

 





