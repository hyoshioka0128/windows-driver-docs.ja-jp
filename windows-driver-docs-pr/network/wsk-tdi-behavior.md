---
title: WSK_TDI_BEHAVIOR
description: WSK_TDI_BEHAVIOR
ms.assetid: 84e4c8c3-2c31-4db5-bb25-309c6bb176ff
ms.date: 07/18/2017
keywords:
- WSK_TDI_BEHAVIOR ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 6321bd798bdec847caaefa8a4dddc517cf5e645a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578625"
---
# <a name="wsktdibehavior"></a>WSK\_TDI\_動作


**注**   TDI 機能は非推奨し、Microsoft Windows の将来のバージョンでは削除されます。

 

WSK アプリケーションの使用、WSK\_TDI\_WSK サブシステムがネットワーク I/O を転送するかどうか、クライアントの動作が制御する操作を制御[TDI](https://msdn.microsoft.com/library/windows/hardware/ff565094)トランスポート。 WSK アプリケーションは、WSK サブシステムの既定の動作をオーバーライドする必要がある場合にのみ、このクライアントの管理操作を使用します。

WSK アプリケーション、WSK を使用している場合\_TDI\_クライアント コントロールの操作の動作が行う必要があります、ソケットを作成する前にします。

WSK アプリケーションが呼び出す WSK サブシステムが TDI トランスポートにネットワーク I/O を転送するかどうかを制御するため、 [ **WskControlClient** ](https://msdn.microsoft.com/library/windows/hardware/ff571126)関数は次のパラメーター。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>パラメーター</th>
<th>値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>ControlCode</em></p></td>
<td><p>WSK_TDI_BEHAVIOR</p></td>
</tr>
<tr class="even">
<td><p><em>InputSize</em></p></td>
<td><p>sizeof(ULONG)</p></td>
</tr>
<tr class="odd">
<td><p><em>InputBuffer</em></p></td>
<td><p>ULONG へのポインターは、WSK サブシステムの動作を制御するフラグを含む変数を入力します。</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSize</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="odd">
<td><p><em>OutputBuffer</em></p></td>
<td><p><strong>NULL</strong></p></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p><strong>NULL</strong></p></td>
</tr>
<tr class="odd">
<td><p><em>Irp</em></p></td>
<td><p><strong>NULL</strong></p></td>
</tr>
</tbody>
</table>

次のフラグは、WSK に対して定義されて\_TDI\_クライアント管理操作の動作。

<a href="" id="wsk-tdi-behavior-bypass-tdi"></a>WSK\_TDI\_動作\_バイパス\_TDI  
アドレス ファミリ、ソケットの種類、および WSK アプリケーションは、ソケットを作成するときに指定されているプロトコルのネイティブ WSK トランスポートが存在する場合このフラグが設定されている場合、WSK サブシステム、TDI フィルター ドライバーを無視し、常にネイティブ WSK トランスポートを使用します。

既定の動作は、アドレス ファミリ、ソケットの種類、および WSK アプリケーションは、新しいソケットを作成するときに指定されているプロトコルに TDI フィルター ドライバーが検出された場合、WSK サブシステム浪費ネットワーク I/O の新しいソケット TDI トランスポートにこれをネットワーク トラフィックとその他のソケット操作は、TDI フィルター ドライバーを通過します。

*Irp*パラメーターである必要があります**NULL**このクライアントのコントロールの操作。

**注**  TDI は Windows Vista の後に Microsoft Windows のバージョンでサポートされていません。

 

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>Windows Vista および Windows オペレーティング システムの以降のバージョンで使用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wsk.h (Wsk.h を含む)</td>
</tr>
</tbody>
</table>

 

 




