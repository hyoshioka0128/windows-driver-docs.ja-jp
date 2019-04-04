---
title: イメージング デバイス参照
description: イメージング デバイス参照
ms.assetid: 2ee6ce92-44dc-4c59-a438-f65b41f3b43a
ms.date: 09/14/2017
ms.localizationpriority: medium
ms.openlocfilehash: b69702cc3df8fdae47c717be62f9d8273623c1dd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560698"
---
# <a name="imaging-devices-reference"></a>イメージング デバイス参照

このセクションには、次のテクノロジに関するリファレンス情報が含まれています。

[イメージング デバイスのデバイスのインターフェイス クラス](device-interface-classes-for-imaging-devices.md)

[IWiaMiniDrv インターフェイス](https://msdn.microsoft.com/library/windows/hardware/ff545027)

[インターフェイスを静止画像します。](https://msdn.microsoft.com/library/windows/hardware/ff548281)

[参照をデバイス上の web サービス](https://msdn.microsoft.com/library/windows/hardware/ff549148)

## <a name="wia-and-sti-driver-reference-table"></a>WIA と STI ドライバーの参照テーブル

次の表には、Windows Image Acquisition (WIA) ドライバーとまだイメージング (STI) ドライバーの参照情報が含まれています。 これらのドライバーでは、スキャナー、静止画像をキャプチャするには、カメラなどのデバイスを制御します。 これらのドライバーの詳細については、[Windows Image Acquisition ドライバー](https://msdn.microsoft.com/library/windows/hardware/ff553346)と[イメージ ドライバーも](https://msdn.microsoft.com/library/windows/hardware/ff548278)を参照してください。

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
<td><p><a href="device-interface-classes-for-imaging-devices.md" data-raw-source="[Device Interface Classes for Imaging Devices](device-interface-classes-for-imaging-devices.md)">イメージング デバイスのデバイスのインターフェイス クラス</a></p></td>
<td><p>イメージング デバイスのデバイス クラス GUID です。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff545027" data-raw-source="[IWiaMiniDrv Interface](https://msdn.microsoft.com/library/windows/hardware/ff545027)">IWiaMiniDrv インターフェイス</a></p></td>
<td><p>WIA ミニドライバーと WIA サービスの間のすべての通信を管理するためのインターフェイス。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551473" data-raw-source="[WIA Driver Services Library Functions](https://msdn.microsoft.com/library/windows/hardware/ff551473)">WIA ドライバー サービス ライブラリ関数</a></p></td>
<td><p>WIA ミニドライバー デバイス アイテムとデータの転送を管理するために使用するヘルパー関数です。</p></td>
</tr>
<tr class="even">
<td><p><a href="wia-properties.md" data-raw-source="[WIA Properties](wia-properties.md)">WIA プロパティ</a></p></td>
<td><p>状態、機能、およびデバイスの識別情報を含め、WIA デバイスのプロパティです。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553303" data-raw-source="[WIA Utility Library Functions and Classes](https://msdn.microsoft.com/library/windows/hardware/ff553303)">WIA ユーティリティ ライブラリ関数およびクラス</a></p></td>
<td><p>ユーティリティ関数とデバッグをサポートする一般的なタスクを実行して、WIA ミニドライバーで使用されるクラス。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543943" data-raw-source="[IWiaMiniDrvCallBack Interface](https://msdn.microsoft.com/library/windows/hardware/ff543943)">IWiaMiniDrvCallBack インターフェイス</a></p></td>
<td><p>WIA サービスと、WIA ミニドライバーの間の状態とイメージ データを転送するためのコールバック インターフェイス。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543896" data-raw-source="[IWiaDrvItem Interface](https://msdn.microsoft.com/library/windows/hardware/ff543896)">IWiaDrvItem インターフェイス</a></p></td>
<td><p>WIA ミニドライバー WIA ドライバー項目のツリーを管理するために使用するインターフェイスです。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543907" data-raw-source="[IWiaErrorHandler Interface](https://msdn.microsoft.com/library/windows/hardware/ff543907)">IWiaErrorHandler インターフェイス</a></p></td>
<td><p>エラー状態を提供し、エラーからの回復をサポートするために、WIA ミニドライバーによって使用されるインターフェイス。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543921" data-raw-source="[IWiaImageFilter Interface](https://msdn.microsoft.com/library/windows/hardware/ff543921)">IWiaImageFilter インターフェイス</a></p></td>
<td><p>インターフェイスは、イメージ処理フィルターによって実装され、フィルターとの通信に WIA サービスによって呼び出されます。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543937" data-raw-source="[IWiaLog Interface and Diagnostic Log Macros](https://msdn.microsoft.com/library/windows/hardware/ff543937)">IWiaLog インターフェイスおよび診断ログのマクロ</a></p></td>
<td><p>インターフェイスとレコードのトレース、エラー、および診断のログ ファイルに警告メッセージに WIA ミニドライバーで使用されるマクロです。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff545035" data-raw-source="[IWiaSegmentationFilter Interface](https://msdn.microsoft.com/library/windows/hardware/ff545035)">IWiaSegmentationFilter インターフェイス</a></p></td>
<td><p>WIA ミニドライバーによってセグメント化されたイメージで領域を検出するために使用されるインターフェイス。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff545043" data-raw-source="[IWiaTransferCallback Interface](https://msdn.microsoft.com/library/windows/hardware/ff545043)">IWiaTransferCallback インターフェイス</a></p></td>
<td><p>インターフェイスは、イメージ処理フィルターによって実装され、イメージ ストリームの処理を開始するには、WIA サービスによって呼び出されます。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552720" data-raw-source="[WIA Microdriver Functions, Structures, and Commands](https://msdn.microsoft.com/library/windows/hardware/ff552720)">WIA Microdriver 関数、構造、およびコマンド</a></p></td>
<td><p>関数、構造、および WIA microdrivers で使用されるコマンド。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553281" data-raw-source="[WIA User Interface Extensions](https://msdn.microsoft.com/library/windows/hardware/ff553281)">WIA ユーザー インターフェイスの拡張機能</a></p></td>
<td><p>デバイスの製造元、デバイスのカスタム ユーザー インターフェイスを提供するために使用するインターフェイスです。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552803" data-raw-source="[WIA Structures](https://msdn.microsoft.com/library/windows/hardware/ff552803)">WIA 構造体</a></p></td>
<td><p>ドライバー レベル WIA メソッドや関数で使用する構造体。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548281" data-raw-source="[Still Image Interfaces](https://msdn.microsoft.com/library/windows/hardware/ff548281)">インターフェイスを静止画像します。</a></p></td>
<td><p>インターフェイス、構造体、データ型、および STI ドライバーによって使用される制御コード。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff547963" data-raw-source="[Web Services on Devices Reference](https://msdn.microsoft.com/library/windows/hardware/ff547963)">参照をデバイス上の web サービス</a></p></td>
<td><p>スキャン サービス (WS スキャン) を含むデバイスについては、上の web サービス</p></td>
</tr>
</tbody>
</table>

 

 

 





