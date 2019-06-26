---
title: ストリームの変更
description: ストリームの変更
ms.assetid: 3bd6a511-c602-4159-87b4-7e1e55c03b2e
keywords:
- ストリームの WDK DVD デコーダーを変更します。
- WDK DVD デコーダーを書式設定します。
- ヘッダーの WDK DVD デコーダー
- ストリーム形式の WDK DVD デコーダー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 39e45bc2789e9941231fcba60226e8c164ed4c89
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377830"
---
# <a name="stream-changes"></a>ストリームの変更





DVD のストリームの形式でいつでも変更可能性があります。 たとえば、オーディオ ストリームの形式は、再生中に AC3 と LPCM 間で変更できます。

ストリーム内の各データ サンプルが含まれています、 [ **KSSTREAM\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksstream_header)構造が追加されます。 この構造に含まれる、 **OptionsFlags**メンバー。

次のフラグのいずれかを含むヘッダーに関連付けられたデータのサンプルは、null データ パケットまたは有効なデータを含めることはできません。

次の値、KSSTREAM の\_ヘッダー **OptionsFlags**メンバーは、DVD の再生を重要。

<a href="" id="ksstream-header-optionsf-datadiscontinuity"></a>**KSSTREAM\_ヘッダー\_OPTIONSF\_DATADISCONTINUITY**  
KSSTREAM\_ヘッダー\_OPTIONSF\_DATADISCONTINUITY ビットは、その直後のサンプルがより前のサンプル データのさまざまなソース (または場所/位置) に属していることを示します。 これは、進行状況は、前のサンプルを完了する必要がありますを使用してすべての処理されたことを示します。 このビットは、デコーダーが前のフレームの破棄し、新しいデータでの処理を開始する必要があることを示す、前のフレームの途中で多くの場合は。

<a href="" id="ksstream-header-optionsf-timediscontinuity"></a>**KSSTREAM\_ヘッダー\_OPTIONSF\_TIMEDISCONTINUITY**  
KSSTREAM\_ヘッダー\_OPTIONSF\_TIMEDISCONTINUITY ビットは、データをすぐにこのサンプルを次の時間差があることを示します。 たとえば、DVD のストリームにフレームは、1 つとしてエンコードされた、静止フレームが含まれている場合、デコーダー受信のすべてのデータ、KSSTREAM を格納している最後のサンプルを使用して、フレームに\_ヘッダー\_OPTIONSF\_TIMEDISCONTINUITY フラグ. これを示すことデコーダーがすぐにデコードにフレームおよび B フレーム データを待つ必要はありません。

<a href="" id="ksstream-header-optionsf-typechanged"></a>**KSSTREAM\_ヘッダー\_OPTIONSF\_TYPECHANGED**  
KSSTREAM\_ヘッダー\_OPTIONSF\_TYPECHANGED ビットは、ヘッダーで接続されているサンプルになるは、新しいことを示します[ **KSDATAFORMAT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksdataformat)をブロックしますストリーム。 これは、ため、データ型を動的に変更できます。 例は、16 x 9、4 x 3 からビデオの変更や pcm AC3 からオーディオの変更になります。 デコーダーは、パケットと新しいブロックの書式設定する前にすべてのデータが処理された場合にのみ新しいブロックの書式設定に必要なすべての変更を行う必要があります。

ミニドライバーが、KSSTREAM でデータ パケットを受信するストリーム形式の変更が発生したときに\_ヘッダー\_OPTIONSF\_TYPECHANGED ビットが設定で、 **OptionsFlags** KSSTREAMのメンバー\_データ パケットのヘッダーの構造体。

ミニドライバーは、KSSTREAM を読み取ることはありません\_ヘッダー\_OPTIONSF\_TYPECHANGED フラグの場合は、オーディオのストリームでサポートされるデータ形式を正しく公開しません。

**ストリームでサポートされるデータ形式が正しく公開するには、2 つの手順が含まれます。**

1.  SRB\_取得\_ストリーム\_ストリームの情報のハンドラーを設定する必要があります、 **StreamFormatsArray**の配列を指すポインター **NumberOfFormatArrayEntries**このポインターを使用して、有効な形式のブロックを参照します。

2.  SRB\_取得\_データ\_積集合のハンドラーは、指定されたバッファーに提案された形式に対応するブロックの書式設定をコピーする必要があります。

ビデオの形式の変更には、KSSTREAM イベントは、ビデオの形式が変更されたことを示すビデオ ポート接続を信号もする必要があります。 ミニドライバーを使用する必要があります[ **StreamClassStreamNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/nf-strmini-streamclassstreamnotification)(SignalMultipleStreamEvents、pMyHwDevExt -&gt;pMyStreamObject、マイ &\_KSEVENTSETID\_VPNOTIFY、KSEVENT\_VPNOTIFY\_段落) この目的のためです。

ピクセル縦横比などのビデオ形式のいくつかのパラメーターが変更されたときに、デコーダーは、ブロックの書式設定を受信します。 デコーダーは、ビデオ ポート接続を再ネゴシエートするビデオ ポートを通知する必要があります。 デコーダー呼び出し[ **StreamClassStreamNotification** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/nf-strmini-streamclassstreamnotification)パラメーターと共に*SignalMultipleStreamEvents*します。

DVD デコーダーのミニドライバーはこのイベントでのサポートが提供されることを示す必要があります、 [ **HW\_ストリーム\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/ns-strmini-_hw_stream_information)ビデオ ポート ストリーム エントリ。 ビデオ ポート イベントがイベント セット ID [KSEVENTSETID\_VPNotify](https://docs.microsoft.com/windows-hardware/drivers/stream/kseventsetid-vpnotify)と ID がイベント[ **KSEVENT\_VPNOTIFY\_段落**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksevent-vpnotify-formatchange).

 

 




