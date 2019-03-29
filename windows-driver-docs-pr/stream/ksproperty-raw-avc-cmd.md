---
title: KSPROPERTY\_RAW\_AVC\_CMD
description: KSPROPERTY\_RAW\_AVC\_CMD プロパティは、生の AV/C コマンドを発行します。 生の AV/C コマンドは、IEEE 1394 bus デバイスのみサポートされます。
ms.assetid: f3ff3815-0f4f-4fcb-89bd-e77d8002813c
keywords:
- KSPROPERTY_RAW_AVC_CMD ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_RAW_AVC_CMD
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c7c6226bb8d79c7a7aa2a861fb2b2a7d01d26d2
ms.sourcegitcommit: 56599ec634b3a731f2d13dff686be3b7b95390e4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2019
ms.locfileid: "58419572"
---
# <a name="kspropertyrawavccmd"></a>KSPROPERTY\_RAW\_AVC\_CMD

KSPROPERTY\_RAW\_AVC\_CMD プロパティは、生の AV/C コマンドを発行します。 生の AV/C コマンドは、IEEE 1394 bus デバイスのみサポートされます。

## <a name="usage-summary-table"></a>使用状況の概要テーブル

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th>取得</th>
<th>Set</th>
<th>移行先</th>
<th>プロパティ記述子の型</th>
<th>プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>はい</p></td>
<td><p>はい</p></td>
<td><p>デバイス</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565167" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTXPORT_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565167)"><strong>KSPROPERTY_EXTXPORT_S</strong></a></p></td>
<td><p>埋め込み<strong>RawAVC</strong>構造体</p></td>
</tr>
</tbody>
</table>

プロパティの値 (データの操作) は、埋め込まれた**RawAVC** 、KSPROPERTY のメンバー\_EXTXPORT\_を実行する生の AV/C コマンドを記述する S 構造体。

## <a name="remarks"></a>コメント

このプロパティは、AV/C コマンドをサポートできるデバイスでのみ使用できます、 [ **KSPROPERTY\_EXTDEVICE\_ポート**](ksproperty-extdevice-port.md)偏差を返します\_ポート\_で 1394、 **DevPort**のメンバー、 [ **KSPROPERTY\_EXTDEVICE\_S** ](https://msdn.microsoft.com/library/windows/hardware/ff565156)構造体。

IEEE 1394 デバイス ドライバーの開発者は、デバイスの標準のインターフェイスでサポートされていないトランスポート コントロールを拡張するにはドライバーにこのプロパティを必要に応じてサポート可能性が (ユーザー モードなど**IAMExtTransport** COMインターフェイス メソッド**配置\_モード**と**取得\_モード**)。

に、USB デバイスでこのプロパティのサポートを実装する必要はありません、 [USB ビデオ クラス ドライバー](https://msdn.microsoft.com/library/windows/hardware/ff568649)この機能を提供します。 通常のアプリケーションを使用できる、 **IKsControl** IEEE 1394 デバイスを制御する COM インターフェイスです。 ただし、 **IKsControl** COM インターフェイスは、標準を提供していない USB および IEEE 1394 のバスの間で移植性がテープをサポートするメソッドがシークします。 そのため、実行するテープ シーク、呼び出し元を使用する必要があります、 **DeviceIoControl**関数の代わりに、 **IKsControl** COM インターフェイスです。 呼び出し元のテープを実行するシーク 1394 の絶対パスを生の AV/C コマンドを使用してデバイスを AV/C (ATN) の数を追跡または時刻をシークするコードです。 これは、USB デバイスにこのプロパティを適用しない原因の主な理由です。

参照してください、[デジタル ビデオ アプリケーションの互換性](https://go.microsoft.com/fwlink/?linkid=2085071)USB 上のテープの場所の検索と 1394 デバイス間の違いの詳細については、ホワイト ペーパー。

## <a name="requirements"></a>必要条件

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Ksmedia.h (Ksmedia.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目

[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

[**KSPROPERTY\_EXTXPORT\_S**](https://msdn.microsoft.com/library/windows/hardware/ff565167)
