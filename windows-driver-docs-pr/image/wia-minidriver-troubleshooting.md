---
title: WIA ミニドライバーのトラブルシューティング
description: WIA ミニドライバーのトラブルシューティング
ms.assetid: a0944bdd-56c4-4f7b-b542-eb353cd4d1f2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6a6057edfecf9868dfab28e0fdc6135d28a32474
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355193"
---
# <a name="wia-minidriver-troubleshooting"></a>WIA ミニドライバーのトラブルシューティング





既定では、WIA サービスがという名前のファイルにエラーをログ*wiadebug.log*で、 **%** <em>windir</em> **%** ディレクトリ。 WIA サービスは、このファイルの情報は、ドライバーの開発中に非常に便利です。 次の例では、一般的な問題を示しています、表示方法の情報は、 *wiadebug.log*ファイルを使用して、問題の解決策を検索します。

開発者は、開発中のスキャナーのドライバーをテストするアプリケーションを書き込みます。 テストの 1 つ、として、開発者は、スキャナーのドットを 1200 にインチ (dpi) ごとにこの操作がエラーを生成する通知を設定しようとします。 次に示します Wiadebug.log ファイルを参照してください。

```console
wiasGetChangedValueLong, validate prop 6147 failed hr: 0x80070057
wiasUpdateScanRect, CheckXResAndUpdate failed (0x80070057)
CDrvWrap::WIA_drvValidateItemProperties, Error calling driver:
drvValidateItemProperties with hr = 0x80070057 (This is normal if the app wrote an invalid value)
```

これらのログ エントリは、アプリケーションが無効な値を記述したこと、ドライバーを報告することを示します。 正確な問題が何の情報からオフになります。 開発者が増加すると、エラーと警告を報告する WIA ログ記録レベル*wiadebug.log*次のような出力が生成されます。

```console
wiasValidateItemProperties, invalid LIST value for : 
    (propID) Horizontal Resolution, value = 1200
Valid values are:
    75
    100
    150
    200
    300
    600
 wiasGetChangedValueLong, validate prop 6147 failed hr: 0x80070057
wiasUpdateScanRect, CheckXResAndUpdate failed (0x80070057)
 CDrvWrap::WIA_drvValidateItemProperties, Error calling driver: 
 drvValidateItemProperties with hr = 0x80070057 (This is normal if the app wrote an invalid value)
```

出力は、水平方向の解像度プロパティが、エラーの原因であるかを示しています。 解像度に 1200 に設定しようとして、アプリケーションが、1200 にサポートされている解像度の一覧は含まれません。 したがって、WIA サービス検証ヘルパー [ **wiasValidateItemProperties** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasvalidateitemproperties)はこの値を設定する要求を拒否します。

これで問題を特定すると、ドライバーまたはアプリケーションを変更する必要がありますがあるかどうかを判断する開発者の責任です。 スキャナーの仕様では、100 と 1400 の dpi の解像度ですべてをサポートするように、ドライバーが 1200 dpi の要求を処理できる必要があります。 スキャナーがこの設定をサポートしていない場合は、このプロパティの無効な値を水平方向の解像度を設定するのには再試行されませんので、アプリケーションを変更しなければなりません。 ここでは、アプリケーション、確認する値がこの値にプロパティを設定する前に有効であります。

ログ記録レベルは、レジストリ内のエントリによって制御されます。 WIA、このキーはで存在します。

**HKLM\\System\\CurrentControlSet\\Control\\StillImage\\Debug\\** <em>MODULE\_NAME</em> **\\DebugFlags**

この例では、モジュールで\_名は、適切なバイナリ モジュールの名前。 これは、WIA サービス*wiaservc.dll*します。 値**デバッグ フラグ**ログ記録レベルを制御します。 3 つの設定は、次の表に与えられます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Value</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0x00000001</p></td>
<td><p>エラー メッセージを表示します。</p></td>
</tr>
<tr class="even">
<td><p>0x00000002</p></td>
<td><p>警告メッセージを表示します。</p></td>
</tr>
<tr class="odd">
<td><p>0x00000004</p></td>
<td><p>トレース メッセージを表示します。</p></td>
</tr>
</tbody>
</table>

値**デバッグ フラグ**フラグ値です (つまり、さまざまな設定をビットごとの OR 演算子と組み合わせることも)。 一度にすべてのエラー、警告、およびトレースのログを有効にするには設定**デバッグ フラグ**0x0000007 にします。

値の変更の順序で**デバッグ フラグ**WIA サービスを有効にする (*stisvc*) 停止し、再起動する必要があります。 参照してください[の開始と停止もイメージ サービス](starting-and-stopping-the-still-image-service.md)詳細についてはします。

**注**  過度のログ記録がパフォーマンスが大幅に低下する可能性があります。 特定の問題の解決を試みたときにのみ、ログ記録レベルを増やす必要があります。 この問題を修正した後は、元のレベルにログ記録を設定します。 既定のログ レベルは、1 つです。 クラッシュが発生する可能性がありますには、上記 3 つのログ記録レベルを増やさないでください。
