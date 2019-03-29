---
title: USBCAMD2 ミニドライバーの操作
description: USBCAMD2 ミニドライバーの操作
ms.assetid: 395612cd-3407-4b42-b3a5-0afa838e73d9
keywords:
- Windows 2000 カーネル ストリーミング モデル WDK、USBCAMD2 ミニドライバー ライブラリ
- ストリーミング モデル WDK Windows 2000 カーネル、USBCAMD2 ミニドライバー ライブラリ
- カーネル ストリーミング モデルの WDK、USBCAMD2 ミニドライバー ライブラリ
- WDK Windows 2000 のカーネル ストリーミング USBCAMD2 ミニドライバーの操作
- USB ベースのストリーミング カメラ WDK USBCAMD2
- カメラ WDK USBCAMD2
- される Srb WDK USBCAMD2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 61a1165316976e6a91e49f2ea2c23dc23773a42a
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349385"
---
# <a name="usbcamd2-minidriver-operation"></a>USBCAMD2 ミニドライバーの操作

USBCAMD2 カメラのミニドライバーは、一般には、次のように動作します。

- カメラのミニドライバー呼び出し[ **USBCAMD\_DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff568593)からその[ *DriverEntry* ](https://msdn.microsoft.com/library/windows/hardware/ff544113)ルーチン。 ミニドライバーを呼び出すと**USBCAMD\_DriverEntry**、ミニドライバーの USBCAMD2 に渡す[ *AdapterReceivePacket* ](https://msdn.microsoft.com/library/windows/hardware/ff554080)コールバック関数。 USBCAMD2 のミニドライバーを登録し、 *stream.sys*クラス ドライバー。

- カメラ ミニドライバーでさまざまなストリーム要求のブロック (される Srb) を受信できますし、その*AdapterReceivePacket*などを処理するコールバック関数。
  - [**SRB\_初期化\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/ff568185)
  - [**SRB\_初期化\_完了**](https://msdn.microsoft.com/library/windows/hardware/ff568182)
  - [**SRB\_GET\_STREAM\_INFO**](https://msdn.microsoft.com/library/windows/hardware/ff568173)
  - [**SRB\_取得\_デバイス\_プロパティ**](https://msdn.microsoft.com/library/windows/hardware/ff568170)
  - [**SRB\_設定\_デバイス\_プロパティ**](https://msdn.microsoft.com/library/windows/hardware/ff568204)
  - [**SRB\_取得\_データ\_積集合**](https://msdn.microsoft.com/library/windows/hardware/ff568168)
  - [**SRB\_OPEN\_STREAM**](https://msdn.microsoft.com/library/windows/hardware/ff568191)
- カメラのミニドライバーは、各 SRB を処理する必要がある方法を決定します。 ミニドライバーは、処理される Srb の推進のために、USBCAMD2 ミニドライバー ライブラリ ルーチンを呼び出すことができます。 これらのルーチンは、通常で始まる、 *USBCAMD\_* プレフィックス。

たとえば、カメラ ミニドライバー カメラ ミニドライバーの USBCAMD2 の別のコールバック関数を指定するには、指定のエントリ ポイントを[ **USBCAMD\_デバイス\_DATA2** ](https://msdn.microsoft.com/library/windows/hardware/ff568590)構造体。 ミニドライバーを呼び出して[ **USBCAMD\_InitializeNewInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff568599)渡す初期化 USBCAMD\_デバイス\_USBCAMD2 DATA2 構造体。 USBCAMD2 は、必要な場合に、ミニドライバーのコールバック関数を呼び出します。

> [!NOTE]
> [ **USBCAMD\_デバイス\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff568585)の旧バージョンと互換性の目的でのみ USBCAMD2 で構造体がサポートされています。

呼び出す必要があります、ミニドライバー [ **USBCAMD\_AdapterReceivePacket** ](https://msdn.microsoft.com/library/windows/hardware/ff568574) USBCAMD2 を処理するにハンドルされない任意される Srb を送信します。

[USBCAMD ライブラリのコールバック関数](https://msdn.microsoft.com/library/windows/hardware/ff568608)ミニドライバーを実装するコールバック関数と省略可能または必須いるかどうかについて説明します。

次の手順の一覧は、カメラ ミニドライバーに送信される Srb の処理の一般的なフローを示しています。

## <a name="minidrivers-srbinitializedevice-handler"></a>ミニドライバーの SRB\_初期化\_デバイス ハンドラー

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>コンポーネント</th>
<th>操作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>カメラのミニドライバー</p></td>
<td><p>USBCAMD2 を呼び出すことによって初期化<a href="https://msdn.microsoft.com/library/windows/hardware/ff568599" data-raw-source="[&lt;strong&gt;USBCAMD_InitializeNewInterface&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568599)"> <strong>USBCAMD_InitializeNewInterface</strong></a>ビデオを示す、または、まだデバイス イベントの有効化などのカーネル モードで生の処理の要件。</p></td>
</tr>
<tr class="even">
<td><p>カメラのミニドライバー</p></td>
<td><p>呼び出す<a href="https://msdn.microsoft.com/library/windows/hardware/ff568574" data-raw-source="[&lt;strong&gt;USBCAMD_AdapterReceivePacket&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568574)"> <strong>USBCAMD_AdapterReceivePacket</strong></a>します。</p></td>
</tr>
<tr class="odd">
<td><p>USBCAMD2</p></td>
<td><p>USB デバイスと構成記述子を取得します。</p></td>
</tr>
<tr class="even">
<td><p>USBCAMD2</p></td>
<td><p>呼び出すようにミニドライバーの<a href="https://msdn.microsoft.com/library/windows/hardware/ff557605" data-raw-source="[&lt;em&gt;CamConfigureEx&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557605)"> <em>CamConfigureEx</em> </a>コールバック関数。</p></td>
</tr>
<tr class="odd">
<td><p>カメラのミニドライバー</p></td>
<td><p>構成を完了します。 代替の設定と最大転送サイズを選択します。 配列を入力<a href="https://msdn.microsoft.com/library/windows/hardware/ff568623" data-raw-source="[&lt;strong&gt;USBCAMD_Pipe_Config_Descriptor&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568623)"> <strong>USBCAMD_Pipe_Config_Descriptor</strong> </a>構造体。</p></td>
</tr>
<tr class="even">
<td><p>USBCAMD2</p></td>
<td><p>配列を解析<strong>USBCAMD_Pipe_Config_Descriptor</strong>構造体。</p></td>
</tr>
<tr class="odd">
<td><p>USBCAMD2</p></td>
<td><p>呼び出すようにミニドライバーの<a href="https://msdn.microsoft.com/library/windows/hardware/ff557614" data-raw-source="[&lt;em&gt;CamInitialize&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557614)"> <em>CamInitialize</em> </a>コールバック関数。</p></td>
</tr>
<tr class="even">
<td><p>カメラのミニドライバー</p></td>
<td><p>初期化を完了します。 デバイスの電源を設定し、カメラの既定の設定をアクティブ化します。</p></td>
</tr>
<tr class="odd">
<td><p>USBCAMD2</p></td>
<td><p>ストリームおよびストリーム記述子サイズの数を指定、 <em>stream.sys</em>クラス ドライバー。</p></td>
</tr>
</tbody>
</table>

## <a name="minidrivers-srbgetstreaminfo-handler"></a>ミニドライバーの SRB\_取得\_ストリーム\_情報ハンドラー

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>コンポーネント</th>
<th>操作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>カメラのミニドライバー</p></td>
<td><p>提供、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff559692" data-raw-source="[&lt;strong&gt;HW_STREAM_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559692)"> <strong>HW_STREAM_INFORMATION</strong> </a>ストリーム情報構造体、 <em>stream.sys</em>クラス ドライバー。</p></td>
</tr>
<tr class="even">
<td><p>カメラのミニドライバー</p></td>
<td><p>デバイスのプロパティ セット内の配列へのポインターの塗りつぶし<em>stream.sys</em>クラス ドライバーの<a href="https://msdn.microsoft.com/library/windows/hardware/ff559690" data-raw-source="[&lt;strong&gt;HW_STREAM_HEADER&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559690)"> <strong>HW_STREAM_HEADER</strong> </a>構造体。</p></td>
</tr>
<tr class="odd">
<td><p>カメラのミニドライバー</p></td>
<td><p>呼び出す<a href="https://msdn.microsoft.com/library/windows/hardware/ff568574" data-raw-source="[&lt;strong&gt;USBCAMD_AdapterReceivePacket&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568574)"> <strong>USBCAMD_AdapterReceivePacket</strong></a>します。</p></td>
</tr>
<tr class="even">
<td><p>USBCAMD2</p></td>
<td><p>ストリーム ヘッダー内のピンの数を入力します。</p></td>
</tr>
<tr class="odd">
<td><p>USBCAMD2</p></td>
<td><p>存在する場合は、デバイスのイベント テーブルを公開します。</p></td>
</tr>
<tr class="even">
<td><p>USBCAMD2</p></td>
<td><p>ストリーム情報のテーブルでは、エントリの値を修正します。 設定カテゴリの名前 (キャプチャまたはも)。</p></td>
</tr>
<tr class="odd">
<td><p>USBCAMD2</p></td>
<td><p>ストリーム プロパティ配列へのポインターを入力します。</p></td>
</tr>
</tbody>
</table>

## <a name="minidrivers-srbinitializationcomplete-handler"></a>ミニドライバーの SRB\_初期化\_完了ハンドラー

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>コンポーネント</th>
<th>操作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>カメラのミニドライバー</p></td>
<td><p>IRP_MJ_PNP と IRP_MN_QUERY_INTERFACE を使用して USBCAMD2 の GUID_USBCAMD_INTERFACE を取得します。</p></td>
</tr>
</tbody>
</table>

## <a name="minidrivers-srbgetdeviceproperty-handler"></a>ミニドライバーの SRB\_取得\_デバイス\_プロパティ ハンドラー

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>コンポーネント</th>
<th>操作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>カメラのミニドライバー</p></td>
<td><p>カメラのミニドライバーを処理するなどのプロパティを取得<a href="https://msdn.microsoft.com/library/windows/hardware/ff568122" data-raw-source="[PROPSETID_VIDCAP_VIDEOPROCAMP](https://msdn.microsoft.com/library/windows/hardware/ff568122)">PROPSETID_VIDCAP_VIDEOPROCAMP</a>、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff567802" data-raw-source="[PROPSETID_VIDCAP_CAMERACONTROL](https://msdn.microsoft.com/library/windows/hardware/ff567802)">PROPSETID_VIDCAP_CAMERACONTROL</a>と<a href="https://msdn.microsoft.com/library/windows/hardware/ff568120" data-raw-source="[PROPSETID_VIDCAP_VIDEOCONTROL](https://msdn.microsoft.com/library/windows/hardware/ff568120)">PROPSETID_VIDCAP_VIDEOCONTROL</a>などその他のカスタム プロパティを設定します。</p></td>
</tr>
</tbody>
</table>

## <a name="minidrivers-srbsetdeviceproperty-handler"></a>ミニドライバーの SRB\_設定\_デバイス\_プロパティ ハンドラー

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>コンポーネント</th>
<th>操作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>カメラのミニドライバー</p></td>
<td><p>カメラのミニドライバーの処理のパラメーターを取得することによって、プロパティを設定<a href="https://msdn.microsoft.com/library/windows/hardware/ff568122" data-raw-source="[PROPSETID_VIDCAP_VIDEOPROCAMP](https://msdn.microsoft.com/library/windows/hardware/ff568122)">PROPSETID_VIDCAP_VIDEOPROCAMP</a>、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff567802" data-raw-source="[PROPSETID_VIDCAP_CAMERACONTROL](https://msdn.microsoft.com/library/windows/hardware/ff567802)">PROPSETID_VIDCAP_CAMERACONTROL</a>と<a href="https://msdn.microsoft.com/library/windows/hardware/ff568120" data-raw-source="[PROPSETID_VIDCAP_VIDEOCONTROL](https://msdn.microsoft.com/library/windows/hardware/ff568120)">PROPSETID_VIDCAP_VIDEOCONTROL</a>、およびカスタム プロパティを設定します。</p></td>
</tr>
</tbody>
</table>

## <a name="minidrivers-srbgetdataintersection-handler"></a>ミニドライバーの SRB\_取得\_データ\_交差ハンドラー

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>コンポーネント</th>
<th>操作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>カメラのミニドライバー</p></td>
<td><p>返す、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff561656" data-raw-source="[&lt;strong&gt;KSDATAFORMAT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561656)"> <strong>KSDATAFORMAT</strong> </a>から構造体、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff561658" data-raw-source="[&lt;strong&gt;KSDATARANGE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561658)"> <strong>KSDATARANGE</strong> </a>構造体。</p></td>
</tr>
<tr class="even">
<td><p>カメラのミニドライバー</p></td>
<td><p>フレーム レートが要求されたことを確認する (<strong>VideoInfoHeader.AvgTimePerFrame</strong>) が要求されるビデオ形式の上限と下限の範囲内で。 制限を超えた場合、ミニドライバーが pSrb - で、次の値を修正する必要があります&gt;CommandData.IntersectInfo-&gt;Datarange:VideoInfoHeader.AvgTimePerFrame、VideoInfoHeader.dwBitRate します。</p></td>
</tr>
</tbody>
</table>

## <a name="minidrivers-srbopenstream-handler"></a>ミニドライバーの SRB\_オープン\_ストリーム ハンドラー

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>コンポーネント</th>
<th>操作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>カメラのミニドライバー</p></td>
<td><p>ビデオ形式を確認します。</p></td>
</tr>
<tr class="even">
<td><p>カメラのミニドライバー</p></td>
<td><p>呼び出す<a href="https://msdn.microsoft.com/library/windows/hardware/ff568574" data-raw-source="[&lt;strong&gt;USBCAMD_AdapterReceivePacket&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568574)"> <strong>USBCAMD_AdapterReceivePacket</strong></a>します。</p></td>
</tr>
<tr class="odd">
<td><p>USBCAMD2</p></td>
<td><p>カメラのミニドライバーで受け入れられるビデオ形式を保存します。</p></td>
</tr>
<tr class="even">
<td><p>USBCAMD2</p></td>
<td><p>呼び出すようにミニドライバーの<a href="https://msdn.microsoft.com/library/windows/hardware/ff557600" data-raw-source="[&lt;em&gt;CamAllocateBandwidthEx&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557600)"> <em>CamAllocateBandwidthEx</em> </a>ビデオ形式のデータに基づく帯域幅の割り当てし、ビデオ形式の最大バッファー サイズを取得するコールバック関数。</p></td>
</tr>
<tr class="odd">
<td><p>カメラのミニドライバー</p></td>
<td><p>要求されたフレーム レートと出力の windows のサイズに適合するアイソクロナス チャネルの最大パケット サイズを計算します。</p></td>
</tr>
<tr class="even">
<td><p>カメラのミニドライバー</p></td>
<td><p>最も近い別の設定を呼び出すことによって選択<a href="https://msdn.microsoft.com/library/windows/hardware/ff568625" data-raw-source="[&lt;strong&gt;USBCAMD_SelectAlternateInterface&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568625)"> <strong>USBCAMD_SelectAlternateInterface</strong></a>します。 ミニドライバーは、カメラによって生成できる最大フレーム サイズを USBCAMD2 を提供する必要があります。</p></td>
</tr>
<tr class="odd">
<td><p>カメラのミニドライバー</p></td>
<td><p>ハードウェアのカメラのスケーリングを設定します。 場合、レジストリに保存されている値または既定の設定に、カメラ コントロールを設定、初めてです。</p></td>
</tr>
<tr class="even">
<td><p>カメラのミニドライバー</p></td>
<td><p>ビデオの形式の制限内でフレーム レート (VideoInfoHeader.AvgTimePerFrame) があることを確認し、そうでない場合に修正します。</p></td>
</tr>
<tr class="odd">
<td><p>USBCAMD2</p></td>
<td><p>呼び出すようにミニドライバーの<a href="https://msdn.microsoft.com/library/windows/hardware/ff557640" data-raw-source="[&lt;em&gt;CamStartCaptureEx&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557640)"> <em>CamStartCaptureEx</em> </a>コールバック関数。</p></td>
</tr>
<tr class="even">
<td><p>カメラのミニドライバー</p></td>
<td><p>ハードウェアのキャプチャ モードを設定します。</p></td>
</tr>
<tr class="odd">
<td><p>USBCAMD2</p></td>
<td><p>アイソクロナスまたは一括転送を初期化します。</p></td>
</tr>
</tbody>
</table>

## <a name="minidrivers-srbclosestream-handler"></a>ミニドライバーの SRB\_閉じる\_ストリーム ハンドラー

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>コンポーネント</th>
<th>操作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>カメラのミニドライバー</p></td>
<td><p>呼び出す<a href="https://msdn.microsoft.com/library/windows/hardware/ff568574" data-raw-source="[&lt;strong&gt;USBCAMD_AdapterReceivePacket&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568574)"> <strong>USBCAMD_AdapterReceivePacket</strong></a>します。</p></td>
</tr>
<tr class="even">
<td><p>USBCAMD2</p></td>
<td><p>保留中の Irp USBCAMD2 に送信をキャンセルします。 保留中のデータのされる Srb を返す、 <em>stream.sys</em>クラス ドライバー。</p></td>
</tr>
<tr class="odd">
<td><p>USBCAMD2</p></td>
<td><p>呼び出すようにミニドライバーの<a href="https://msdn.microsoft.com/library/windows/hardware/ff557643" data-raw-source="[&lt;em&gt;CamStopCaptureEx&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557643)"> <em>CamStopCaptureEx</em> </a>コールバック関数。</p></td>
</tr>
<tr class="even">
<td><p>カメラのミニドライバー</p></td>
<td><p>カメラに停止キャプチャ コマンドを送信します。</p></td>
</tr>
<tr class="odd">
<td><p>USBCAMD2</p></td>
<td><p>呼び出すようにミニドライバーの<a href="https://msdn.microsoft.com/library/windows/hardware/ff557613" data-raw-source="[&lt;em&gt;CamFreeBandwidthEx&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557613)"> <em>CamFreeBandwidthEx</em> </a>アイソクロナスを解放するコールバック関数バスの帯域幅、該当する場合。</p></td>
</tr>
<tr class="even">
<td><p>カメラのミニドライバー</p></td>
<td><p>アイドル状態の代替設定を選択します。</p></td>
</tr>
<tr class="odd">
<td><p>USBCAMD2</p></td>
<td><p>USB パイプに関連付けられているリソースを解放します。</p></td>
</tr>
</tbody>
</table>

## <a name="minidrivers-srbuninitializedevice-handler"></a>ミニドライバーの SRB\_非\_デバイス ハンドラー

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>コンポーネント</th>
<th>操作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>カメラのミニドライバー</p></td>
<td><p>呼び出す<a href="https://msdn.microsoft.com/library/windows/hardware/ff568574" data-raw-source="[&lt;strong&gt;USBCAMD_AdapterReceivePacket&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568574)"> <strong>USBCAMD_AdapterReceivePacket</strong></a>します。</p></td>
</tr>
<tr class="even">
<td><p>USBCAMD2</p></td>
<td><p>任意のストリームが開いている場合は、呼び出すようにミニドライバーのして閉じます<a href="https://msdn.microsoft.com/library/windows/hardware/ff557643" data-raw-source="[&lt;em&gt;CamStopCaptureEx&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557643)"> <em>CamStopCaptureEx</em> </a>と<a href="https://msdn.microsoft.com/library/windows/hardware/ff557613" data-raw-source="[&lt;em&gt;CamFreeBandwidthEx&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557613)"> <em>CamFreeBandwidthEx</em> </a>コールバック各ストリームの機能です。</p></td>
</tr>
<tr class="odd">
<td><p>USBCAMD2</p></td>
<td><p>呼び出すようにミニドライバーの<a href="https://msdn.microsoft.com/library/windows/hardware/ff557646" data-raw-source="[&lt;em&gt;CamUnInitialize&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557646)"> <em>CamUnInitialize</em> </a>コールバック関数。</p></td>
</tr>
<tr class="even">
<td><p>カメラのミニドライバー</p></td>
<td><p>リソースを解放してクリーンアップします。</p></td>
</tr>
</tbody>
</table>

## <a name="minidrivers-srbsurpriseremoval-handler"></a>ミニドライバーの SRB\_突然\_削除ハンドラー

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>コンポーネント</th>
<th>操作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>カメラのミニドライバー</p></td>
<td><p>呼び出す<a href="https://msdn.microsoft.com/library/windows/hardware/ff568574" data-raw-source="[&lt;strong&gt;USBCAMD_AdapterReceivePacket&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568574)"> <strong>USBCAMD_AdapterReceivePacket</strong></a>します。</p></td>
</tr>
<tr class="even">
<td><p>USBCAMD2</p></td>
<td><p>保留中のデータのされる Srb をキャンセルし、STATUS_CANCELLED とされる Srb を返します。</p></td>
</tr>
<tr class="odd">
<td><p>USBCAMD2</p></td>
<td><p>呼び出すようにミニドライバーの<a href="https://msdn.microsoft.com/library/windows/hardware/ff557643" data-raw-source="[&lt;em&gt;CamStopCaptureEx&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557643)"> <em>CamStopCaptureEx</em> </a>と<a href="https://msdn.microsoft.com/library/windows/hardware/ff557613" data-raw-source="[&lt;em&gt;CamFreeBandwidthEx&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557613)"> <em>CamFreeBandwidthEx</em> </a>すべての開いているストリームにコールバック関数。</p></td>
</tr>
<tr class="even">
<td><p>USBCAMD2</p></td>
<td><p>上の読み書きされる Srb の後に続く SRB_SURPRISE_REMOVAL STATUS_CANCELLED を返します。</p></td>
</tr>
</tbody>
</table>

## <a name="minidrivers-srbsetdataformat-handler"></a>ミニドライバーの SRB\_設定\_データ\_形式ハンドラー

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>コンポーネント</th>
<th>操作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>カメラのミニドライバー</p></td>
<td><p>新しいビデオ形式を確認します。</p></td>
</tr>
<tr class="even">
<td><p>カメラのミニドライバー</p></td>
<td><p>呼び出す<a href="https://msdn.microsoft.com/library/windows/hardware/ff568634" data-raw-source="[&lt;em&gt;USBCAMD_SetVideoFormat&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568634)"> <em>USBCAMD_SetVideoFormat</em></a>します。</p></td>
</tr>
<tr class="odd">
<td><p>USBCAMD2</p></td>
<td><p>関連付けられているストリームの拡張子を持つ新しい形式を保存します。</p></td>
</tr>
</tbody>
</table>

## <a name="minidrivers-srbchangepowerstate-from-power-on-to-power-off-handler"></a>ミニドライバーの SRB\_変更\_POWER\_電源をオンから電源オフ ハンドラーへの状態

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>コンポーネント</th>
<th>操作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>カメラのミニドライバー</p></td>
<td><p>呼び出す<a href="https://msdn.microsoft.com/library/windows/hardware/ff568574" data-raw-source="[&lt;strong&gt;USBCAMD_AdapterReceivePacket&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568574)"> <strong>USBCAMD_AdapterReceivePacket</strong></a>します。</p></td>
</tr>
<tr class="even">
<td><p>USBCAMD2</p></td>
<td><p>該当する場合、アイソクロナス パイプでストリーミングを停止または保留中の一括または割り込みの転送をキャンセルします。</p></td>
</tr>
<tr class="odd">
<td><p>USBCAMD2</p></td>
<td><p>呼び出すようにミニドライバーの<a href="https://msdn.microsoft.com/library/windows/hardware/ff557643" data-raw-source="[&lt;em&gt;CamStopCaptureEx&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557643)"> <em>CamStopCaptureEx</em> </a>コールバック関数。</p></td>
</tr>
<tr class="even">
<td><p>カメラのミニドライバー</p></td>
<td><p>ハードウェアにキャプチャの停止コマンドを送信します。</p></td>
</tr>
</tbody>
</table>

## <a name="minidrivers-srbchangepowerstate-from-power-off-to-power-on-handler"></a>ミニドライバーの SRB\_変更\_POWER\_ハンドラーの電源をオンから電源オフ状態

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>コンポーネント</th>
<th>操作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>カメラのミニドライバー</p></td>
<td><p>呼び出す<a href="https://msdn.microsoft.com/library/windows/hardware/ff568574" data-raw-source="[&lt;strong&gt;USBCAMD_AdapterReceivePacket&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568574)"> <strong>USBCAMD_AdapterReceivePacket</strong></a>します。</p></td>
</tr>
<tr class="even">
<td><p>USBCAMD2</p></td>
<td><p>該当する場合、アイソクロナス パイプでストリーミングを再開または一括を再送信または USB クラスへの転送を中断します。</p></td>
</tr>
<tr class="odd">
<td><p>カメラのミニドライバー</p></td>
<td><p>カメラの設定とカメラの電力消費量を通常のレベルに復元します。</p></td>
</tr>
<tr class="even">
<td><p>USBCAMD2</p></td>
<td><p>呼び出すようにミニドライバーの<a href="https://msdn.microsoft.com/library/windows/hardware/ff557643" data-raw-source="[&lt;em&gt;CamStopCaptureEx&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557643)"> <em>CamStopCaptureEx</em> </a>コールバック関数。</p></td>
</tr>
<tr class="odd">
<td><p>USBCAMD2</p></td>
<td><p>呼び出すようにミニドライバーの<a href="https://msdn.microsoft.com/library/windows/hardware/ff557640" data-raw-source="[&lt;em&gt;CamStartCaptureEx&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557640)"> <em>CamStartCaptureEx</em> </a>コールバック関数。</p></td>
</tr>
</tbody>
</table>
