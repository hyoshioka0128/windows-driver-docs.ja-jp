---
title: MB インターフェイス モデルの概要
description: ここでは、モバイルブロードバンドインターフェイスモデル (MBIM) 仕様に基づいて実装されているモバイルブロードバンドデバイスについて説明します。
ms.assetid: B1C6D5F4-63E2-4C46-8038-71B8144AB474
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: abfa4ee22a47361168ff3822cef2ee662838b6bf
ms.sourcegitcommit: 238308264c1ee2c74ec0c8c303258dc00c79b902
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/28/2019
ms.locfileid: "70063912"
---
# <a name="mb-interface-model-overview"></a>MB インターフェイス モデルの概要


ここでは、モバイルブロードバンドインターフェイスモデル (MBIM) 仕様に基づいて実装されているモバイルブロードバンドデバイスについて説明します。

Windows 8 以降では、MBIM 関数のために、Microsoft が MBCD と呼ばれる受信トレイクラスドライバーを提供しています。 Microsoft では、複合デバイス用の受信トレイドライバー USBCCGP を既に提供しています。 このセクションでは、Windows 8 で USBCCGP と MBCD を読み込むためのモバイルブロードバンドデバイスの要件について説明します。

インターフェイスを関数にグループ化するために WMC UFD を使用するモバイルブロードバンド複合デバイスは、Microsoft OS 記述子を実装して Windows 8 で USBCCGP を読み込み、WMC UFD を解析して関数を作成するよう USBCCGP に指示する必要があります。 インターフェイスを関数にグループ化するためにインターフェイスの関連付け記述子 (IADs) を使用するモバイルブロードバンド複合デバイスでは、USBCCGP を読み込むために Microsoft OS 記述子を実装する必要はありません。

旧バージョンとの互換性がある MBIM 関数では、MBCD を読み込むために Microsoft OS 記述子を実装する必要があります。 旧バージョンとの互換性がない MBIM 関数では、MBCD を読み込むために Microsoft OS 記述子を実装する必要はありません。

Id のモーフィングを示すモバイルブロードバンドデバイスでは、Microsoft OS 記述子も実装する必要があります。

これらのシナリオの詳細については、「MB インターフェイスモデル」のトピックを参照してください。 次の表は、これらのサブトピックに記載されている Microsoft OS と互換性のあるすべての Id をまとめたものです。 詳細については、「 [MICROSOFT OS 記述子](https://go.microsoft.com/fwlink/p/?linkid=308932)」を参照してください。

*Microsoft OS 互換 Id*

<table>  
<colgroup> <col width="33%" /> <col width="33%" /> <col width="33%" /> </colgroup>  
<thead>  
<tr class="header">  
<th align="left">Microsoft OS 互換 ID</th>
<th align="left">Microsoft OS の下位互換性 ID</th>
<th align="left">シナリオに必要</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>"CDC_WMC"</p></td>
<td align="left"><p></p></td>
<td align="left"><p>インターフェイスを関数にグループ化するために WMC UFD を使用する複合デバイスに USBCCGP を読み込んでいます</p></td>
</tr>
<tr class="even">
<td align="left"><p>MBIM</p></td>
<td align="left"><p></p></td>
<td align="left"><p>MBIM の旧バージョンと互換性がある関数に MBCD を読み込んでいます</p></td>
</tr>
<tr class="odd">
<td align="left"><p>"ALTRCFG"</p></td>
<td align="left"><p>ASCII の構成番号</p></td>
<td align="left"><p>IADs での id のモーフィング</p></td>
</tr>
<tr class="even">
<td align="left"><p>"WMCALTR"</p></td>
<td align="left"><p>ASCII の構成番号</p></td>
<td align="left"><p>WMC UFD による id のモーフィング</p></td>
</tr>
</tbody>
</table>

 

次のサブトピックで詳細に説明されている、MB のインターフェイスモデル。

[Mb インターフェイス使用条件](mb-interface-terms.md)
[mb 共用体関数記述子](mb-union-function-descriptors.md)
[mb id モーフィング](mb-identity-morphing.md)
[mb インターフェイスモデル補助](mb-interface-model-supplement.md)
 

 





