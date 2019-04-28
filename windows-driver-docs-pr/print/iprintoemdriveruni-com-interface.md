---
title: IPrintOemDriverUni COM インターフェイス
description: IPrintOemDriverUni COM インターフェイス
ms.assetid: 84b3f43c-039a-4e9d-b596-41c08f1e0284
keywords:
- IPrintOemDriverUni
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5bd00f455a74a3a42702be5366cabcaf3aca5e4a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366345"
---
# <a name="iprintoemdriveruni-com-interface"></a>IPrintOemDriverUni COM インターフェイス





`IPrintOemDriverUni COM`インターフェイスには、レンダリング Unidrv のプリンター グラフィックス DLL によって提供されるユーティリティ操作へのアクセス権を持つプラグインが用意されています。 これらの操作では、印刷スプーラーにデータ ストリームを送信し、ドライバー管理の情報を取得します。

次の表とによって定義されたメソッドのすべてについて説明します、 **IPrintOemDriverUni**インターフェイス。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>メソッド</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553126" data-raw-source="[&lt;strong&gt;IPrintOemDriverUni::DrvGetDriverSetting&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553126)"><strong>IPrintOemDriverUni::DrvGetDriverSetting</strong></a></p></td>
<td><p>プリンターの機能とその他の内部情報の現在の状態を返します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553128" data-raw-source="[&lt;strong&gt;IPrintOemDriverUni::DrvGetGPDData&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553128)"><strong>IPrintOemDriverUni::DrvGetGPDData</strong></a></p></td>
<td><p>プリンターので定義されているデータを取得するプラグインをレンダリングできるように<a href="https://msdn.microsoft.com/library/windows/hardware/ff556283#wdkgloss-generic-printer-description--gpd-" data-raw-source="&lt;em&gt;generic printer description (GPD)&lt;/em&gt;"><em>ジェネリック プリンターの説明 (GPD)</em> </a>ファイル。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553129" data-raw-source="[&lt;strong&gt;IPrintOemDriverUni::DrvGetStandardVariable&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553129)"><strong>IPrintOemDriverUni::DrvGetStandardVariable</strong></a></p></td>
<td><p>により、レンダリングの Unidrv の現在の値を取得するプラグインを<a href="standard-variables.md" data-raw-source="[standard variables](standard-variables.md)">標準変数</a>します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553132" data-raw-source="[&lt;strong&gt;IPrintOemDriverUni::DrvUniTextOut&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553132)"><strong>IPrintOemDriverUni::DrvUniTextOut</strong></a></p></td>
<td><p>デバイス管理の描画サーフェイスを使用して簡単にテキスト文字列を出力するプラグインのレンダリングを有効にします。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553135" data-raw-source="[&lt;strong&gt;IPrintOemDriverUni::DrvWriteAbortBuf&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553135)"><strong>IPrintOemDriverUni::DrvWriteAbortBuf</strong></a></p></td>
<td><p>ユーザーが印刷ジョブを終了した後、プリンターをリセットするプラグインのレンダリングを有効にします。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553138" data-raw-source="[&lt;strong&gt;IPrintOemDriverUni::DrvWriteSpoolBuf&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553138)"><strong>IPrintOemDriverUni::DrvWriteSpoolBuf</strong></a></p></td>
<td><p>プリンター データをスプーラーに送信します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553141" data-raw-source="[&lt;strong&gt;IPrintOemDriverUni::DrvXMoveTo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553141)"><strong>IPrintOemDriverUni::DrvXMoveTo</strong></a></p></td>
<td><p>カーソルの x 位置の変更の Unidrv に通知します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553144" data-raw-source="[&lt;strong&gt;IPrintOemDriverUni::DrvYMoveTo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553144)"><strong>IPrintOemDriverUni::DrvYMoveTo</strong></a></p></td>
<td><p>カーソルの y 位置の変更の Unidrv に通知します。</p></td>
</tr>
</tbody>
</table>

 

詳細については、次を参照してください。[プリンター ドライバーの COM インターフェイスを実装する](implementing-printer-driver-com-interfaces.md)します。

 

 




