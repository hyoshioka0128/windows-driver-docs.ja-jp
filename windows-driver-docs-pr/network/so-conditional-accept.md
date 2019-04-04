---
title: SO_CONDITIONAL_ACCEPT
description: SO_CONDITIONAL_ACCEPT
ms.assetid: 8aaaa08b-b239-4648-8c4f-8db2efbda551
ms.date: 08/08/2017
keywords: -SO_CONDITIONAL_ACCEPT ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: ce45eb619d33c7feae23cf24c6f6b337bbd52bba
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527526"
---
# <a name="soconditionalaccept"></a>したがって\_条件付き\_ACCEPT


SO の状態\_条件付き\_ACCEPT ソケット オプションは、リスナ ソケットで条件付きの受け入れモードが有効になっているかどうかを決定します。 このソケット オプションは、リッスン ソケットだけに適用されます。

WSK アプリケーションでは、このソケット オプションを設定する場合、ローカル トランスポート アドレスをリッスンしているソケットがバインドされる前に、実行する必要があります。

WSK アプリケーションを呼び出すこのソケット オプションの状態を設定する、 [ **WskControlSocket** ](https://msdn.microsoft.com/library/windows/hardware/ff571127)関数は次のパラメーター。

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
<td><p><em>RequestType</em></p></td>
<td><p><strong>WskSetOption</strong></p></td>
</tr>
<tr class="even">
<td><p><em>ControlCode</em></p></td>
<td><p>SO_CONDITIONAL_ACCEPT</p></td>
</tr>
<tr class="odd">
<td><p><em>レベル</em></p></td>
<td><p>取得</p></td>
</tr>
<tr class="even">
<td><p><em>InputSize</em></p></td>
<td><p>sizeof(ULONG)</p></td>
</tr>
<tr class="odd">
<td><p><em>InputBuffer</em></p></td>
<td><p>新しいソケット オプションの状態の値を含む ULONG に型指定された変数へのポインター。</p>
<p>0:受け入れモードを無効にする条件付き</p>
<p>1:受け入れモードを有効にする条件付き</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSize</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="odd">
<td><p><em>OutputBuffer</em></p></td>
<td><p>NULL</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p>NULL</p></td>
</tr>
</tbody>
</table>


このソケット オプションの状態を取得するには、WSK アプリケーションが呼び出す、 **WskControlSocket**関数は次のパラメーター。

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
<td><p><em>RequestType</em></p></td>
<td><p><strong>WskGetOption</strong></p></td>
</tr>
<tr class="even">
<td><p><em>ControlCode</em></p></td>
<td><p>SO_CONDITIONAL_ACCEPT</p></td>
</tr>
<tr class="odd">
<td><p><em>レベル</em></p></td>
<td><p>取得</p></td>
</tr>
<tr class="even">
<td><p><em>InputSize</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="odd">
<td><p><em>InputBuffer</em></p></td>
<td><p>NULL</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSize</em></p></td>
<td><p>sizeof(ULONG)</p></td>
</tr>
<tr class="odd">
<td><p><em>OutputBuffer</em></p></td>
<td><p>ソケット オプションの状態の値を受信する ULONG に型指定された変数へのポインター。</p>
<p>0:モードが無効になっている条件に同意します。</p>
<p>1:モードが有効になっている条件に同意します。</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p>NULL</p></td>
</tr>
</tbody>
</table>



呼び出すときに、WSK アプリケーションは IRP へのポインターを指定する必要があります、 **WskControlSocket**などの状態を取得または設定する関数\_条件付き\_ACCEPT ソケット オプション。

このソケット オプションの既定の状態は、その条件に同意モードが無効になっています。

一部のトランスポート プロトコル サポート条件ではありませんがリスニング ソケットでモードを受け付ける場合があります。

条件付きで着信接続の受け入れの詳細については、[リッスン中の接続と着信接続を受け入れる](https://msdn.microsoft.com/library/windows/hardware/ff557059)を参照してください。

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
<td><p>Windows Vista および Windows オペレーティング システムの以降のバージョンで使用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ws2def.h (Wsk.h を含む)</td>
</tr>
</tbody>
</table>

 

 




