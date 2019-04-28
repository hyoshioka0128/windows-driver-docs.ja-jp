---
title: GDI ユーティリティ サービス
description: GDI ユーティリティ サービス
ms.assetid: 4ceec90d-5be2-4b79-87b3-1fdb6b0aea6b
keywords:
- GDI WDK Windows 2000 の表示、ユーティリティ サービス
- グラフィックス ドライバー WDK Windows 2000 の表示、ユーティリティ サービス
- 描画 WDK GDI、ユーティリティ サービス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a27e105c9544f9692427e654c7b2ddd73e53507c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374610"
---
# <a name="gdi-utility-services"></a>GDI ユーティリティ サービス


## <span id="ddk_gdi_utility_services_gg"></span><span id="DDK_GDI_UTILITY_SERVICES_GG"></span>


次の表は、その他の GDI ユーティリティ サービスを一覧表示します。 いくつかの変換サービスの 1 つの文字を別の種類に、並べ替えルーチン、およびその他のエンコーディングからその変換、デバッグのサポートを取得、および最後のエラーの設定にこれらのサービスが含まれます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">関数</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564187" data-raw-source="[&lt;strong&gt;EngBugCheckEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564187)"><strong>EngBugCheckEx</strong></a></p></td>
<td align="left"><p>呼び出し元が回復不能な不整合を検出した場合、制御された方法でシステムが表示されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564773" data-raw-source="[&lt;strong&gt;EngDebugBreak&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564773)"><strong>EngDebugBreak</strong></a></p></td>
<td align="left"><p>発生する現在のプロセスでは、ブレークポイントを発生させます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564779" data-raw-source="[&lt;strong&gt;EngDebugPrint&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564779)"><strong>EngDebugPrint</strong></a></p></td>
<td align="left"><p>カーネル デバッガーに指定されたデバッグ メッセージを出力します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564940" data-raw-source="[&lt;strong&gt;EngGetLastError&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564940)"><strong>EngGetLastError</strong></a></p></td>
<td align="left"><p>呼び出し元のスレッドの GDI によって記録された最後のエラー コードを返します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564958" data-raw-source="[&lt;strong&gt;EngHangNotification&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564958)"><strong>EngHangNotification</strong></a></p></td>
<td align="left"><p>指定したデバイスが動作不能になったり応答しなくであるシステムに通知します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564969" data-raw-source="[&lt;strong&gt;EngLpkInstalled&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564969)"><strong>EngLpkInstalled</strong></a></p></td>
<td align="left"><p>システムの言語パックがインストールされているかどうかを判断します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564978" data-raw-source="[&lt;strong&gt;EngMulDiv&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564978)"><strong>EngMulDiv</strong></a></p></td>
<td align="left"><p>2 つの 32 ビット値を乗算し、64 ビットの結果を 3 番目の 32 ビット値で除算します。 戻り値は、上または最も近い整数に丸められます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564979" data-raw-source="[&lt;strong&gt;EngMultiByteToUnicodeN&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564979)"><strong>EngMultiByteToUnicodeN</strong></a></p></td>
<td align="left"><p>指定された ANSI ソース文字列を現在の ANSI コード ページを使用して Unicode 文字列に変換します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564980" data-raw-source="[&lt;strong&gt;EngMultiByteToWideChar&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564980)"><strong>EngMultiByteToWideChar</strong></a></p></td>
<td align="left"><p>ソースの ANSI 文字列を指定したコード ページを使用してワイド文字の文字列に変換します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564983" data-raw-source="[&lt;strong&gt;EngProbeForRead&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564983)"><strong>EngProbeForRead</strong></a></p></td>
<td align="left"><p>読み取りのアクセシビリティの構造体をプローブします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564984" data-raw-source="[&lt;strong&gt;EngProbeForReadAndWrite&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564984)"><strong>EngProbeForReadAndWrite</strong></a></p></td>
<td align="left"><p>プローブの構造は、アクセシビリティを読み書きします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565015" data-raw-source="[&lt;strong&gt;EngSetLastError&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565015)"><strong>EngSetLastError</strong></a></p></td>
<td align="left"><p>エラー コードは、アプリケーションを取得できるを報告する GDI をによりします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565022" data-raw-source="[&lt;strong&gt;EngSort&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565022)"><strong>EngSort</strong></a></p></td>
<td align="left"><p>指定したリストに対してクイック ソートを実行します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565038" data-raw-source="[&lt;strong&gt;EngUnicodeToMultiByteN&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565038)"><strong>EngUnicodeToMultiByteN</strong></a></p></td>
<td align="left"><p>指定した Unicode 文字列を現在の ANSI コード ページを使用して ANSI 文字列に変換します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565466" data-raw-source="[&lt;strong&gt;EngWideCharToMultiByte&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565466)"><strong>EngWideCharToMultiByte</strong></a></p></td>
<td align="left"><p>ワイド文字の文字列を指定したコード ページを使用して、ANSI ソース文字列に変換します。</p></td>
</tr>
</tbody>
</table>

 

 

 





