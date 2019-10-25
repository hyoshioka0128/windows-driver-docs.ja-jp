---
title: WSK_TDI_BEHAVIOR
description: WSK_TDI_BEHAVIOR
ms.assetid: 84e4c8c3-2c31-4db5-bb25-309c6bb176ff
ms.date: 07/18/2017
keywords:
- WSK_TDI_BEHAVIOR ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: 3c18ae7179a59379c3e1e04a20682c392a67f438
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844423"
---
# <a name="wsk_tdi_behavior"></a>WSK\_TDI\_の動作


TDI 機能は非推奨とされて**いる  、** 今後のバージョンの Microsoft Windows では削除される予定です。

 

Wsk アプリケーションは、wsk\_TDI\_BEHAVIOR クライアントコントロール操作を使用して、WSK サブシステムがネットワーク i/o を[tdi](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565094(v=vs.85))トランスポートに転送するかどうかを制御します。 WSK アプリケーションは、WSK サブシステムの既定の動作をオーバーライドする必要がある場合にのみ、このクライアントコントロール操作を使用します。

WSK アプリケーションが WSK\_TDI\_BEHAVIOR クライアントコントロール操作を使用する場合は、ソケットを作成する前にその操作を行う必要があります。

WSK サブシステムがネットワーク i/o を TDI トランスポートに転送するかどうかを制御するために、WSK アプリケーションは次のパラメーターを使用して[**Wskcontrolclient**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_client)関数を呼び出します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>パラメーター</th>
<th>Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>ControlCode</em></p></td>
<td><p>WSK_TDI_BEHAVIOR</p></td>
</tr>
<tr class="even">
<td><p><em>InputSize</em></p></td>
<td><p>sizeof (ULONG)</p></td>
</tr>
<tr class="odd">
<td><p><em>InputBuffer</em></p></td>
<td><p>WSK サブシステムの動作を制御するフラグを格納する、ULONG 型の変数へのポインター。</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSize</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="odd">
<td><p><em>OutputBuffer</em></p></td>
<td><p><strong>空白</strong></p></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p><strong>空白</strong></p></td>
</tr>
<tr class="odd">
<td><p><em>Irp</em></p></td>
<td><p><strong>空白</strong></p></td>
</tr>
</tbody>
</table>

WSK\_TDI\_BEHAVIOR クライアントコントロール操作には、次のフラグが定義されています。

<a href="" id="wsk-tdi-behavior-bypass-tdi"></a>WSK\_TDI\_動作\_バイパス\_TDI  
WSK アプリケーションでソケットが作成されるときに指定されたアドレスファミリ、ソケットの種類、およびプロトコルに対してネイティブ WSK トランスポートが存在する場合、WSK サブシステムはすべての TDI フィルタードライバーを無視し、常にネイティブ WSK トランスポートを使用します。

既定の動作では、WSK アプリケーションで新しいソケットが作成されたときに指定されたアドレスファミリ、ソケットの種類、およびプロトコルに対して TDI フィルタードライバーが検出されると、WSK サブシステムによって、新しいソケットのネットワーク i/o が TDI トランスポートに振り向けされます。ネットワークトラフィックとその他のソケット操作は、TDI フィルタードライバーを通過します。

このクライアントコントロール操作では、 *Irp*パラメーターは**NULL**である必要があります。

Windows Vista 以降では、Microsoft Windows のバージョンでは TDI はサポートされていない**ことに注意**してください  。

 

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>Windows Vista 以降のバージョンの Windows オペレーティングシステムで使用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wsk .h (Wsk .h を含む)</td>
</tr>
</tbody>
</table>

 

 




