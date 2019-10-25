---
title: ストリームの変更
description: ストリームの変更
ms.assetid: 3bd6a511-c602-4159-87b4-7e1e55c03b2e
keywords:
- ストリームの変更 (WDK DVD デコーダー)
- WDK DVD デコーダーのフォーマット
- ヘッダー WDK DVD デコーダー
- ストリーム形式 WDK DVD デコーダー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 220ef48d354ed5c0efc843e7af513b0bd05ae7aa
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837689"
---
# <a name="stream-changes"></a>ストリームの変更





DVD ストリームの形式はいつでも変更される可能性があります。 たとえば、オーディオストリーム形式は、再生中に AC3 と LPCM の間で変わる可能性があります。

ストリーム内の各データサンプルには、 [**Ksk ストリーム\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksstream_header)構造体が追加されています。 この構造体には、 **Optionsflags**メンバーが含まれています。

次のいずれかのフラグを含むヘッダーに関連付けられているデータサンプルには、null データパケットまたは有効なデータが含まれている場合があります。

次の KSK ストリーム\_ヘッダーの**オプション**の値は、DVD の再生にとって重要です。

<a href="" id="ksstream-header-optionsf-datadiscontinuity"></a>**KSK ストリーム\_ヘッダー\_オプション SF\_DATADISCONTINUITY 性**  
KSK ストリーム\_ヘッダー\_オプション SF\_DATADISCONTINUITY ビットは、その直後に続くサンプルが、前のサンプルとは異なるデータソース (または場所/位置) に属していることを示します。 これは、前のサンプルを使用して実行されていた処理がすべて完了している必要があることを示します。 このビットは、多くの場合、前のフレームの途中にあるため、デコーダーは前のフレームを破棄して新しいデータで処理を開始する必要があることを示しています。

<a href="" id="ksstream-header-optionsf-timediscontinuity"></a>**KSK ストリーム\_ヘッダー\_オプション SF\_TIMEDISCONTINUITY 性**  
KSK ストリーム\_ヘッダー\_オプション SF\_TIMEDISCONTINUITY ビットは、このサンプルの直後にあるデータに時間間隔があることを示します。 たとえば、DVD ストリームに1つの I フレームとしてエンコードされた静止フレームが含まれている場合、デコーダーは I フレームのすべてのデータを受け取ります。最後のサンプルには、KSK ストリーム\_ヘッダー\_オプション SF\_TIMEDISCONTINUITY フラグが含まれています。 これは、デコーダーが I フレームをすぐにデコードし、B フレームデータを待機しないことを示します。

<a href="" id="ksstream-header-optionsf-typechanged"></a>**KSK ストリーム\_ヘッダー\_オプション SF\_TYPECHANGED**  
KSK ストリーム\_ヘッダー\_オプション SF\_TYPECHANGED ビットは、ヘッダーに接続されているサンプルがストリームの新しい[**KSDATAFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat)ブロックであることを示します。 これにより、データ型を動的に変更できます。 たとえば、ビデオを4x3 から16x9 に変更したり、オーディオを AC3 から PCM に変更したりすることができます。 デコーダーは、新しいフォーマットブロックを使用したパケットより前のすべてのデータが処理された場合にのみ、新しいフォーマットブロックに必要なすべての変更を行います。

ストリーム形式の変更が発生すると、ミニドライバーは、データパケットの KSK ストリームの\_ヘッダー構造の**Optionsflags**メンバーに設定された ksk ストリーム\_ヘッダー\_オプション SF\_typechanged ビットを持つデータパケットを受信します。

ミニドライバーでは、オーディオストリームでサポートされているデータ形式が正しく公開されていない場合は、\_ヘッダー\_オプション SF\_TYPECHANGED フラグが表示されないことがあります。

**ストリームでサポートされているデータ形式を正しく公開するには、次の2つの手順を実行します。**

1.  ストリームの SRB\_GET\_ストリーム\_情報ハンドラーでは、 **Numberofformatarrayentries**ポインターの配列を指すように**StreamFormatsArray**ポインターを設定する必要があります。これらはそれぞれ、有効な書式ブロックを指します。

2.  SRB\_GET\_DATA\_共通部分ハンドラーは、指定された形式に対応する書式ブロックを、指定されたバッファーにコピーする必要があります。

ビデオ形式の変更では、ビデオ形式が変更されたことを示すために、KSK ストリームイベントにビデオポート接続を知らせる必要もあります。 ミニドライバーでは、 [**Streamclassstreamnotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nf-strmini-streamclassstreamnotification)(signal Streamevents、pMyHwDevExt-&gt;pMyStreamObject、& MY\_KSEVENTSETID\_VPNOTIFY、KSEVENT\_vpnotify\_formatchange) を使用する必要があります汎用.

ピクセル縦横比など、ビデオ形式のパラメーターを変更すると、デコーダーはフォーマットブロックを受け取ります。 デコーダーはビデオポートにビデオポート接続を再ネゴシエートするように通知する必要があります。 デコーダーは、パラメーター *Signal多重 Streamevents*を使用して[**Streamclassstreamnotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nf-strmini-streamclassstreamnotification)を呼び出します。

DVD デコーダーミニドライバーは、VideoPort ストリームの[**HW\_ストリームの\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_information)エントリで、このイベントのサポートが提供されていることを示す必要があります。 ビデオポートイベントのイベントセット ID は[KSEVENTSETID\_VPNotify](https://docs.microsoft.com/windows-hardware/drivers/stream/kseventsetid-vpnotify) 、イベント ID は[**KSEVENT\_VPNOTIFY\_formatchange**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksevent-vpnotify-formatchange)です。

 

 




