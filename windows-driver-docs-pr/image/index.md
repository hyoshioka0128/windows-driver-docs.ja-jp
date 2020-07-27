---
title: イメージング デバイス ドライバー設計ガイド
description: イメージング デバイス ドライバー設計ガイド
ms.assetid: dfdeeec8-bd06-452a-9189-87b20ce27699
ms.date: 04/20/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.openlocfilehash: 36924fab98903a717ebb001ff08973af31f4eb2d
ms.sourcegitcommit: 6914901515545eda08b2c35bef816e6e2711a5b6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/22/2020
ms.locfileid: "86944614"
---
# <a name="imaging-device-driver-design-guide"></a>イメージング デバイス ドライバー設計ガイド


このセクションでは、Windows Image Acquisition (WIA) ドライバー、Still Image (STI) ドライバー、Web Services on Devices (WSD) について説明します。

> [!NOTE]
> WIA プログラミング インターフェイスは、最新の Windows オペレーティング システム用のイメージング ドライバーを開発するために使用されます。 STI プログラミング インターフェイスは、レガシ Windows オペレーティング システム用のイメージング ドライバーを開発するために使用されていました。 STI プログラミング インターフェイスのドキュメントは今後のリリースでアーカイブされる予定です。 

## <a name="in-this-section"></a>このセクションの内容

- [イメージング デバイスのデバイス インターフェイス クラス](device-interface-classes-for-imaging-devices.md)

- [Windows イメージ取得ドライバー](windows-image-acquisition-drivers.md)

- [WIA のプロパティ](about-wia-properties.md)

- [64 ビットと WIA](64-bit-and-wia.md)

- [WIA 互換レイヤー](wia-compatibility-layer.md)

- [WIA ドライバー フィルター](wia-driver-filters.md)

- [WIA 項目ツリー](wia-item-trees.md)

- [WIA と Web Services for Devices](wia-with-web-services-for-devices.md)

- [WIA ドライバーの開発](developing-a-wia-driver.md)

- [WIA カメラ ドライバーの開発](developing-a-wia-camera-driver.md)

- [WIA ミニドライバーのベスト プラクティス](wia-minidriver-best-practices.md)

- [WIA マイクロドライバーのコマンド](wia-microdriver-commands.md)

- [WIA ミニドライバーの構築、トラブルシューティング、デバッグ](building--troubleshooting-and-debugging-wia-minidrivers.md)

- [WIA のサンプルとツール](wia-samples-and-tools.md)

- [Still Image ドライバー](still-image-drivers.md)

- [Web Services on Devices](web-services-on-devices.md)

- [Web Services on Devices リファレンス](web-services-on-devices-reference.md)

## <a name="wia-and-sti-driver-reference"></a>WIA および STI ドライバーのリファレンス

