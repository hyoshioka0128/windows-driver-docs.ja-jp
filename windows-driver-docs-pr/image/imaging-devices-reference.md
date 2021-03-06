---
title: イメージング デバイス参照
description: イメージング デバイス参照
ms.assetid: 2ee6ce92-44dc-4c59-a438-f65b41f3b43a
ms.date: 09/14/2017
ms.localizationpriority: medium
ms.openlocfilehash: bf2827957c41ad45ee3253752e41ee5a235edac2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373532"
---
# <a name="imaging-devices-reference"></a>イメージング デバイス参照

このセクションには、次のテクノロジに関するリファレンス情報が含まれています。

[イメージング デバイスのデバイス インターフェイス クラス](device-interface-classes-for-imaging-devices.md)

[IWiaMiniDrv インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nn-wiamindr_lh-iwiaminidrv)

[インターフェイスを静止画像します。](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_image/index)

[Web Services on Devices リファレンス](https://docs.microsoft.com/windows-hardware/drivers/image/web-services-on-devices-reference)

## <a name="wia-and-sti-driver-reference-table"></a>WIA と STI ドライバーの参照テーブル

次の表には、Windows Image Acquisition (WIA) ドライバーとまだイメージング (STI) ドライバーの参照情報が含まれています。 これらのドライバーでは、スキャナー、静止画像をキャプチャするには、カメラなどのデバイスを制御します。 これらのドライバーの詳細については、次を参照してください。 [Windows Image Acquisition ドライバー](https://docs.microsoft.com/windows-hardware/drivers/image/windows-image-acquisition-drivers)と[イメージ ドライバーも](https://docs.microsoft.com/windows-hardware/drivers/image/still-image-drivers)します。

次のセクションでは、インターフェイス、関数、構造、および WIA と STI ドライバーによって使用されるプロパティについて説明します。

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
<td><p><a href="device-interface-classes-for-imaging-devices.md" data-raw-source="[Device Interface Classes for Imaging Devices](device-interface-classes-for-imaging-devices.md)">イメージング デバイスのデバイス インターフェイス クラス</a></p></td>
<td><p>イメージング デバイスのデバイス クラス GUID です。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nn-wiamindr_lh-iwiaminidrv" data-raw-source="[IWiaMiniDrv Interface](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nn-wiamindr_lh-iwiaminidrv)">IWiaMiniDrv インターフェイス</a></p></td>
<td><p>WIA ミニドライバーと WIA サービスの間のすべての通信を管理するためのインターフェイス。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/index" data-raw-source="[WIA Driver Services Library Functions](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/index)">WIA ドライバー サービス ライブラリ関数</a></p></td>
<td><p>WIA ミニドライバー デバイス アイテムとデータの転送を管理するために使用するヘルパー関数です。</p></td>
</tr>
<tr class="even">
<td><p><a href="wia-properties.md" data-raw-source="[WIA Properties](wia-properties.md)">WIA のプロパティ</a></p></td>
<td><p>状態、機能、およびデバイスの識別情報を含め、WIA デバイスのプロパティです。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_image/index" data-raw-source="[WIA Utility Library Functions and Classes](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_image/index)">WIA ユーティリティ ライブラリ関数およびクラス</a></p></td>
<td><p>ユーティリティ関数とデバッグをサポートする一般的なタスクを実行して、WIA ミニドライバーで使用されるクラス。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nn-wiamindr_lh-iwiaminidrvcallback" data-raw-source="[IWiaMiniDrvCallBack Interface](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nn-wiamindr_lh-iwiaminidrvcallback)">IWiaMiniDrvCallBack インターフェイス</a></p></td>
<td><p>WIA サービスと、WIA ミニドライバーの間の状態とイメージ データを転送するためのコールバック インターフェイス。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nn-wiamindr_lh-iwiadrvitem" data-raw-source="[IWiaDrvItem Interface](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nn-wiamindr_lh-iwiadrvitem)">IWiaDrvItem インターフェイス</a></p></td>
<td><p>WIA ミニドライバー WIA ドライバー項目のツリーを管理するために使用するインターフェイスです。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wia_lh/nn-wia_lh-iwiaerrorhandler" data-raw-source="[IWiaErrorHandler Interface](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wia_lh/nn-wia_lh-iwiaerrorhandler)">IWiaErrorHandler インターフェイス</a></p></td>
<td><p>エラー状態を提供し、エラーからの回復をサポートするために、WIA ミニドライバーによって使用されるインターフェイス。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wia_lh/nn-wia_lh-iwiaimagefilter" data-raw-source="[IWiaImageFilter Interface](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wia_lh/nn-wia_lh-iwiaimagefilter)">IWiaImageFilter インターフェイス</a></p></td>
<td><p>インターフェイスは、イメージ処理フィルターによって実装され、フィルターとの通信に WIA サービスによって呼び出されます。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_image/index" data-raw-source="[IWiaLog Interface and Diagnostic Log Macros](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_image/index)">IWiaLog インターフェイスおよび診断ログのマクロ</a></p></td>
<td><p>インターフェイスとレコードのトレース、エラー、および診断のログ ファイルに警告メッセージに WIA ミニドライバーで使用されるマクロです。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wia_lh/nn-wia_lh-iwiasegmentationfilter" data-raw-source="[IWiaSegmentationFilter Interface](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wia_lh/nn-wia_lh-iwiasegmentationfilter)">IWiaSegmentationFilter インターフェイス</a></p></td>
<td><p>WIA ミニドライバーによってセグメント化されたイメージで領域を検出するために使用されるインターフェイス。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wia_lh/nn-wia_lh-iwiatransfercallback" data-raw-source="[IWiaTransferCallback Interface](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wia_lh/nn-wia_lh-iwiatransfercallback)">IWiaTransferCallback インターフェイス</a></p></td>
<td><p>インターフェイスは、イメージ処理フィルターによって実装され、イメージ ストリームの処理を開始するには、WIA サービスによって呼び出されます。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_image/index" data-raw-source="[WIA Microdriver Functions, Structures, and Commands](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_image/index)">WIA Microdriver 関数、構造、およびコマンド</a></p></td>
<td><p>関数、構造、および WIA microdrivers で使用されるコマンド。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiadevd/index" data-raw-source="[WIA User Interface Extensions](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiadevd/index)">WIA ユーザー インターフェイスの拡張機能</a></p></td>
<td><p>デバイスの製造元、デバイスのカスタム ユーザー インターフェイスを提供するために使用するインターフェイスです。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_image/index" data-raw-source="[WIA Structures](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_image/index)">WIA 構造体</a></p></td>
<td><p>ドライバー レベル WIA メソッドや関数で使用する構造体。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_image/index" data-raw-source="[Still Image Interfaces](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_image/index)">インターフェイスを静止画像します。</a></p></td>
<td><p>インターフェイス、構造体、データ型、および STI ドライバーによって使用される制御コード。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/image/scan-service--ws-scan--schema" data-raw-source="[Web Services on Devices Reference](https://docs.microsoft.com/windows-hardware/drivers/image/scan-service--ws-scan--schema)">Web Services on Devices リファレンス</a></p></td>
<td><p>スキャン サービス (WS スキャン) を含むデバイスについては、上の web サービス</p></td>
</tr>
</tbody>
</table>

 

 

 





