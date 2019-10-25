---
title: WIA ミニドライバーのトラブルシューティング
description: WIA ミニドライバーのトラブルシューティング
ms.assetid: a0944bdd-56c4-4f7b-b542-eb353cd4d1f2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 37be79dce324cd0c7ce96f54c2eec0b9c766763c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840674"
---
# <a name="wia-minidriver-troubleshooting"></a>WIA ミニドライバーのトラブルシューティング





既定では、WIA サービスは、 **%** <em>windir</em> **%** ディレクトリ内の*wiadebug .log*という名前のファイルにエラーを記録します。 WIA サービスがこのファイルに格納する情報は、ドライバーの開発時に非常に役立ちます。 次の例は、一般的な問題を示しています。また、 *wiadebug .log*ファイルの情報を使用して問題の解決策を見つける方法を示しています。

開発者は、開発中のスキャナードライバーをテストするアプリケーションを記述します。 テストの1つとして、開発者はスキャナーのドット/インチ (dpi) を1200に設定しようとしますが、この操作でエラーが発生することが通知されます。 Wiadebug .log ファイルには、次のような内容が表示されます。

```console
wiasGetChangedValueLong, validate prop 6147 failed hr: 0x80070057
wiasUpdateScanRect, CheckXResAndUpdate failed (0x80070057)
CDrvWrap::WIA_drvValidateItemProperties, Error calling driver:
drvValidateItemProperties with hr = 0x80070057 (This is normal if the app wrote an invalid value)
```

これらのログエントリは、アプリケーションによって無効な値が書き込まれたことがドライバーによって報告されていることを示しています。 この情報から明らかになるのは、このような問題ではありません。 開発者が、警告とエラーを報告するために WIA ログ記録レベルを上げると、次のような出力が生成さ*れ*ます。

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

出力には、水平方向の解像度プロパティが原因でエラーが発生していることが示されています。 アプリケーションが解像度を1200に設定しようとしていますが、サポートされている解像度の一覧に1200が含まれていません。 このため、WIA サービス検証ヘルパー [**wiasValidateItemProperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasvalidateitemproperties)は、この値を設定する要求を拒否します。

問題が特定されたので、開発者は、それがドライバーであるか、または変更する必要があるアプリケーションであるかを判断します。 スキャナーの仕様で100と 1400 dpi のすべての解像度をサポートできる場合、ドライバーは 1200 dpi の要求を処理できる必要があります。 スキャナーでこの設定がサポートされていない場合は、アプリケーションを変更して、水平方向の解像度がこのプロパティに対して無効な値に設定されないようにする必要があります。 この場合、アプリケーションは、プロパティをこの値に設定しようとする前に、値が有効であることを確認する必要があります。

ログ記録レベルは、レジストリのエントリによって制御されます。 WIA の場合、このキーは次の場所に存在します。

**HKLM\\System\\CurrentControlSet\\コントロール\\StillImage\\デバッグ\\** <em>モジュール\_名前</em> **\\debugflags**

この例では、MODULE\_NAME は、適切なバイナリモジュールの名前です。 WIA サービスの場合、これは*wiaservc*です。 **Debugflags**の値は、ログ記録レベルを制御します。 次の表に、3つの設定を示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Value</th>
<th>意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0x00000001</p></td>
<td><p>エラーメッセージを表示します。</p></td>
</tr>
<tr class="even">
<td><p>0x00000002</p></td>
<td><p>警告メッセージを表示します。</p></td>
</tr>
<tr class="odd">
<td><p>0x00000004</p></td>
<td><p>トレースメッセージを表示します。</p></td>
</tr>
</tbody>
</table>

**Debugflags**の値はフラグ値です (つまり、異なる設定をビットごとの or 演算子と組み合わせることができます)。 エラー、警告、およびトレースのログ記録をすべて一度に有効にするには、 **Debugflags**を0x0000007 に設定します。

**Debugflags**の値の変更を有効にするには、WIA サービス (*stisvc*) を停止してから再起動する必要があります。 詳細について[は、「イメージサービスの開始と停止](starting-and-stopping-the-still-image-service.md)」を参照してください。

ログが過剰**に   と**、パフォーマンスが大幅に低下する可能性があります。 特定の問題を解決しようとする場合にのみ、ログ記録レベルを上げる必要があります。 問題を修正したら、ログを元のレベルに設定します。 既定のログ記録レベルは1です。 このようなクラッシュが発生する可能性があるので、ログレベルを3より大きくしないでください。
