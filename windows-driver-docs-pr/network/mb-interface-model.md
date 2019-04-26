---
title: MB インターフェイス モデル
description: このセクションでは、モバイル ブロード バンド インターフェイス モデル (MBIM) 仕様に基づいて実装されているモバイル ブロード バンド デバイスの情報を提供します。
ms.assetid: B1C6D5F4-63E2-4C46-8038-71B8144AB474
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 907eb83a0ddc9b27a179000e745bce9b4a19b0e8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343402"
---
# <a name="mb-interface-model"></a>MB インターフェイス モデル


このセクションでは、モバイル ブロード バンド インターフェイス モデル (MBIM) 仕様に基づいて実装されているモバイル ブロード バンド デバイスの情報を提供します。

Windows 8 以降、Microsoft は、MBIM 関数 MBCD と呼ばれる、インボックス クラス ドライバーを提供します。 Microsoft では、複合デバイス用インボックス ドライバー、USBCCGP、既に用意されています。 このセクションでは、USBCCGP および Windows 8 で MBCD の読み込みにモバイル ブロード バンド デバイスの要件について説明します。

関数にグループ化のインターフェイスの WMC UFD を使用して、モバイル ブロード バンドの複合デバイスには、Microsoft OS ディスクリプターを Windows 8 の USBCCGP を読み込み、USBCCGP 関数を作成する WMC UFD を解析するよう指示を実装する必要があります。 関数にグループ化のインターフェイスのインターフェイスの関連付け記述子 (Iad) を使用して、モバイル ブロード バンドの複合デバイスは、Microsoft OS ディスクリプターを読み込む USBCCGP を実装する必要はありません。

旧バージョンと互換性のある MBIM 関数は、Microsoft OS ディスクリプターを MBCD を読み込むを実装する必要があります。 旧バージョンと互換性がありません MBIM 関数は、Microsoft OS ディスクリプターを読み込む MBCD を実装する必要はありません。

モバイル ブロード バンド デバイス id モーフィングを示すには、Microsoft OS ディスクリプターも実装する必要があります。

MB インターフェイス モデルのトピックについて詳細には、これらのシナリオについて説明します。 次の表は、これらのサブトピックに記載されている Microsoft OS 互換性 Id のすべてをまとめたものです。 詳細については、次を参照してください。 [Microsoft OS ディスクリプター](https://go.microsoft.com/fwlink/p/?linkid=308932)します。

*Microsoft OS 互換性 Id*

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Microsoft OS 互換性のある ID</th>
<th align="left">Microsoft OS Sub 互換性 ID</th>
<th align="left">シナリオに必要な</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>"CDC_WMC"</p></td>
<td align="left"><p></p></td>
<td align="left"><p>関数へのインターフェイスをグループ化するため WMC UFD を使用する複合デバイスで USBCCGP の読み込み</p></td>
</tr>
<tr class="even">
<td align="left"><p>"MBIM"</p></td>
<td align="left"><p></p></td>
<td align="left"><p>MBIM 下位互換性のある関数で MBCD の読み込み</p></td>
</tr>
<tr class="odd">
<td align="left"><p>"ALTRCFG"</p></td>
<td align="left"><p>ASCII で構成数</p></td>
<td align="left"><p>Identity で Iad モーフィング</p></td>
</tr>
<tr class="even">
<td align="left"><p>"WMCALTR"</p></td>
<td align="left"><p>ASCII で構成数</p></td>
<td align="left"><p>WMC UFD をモーフィングの id</p></td>
</tr>
</tbody>
</table>

 

MB インターフェイス モデルで次のサブトピックで詳しく説明します。

[MB インターフェイス条項](mb-interface-terms.md)
[MB の統合機能ディスクリプター](mb-union-function-descriptors.md)
[MB Id モーフィング](mb-identity-morphing.md)
[MB インターフェイス モデルの追加条項](mb-interface-model-supplement.md)
 

 