次の表に、Windows Image Acquisition (WIA) ドライバーと Still Imaging (STI) ドライバーのリファレンス情報を記載します。 これらのドライバーは、静止画像をキャプチャする、スキャナーやカメラなどのデバイスを制御します。 これらのドライバーの詳細については、「[Windows Image Acquisition ドライバー](https://docs.microsoft.com/windows-hardware/drivers/image/windows-image-acquisition-drivers)」と「[Still Image ドライバー](https://docs.microsoft.com/windows-hardware/drivers/image/still-image-drivers)」を参照してください。

以下のセクションでは、WIA および STI ドライバーで使用されるインターフェイス、関数、構造体、プロパティについて説明します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Section</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="device-interface-classes-for-imaging-devices.md" data-raw-source="[Device Interface Classes for Imaging Devices](device-interface-classes-for-imaging-devices.md)">イメージング デバイスのデバイス インターフェイス クラス</a></p></td>
<td><p>イメージング デバイス用のデバイス クラス GUID。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nn-wiamindr_lh-iwiaminidrv" data-raw-source="[IWiaMiniDrv Interface](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nn-wiamindr_lh-iwiaminidrv)">IWiaMiniDrv インターフェイス</a></p></td>
<td><p>WIA ミニドライバーと WIA サービス間のすべての通信を管理するためのインターフェイス。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/index" data-raw-source="[WIA Driver Services Library Functions](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/index)">WIA ドライバー サービス ライブラリ関数</a></p></td>
<td><p>デバイス項目とデータ転送を管理するために WIA ミニドライバーによって使用されるヘルパー関数。</p></td>
</tr>
<tr class="even">
<td><p><a href="wia-properties.md" data-raw-source="[WIA Properties](wia-properties.md)">WIA のプロパティ</a></p></td>
<td><p>状態、機能、デバイス識別情報など、WIA デバイスのプロパティ。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/_image/index" data-raw-source="[WIA Utility Library Functions and Classes](https://docs.microsoft.com/windows-hardware/drivers/ddi/_image/index)">WIA ユーティリティ ライブラリの関数とクラス</a></p></td>
<td><p>デバッグをサポートし、一般的なタスクを実行するために、WIA ミニドライバーによって使用されるユーティリティ関数とクラス。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nn-wiamindr_lh-iwiaminidrvcallback" data-raw-source="[IWiaMiniDrvCallBack Interface](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nn-wiamindr_lh-iwiaminidrvcallback)">IWiaMiniDrvCallBack インターフェイス</a></p></td>
<td><p>WIA サービスと WIA ミニドライバー間で状態と画像データを転送するためのコールバック インターフェイス。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nn-wiamindr_lh-iwiadrvitem" data-raw-source="[IWiaDrvItem Interface](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nn-wiamindr_lh-iwiadrvitem)">IWiaDrvItem インターフェイス</a></p></td>
<td><p>WIA ドライバー項目のツリーを管理するために WIA ミニドライバーによって使用されるインターフェイス。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wia_lh/nn-wia_lh-iwiaerrorhandler" data-raw-source="[IWiaErrorHandler Interface](https://docs.microsoft.com/windows-hardware/drivers/ddi/wia_lh/nn-wia_lh-iwiaerrorhandler)">IWiaErrorHandler インターフェイス</a></p></td>
<td><p>エラー状態を提供し、エラーの回復をサポートするために、WIA ミニドライバーによって使用されるインターフェイス。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wia_lh/nn-wia_lh-iwiaimagefilter" data-raw-source="[IWiaImageFilter Interface](https://docs.microsoft.com/windows-hardware/drivers/ddi/wia_lh/nn-wia_lh-iwiaimagefilter)">IWiaImageFilter インターフェイス</a></p></td>
<td><p>画像処理フィルターによって実装され、そのフィルターと通信するために WIA サービスによって呼び出されるインターフェイス。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/_image/index" data-raw-source="[IWiaLog Interface and Diagnostic Log Macros](https://docs.microsoft.com/windows-hardware/drivers/ddi/_image/index)">IWiaLog インターフェイスと診断ログ マクロ</a></p></td>
<td><p>トレース、エラー、警告メッセージを診断ログ ファイルに記録するために WIA ミニドライバーによって使用されるインターフェイスとマクロ。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wia_lh/nn-wia_lh-iwiasegmentationfilter" data-raw-source="[IWiaSegmentationFilter Interface](https://docs.microsoft.com/windows-hardware/drivers/ddi/wia_lh/nn-wia_lh-iwiasegmentationfilter)">IWiaSegmentationFilter インターフェイス</a></p></td>
<td><p>セグメント化された画像内の領域を検出するために WIA ミニドライバーによって使用されるインターフェイス。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wia_lh/nn-wia_lh-iwiatransfercallback" data-raw-source="[IWiaTransferCallback Interface](https://docs.microsoft.com/windows-hardware/drivers/ddi/wia_lh/nn-wia_lh-iwiatransfercallback)">IWiaTransferCallback インターフェイス</a></p></td>
<td><p>画像処理フィルターによって実装され、画像ストリームの処理を開始するために WIA サービスによって呼び出されるインターフェイス。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/_image/index" data-raw-source="[WIA Microdriver Functions, Structures, and Commands](https://docs.microsoft.com/windows-hardware/drivers/ddi/_image/index)">WIA マイクロドライバーの関数、構造体、コマンド</a></p></td>
<td><p>WIA マイクロドライバーで使用される関数、構造体、コマンド。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiadevd/index" data-raw-source="[WIA User Interface Extensions](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiadevd/index)">WIA ユーザー インターフェイスの拡張機能</a></p></td>
<td><p>自社デバイスのカスタム ユーザー インターフェイスを提供するためにデバイス ベンダーによって使用されるインターフェイス。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/_image/index" data-raw-source="[WIA Structures](https://docs.microsoft.com/windows-hardware/drivers/ddi/_image/index)">WIA 構造体</a></p></td>
<td><p>ドライバー レベルの WIA メソッドおよび関数によって使用される構造体。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/_image/index" data-raw-source="[Still Image Interfaces](https://docs.microsoft.com/windows-hardware/drivers/ddi/_image/index)">Still Image インターフェイス</a></p></td>
<td><p>STI ドライバーによって使用されるインターフェイス、構造体、データ型、制御コード。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/image/scan-service--ws-scan--schema" data-raw-source="[Web Services on Devices Reference](https://docs.microsoft.com/windows-hardware/drivers/image/scan-service--ws-scan--schema)">Web Services on Devices リファレンス</a></p></td>
<td><p>スキャン サービス (WS-SCAN) を含む、Web Services on Devices の情報</p></td>
</tr>
</tbody>
</table>

## <a name="related-sections"></a>関連セクション

- [イメージング DDI リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_image)
