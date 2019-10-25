---
title: イメージングデバイスのリファレンス
description: イメージングデバイスのリファレンス
ms.assetid: 2ee6ce92-44dc-4c59-a438-f65b41f3b43a
ms.date: 09/14/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1df3a2855b9c19b7b48484ef5ab38c75994c5cbc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840828"
---
# <a name="imaging-devices-reference"></a>イメージングデバイスのリファレンス

このセクションには、次のテクノロジに関するリファレンス情報が含まれています。

[デバイスをイメージングするためのデバイスインターフェイスクラス](device-interface-classes-for-imaging-devices.md)

[IWiaMiniDrv インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nn-wiamindr_lh-iwiaminidrv)

[静止画像インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_image/index)

[Web Services on Devices リファレンス](https://docs.microsoft.com/windows-hardware/drivers/image/web-services-on-devices-reference)

## <a name="wia-and-sti-driver-reference-table"></a>WIA および STI ドライバーのリファレンス表

次の表には、Windows イメージ取得 (WIA) ドライバーと、引き続きイメージング (STI) ドライバーのリファレンス情報が含まれています。 これらのドライバーは、まだイメージをキャプチャするスキャナーやカメラなどのデバイスを制御します。 これらのドライバーの詳細については、「 [Windows イメージ取得ドライバー](https://docs.microsoft.com/windows-hardware/drivers/image/windows-image-acquisition-drivers) 」および「[イメージドライバー](https://docs.microsoft.com/windows-hardware/drivers/image/still-image-drivers)」を参照してください。

以下のセクションでは、WIA および STI ドライバーで使用されるインターフェイス、関数、構造体、およびプロパティについて説明します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>セクション</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="device-interface-classes-for-imaging-devices.md" data-raw-source="[Device Interface Classes for Imaging Devices](device-interface-classes-for-imaging-devices.md)">デバイスをイメージングするためのデバイスインターフェイスクラス</a></p></td>
<td><p>イメージングデバイス用のデバイスクラス GUID。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nn-wiamindr_lh-iwiaminidrv" data-raw-source="[IWiaMiniDrv Interface](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nn-wiamindr_lh-iwiaminidrv)">IWiaMiniDrv インターフェイス</a></p></td>
<td><p>WIA ミニドライバーと WIA サービス間のすべての通信を管理するためのインターフェイスです。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/index" data-raw-source="[WIA Driver Services Library Functions](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/index)">WIA ドライバーサービスライブラリ関数</a></p></td>
<td><p>デバイス項目とデータ転送を管理するために、WIA ミニドライバーによって使用されるヘルパー関数。</p></td>
</tr>
<tr class="even">
<td><p><a href="wia-properties.md" data-raw-source="[WIA Properties](wia-properties.md)">WIA のプロパティ</a></p></td>
<td><p>状態、機能、デバイス識別情報など、WIA デバイスのプロパティ。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/_image/index" data-raw-source="[WIA Utility Library Functions and Classes](https://docs.microsoft.com/windows-hardware/drivers/ddi/_image/index)">WIA ユーティリティライブラリの関数とクラス</a></p></td>
<td><p>デバッグおよび一般的なタスクの実行をサポートするために、WIA ミニドライバーによって使用されるユーティリティ関数とクラス。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nn-wiamindr_lh-iwiaminidrvcallback" data-raw-source="[IWiaMiniDrvCallBack Interface](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nn-wiamindr_lh-iwiaminidrvcallback)">IWiaMiniDrvCallBack インターフェイス</a></p></td>
<td><p>WIA サービスと WIA ミニドライバーの間で状態とイメージデータを転送するためのコールバックインターフェイス。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nn-wiamindr_lh-iwiadrvitem" data-raw-source="[IWiaDrvItem Interface](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nn-wiamindr_lh-iwiadrvitem)">IWiaDrvItem インターフェイス</a></p></td>
<td><p>Wia ドライバー項目のツリーを管理するために、WIA ミニドライバーによって使用されるインターフェイスです。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wia_lh/nn-wia_lh-iwiaerrorhandler" data-raw-source="[IWiaErrorHandler Interface](https://docs.microsoft.com/windows-hardware/drivers/ddi/wia_lh/nn-wia_lh-iwiaerrorhandler)">IWiaErrorHandler インターフェイス</a></p></td>
<td><p>エラー状態を提供し、エラーの回復をサポートするために、WIA ミニドライバーによって使用されるインターフェイスです。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wia_lh/nn-wia_lh-iwiaimagefilter" data-raw-source="[IWiaImageFilter Interface](https://docs.microsoft.com/windows-hardware/drivers/ddi/wia_lh/nn-wia_lh-iwiaimagefilter)">IWiaImageFilter インターフェイス</a></p></td>
<td><p>画像処理フィルターによって実装され、フィルターと通信するために WIA サービスによって呼び出されるインターフェイス。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/_image/index" data-raw-source="[IWiaLog Interface and Diagnostic Log Macros](https://docs.microsoft.com/windows-hardware/drivers/ddi/_image/index)">IWiaLog インターフェイスと診断ログマクロ</a></p></td>
<td><p>トレース、エラー、警告メッセージを診断ログファイルに記録するために、WIA ミニドライバーによって使用されるインターフェイスとマクロ。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wia_lh/nn-wia_lh-iwiasegmentationfilter" data-raw-source="[IWiaSegmentationFilter Interface](https://docs.microsoft.com/windows-hardware/drivers/ddi/wia_lh/nn-wia_lh-iwiasegmentationfilter)">IWiaSegmentationFilter インターフェイス</a></p></td>
<td><p>セグメント化されたイメージ内の領域を検出するために、WIA ミニドライバーによって使用されるインターフェイス。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wia_lh/nn-wia_lh-iwiatransfercallback" data-raw-source="[IWiaTransferCallback Interface](https://docs.microsoft.com/windows-hardware/drivers/ddi/wia_lh/nn-wia_lh-iwiatransfercallback)">Iwiatransのコールバックインターフェイス</a></p></td>
<td><p>イメージ処理フィルターによって実装され、イメージストリームの処理を開始するために、WIA サービスによって呼び出されるインターフェイス。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/_image/index" data-raw-source="[WIA Microdriver Functions, Structures, and Commands](https://docs.microsoft.com/windows-hardware/drivers/ddi/_image/index)">WIA マイクロドライバーの関数、構造体、およびコマンド</a></p></td>
<td><p>WIA マイクロドライバで使用される関数、構造体、およびコマンド。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiadevd/index" data-raw-source="[WIA User Interface Extensions](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiadevd/index)">WIA ユーザーインターフェイスの拡張機能</a></p></td>
<td><p>デバイスのカスタムユーザーインターフェイスを提供するために、デバイスベンダーによって使用されるインターフェイス。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/_image/index" data-raw-source="[WIA Structures](https://docs.microsoft.com/windows-hardware/drivers/ddi/_image/index)">WIA 構造体</a></p></td>
<td><p>ドライバーレベルの WIA メソッドおよび関数によって使用される構造体。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/_image/index" data-raw-source="[Still Image Interfaces](https://docs.microsoft.com/windows-hardware/drivers/ddi/_image/index)">静止画像インターフェイス</a></p></td>
<td><p>STI ドライバーによって使用されるインターフェイス、構造体、データ型、および制御コード。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/image/scan-service--ws-scan--schema" data-raw-source="[Web Services on Devices Reference](https://docs.microsoft.com/windows-hardware/drivers/image/scan-service--ws-scan--schema)">Web Services on Devices リファレンス</a></p></td>
<td><p>スキャンサービスを含む、デバイス上の Web サービスの情報 (WS-MANAGEMENT)</p></td>
</tr>
</tbody>
</table>

 

 

 





