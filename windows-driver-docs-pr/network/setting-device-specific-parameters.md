---
title: デバイス固有パラメーターの設定
description: デバイス固有パラメーターの設定
ms.assetid: 5df72c11-e8d4-4e06-8f34-c9b85ad779f6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4cd4cf05812dfa5ed694cc6a58c5b2c404f24a73
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346659"
---
# <a name="setting-device-specific-parameters"></a>デバイス固有パラメーターの設定





ほとんどのデバイスのリモートの NDIS はホスト上のパラメーターの構成をしなくても機能することが必要です。 ただし、ホスト上のいくつかの構成が適切なネットワークの操作に必要な場合があります。 デバイスで構成可能なパラメーターは、サポートするかどうかは、それに対するクエリへの応答でのレポートがサポートされている Oid の一覧で、次の省略可能な OID を含める必要があります[OID\_GEN\_サポートされている\_一覧](https://msdn.microsoft.com/library/windows/hardware/ff569642):

```C++
#define OID_GEN_RNDIS_CONFIG_PARAMETER 0x0001021B
```

デバイスがサポートしている場合、 [OID\_GEN\_RNDIS\_CONFIG\_パラメーター](https://msdn.microsoft.com/library/windows/hardware/ff569639) OID、ホストが使用して、デバイスが初期化状態に入るとすぐに、デバイス固有のパラメーターを設定するには初期化されていない状態からリモートの NDIS。 0 個以上のリモート送信ホスト\_NDIS\_設定\_OID と、デバイスにメッセージ\_GEN\_RNDIS\_CONFIG\_パラメーターを設定する OID 値として。 これらの各[**リモート\_NDIS\_設定\_MSG** ](https://msdn.microsoft.com/library/windows/hardware/ff570654)ホストに構成されている 1 つのデバイスに固有のパラメーターに対応します。

*InformationBuffer*に関連付けられたこれらの各[**リモート\_NDIS\_設定\_MSG** ](https://msdn.microsoft.com/library/windows/hardware/ff570654)形式は、次のとおりです。 情報バッファーの先頭の相対オフセット値に注意してください。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Offset</th>
<th align="left">サイズ</th>
<th align="left">フィールド</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>4</p></td>
<td align="left"><p>ParameterNameOffset</p></td>
<td align="left"><p>パラメーター名を表す Unicode 文字の文字列がある ParameterNameOffset フィールドの先頭からのオフセットをバイトを指定します。 文字列では、終端の NULL は含まれません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>4</p></td>
<td align="left"><p>ParameterNameLength</p></td>
<td align="left"><p>パラメーター名の文字列のバイトの長さを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>8</p></td>
<td align="left"><p>4</p></td>
<td align="left"><p>ParameterType</p></td>
<td align="left"><p>パラメーター値のデータ型を指定します。 これは、次のいずれかです。0 - 数値を指定します。2-文字列値です。</p></td>
</tr>
<tr class="even">
<td align="left"><p>12</p></td>
<td align="left"><p>4</p></td>
<td align="left"><p>ParameterValueOffset</p></td>
<td align="left"><p>パラメーターの値がある ParameterNameOffset フィールドの先頭からのオフセットをバイトを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>16</p></td>
<td align="left"><p>4</p></td>
<td align="left"><p>ParameterValueLength</p></td>
<td align="left"><p>パラメーター値のバイトの長さを指定します。</p></td>
</tr>
</tbody>
</table>

 

デバイスから送信する[**リモート\_NDIS\_設定\_CMPLT** ](https://msdn.microsoft.com/library/windows/hardware/ff570651)それぞれへの応答で[**リモート\_NDIS\_設定\_MSG**](https://msdn.microsoft.com/library/windows/hardware/ff570654)パラメーターの値を適用した後。 RNDIS のステータスを返す、パラメーターの設定が許容される場合は、\_状態\_応答に成功します。 かどうか、パラメーターの設定は受け入れられずと、デバイスは、このパラメーターの既定値を適用できませんし、デバイスが適切なエラーの状態値を返します (状態の値のセクションを参照してください)。 エラー状態が返された場合、ホストの間でデバイスの停止のプロセスが開始されます。

デバイス固有のパラメーターは、Windows レジストリで構成する必要があります。 通常、パラメーター値を定義するキーはデバイスのインストールの処理中に、レジストリに作成されます。 キー、型情報、既定値、および有効な値の省略可能な範囲の一覧は、デバイスの INF ファイルで指定されます。 INF を使用してネットワーク デバイスのレジストリで構成パラメーターを設定する方法の詳細については、Windows 2000 Driver Development Kit (DDK) を参照してください。

 

 





