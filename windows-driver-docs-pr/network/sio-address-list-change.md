---
title: SIO_ADDRESS_LIST_CHANGE
description: SIO_ADDRESS_LIST_CHANGE
ms.assetid: d451208d-c850-4f2f-9ee0-d34139454ed4
ms.date: 08/08/2017
keywords: -SIO_ADDRESS_LIST_CHANGE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: bfb3f9f96087e2cf76f0df1ff01fc8db178f0d81
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535502"
---
# <a name="sioaddresslistchange"></a>SIO\_アドレス\_一覧\_変更


SIO\_アドレス\_一覧\_変更ソケット I/O 制御操作は、ソケットのアドレス ファミリ用のローカル トランスポート アドレスの一覧への変更があったときに、WSK アプリケーションに通知します。 このソケット I/O 制御操作は、すべての種類のソケットに適用されます。

ソケットのアドレス ファミリ用のローカル トランスポート アドレスの一覧への変更があったときの通知、WSK アプリケーションが呼び出す、 [ **WskControlSocket** ](https://msdn.microsoft.com/library/windows/hardware/ff571127)関数は次のパラメーター。

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
<td><p><strong>WskIoctl</strong></p></td>
</tr>
<tr class="even">
<td><p><em>ControlCode</em></p></td>
<td><p>SIO_ADDRESS_LIST_CHANGE</p></td>
</tr>
<tr class="odd">
<td><p><em>レベル</em></p></td>
<td><p>0</p></td>
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

呼び出すときに、WSK アプリケーションは IRP へのポインターを指定する必要があります、 **WskControlSocket**ソケットのアドレス ファミリ用のローカル トランスポート アドレスの一覧への変更の通知を受け取る関数。 WSK サブシステム IRP のキューおよび状態を返します\_保留します。 ソケットのアドレス ファミリ用のローカル トランスポート アドレスの一覧に変更が行われた場合、WSK サブシステムは IRP を完了します。 IRP の完了ルーチンを呼び出すと、WSK アプリケーションで使用できます、 [ **SIO\_アドレス\_一覧\_クエリ**](sio-address-list-query.md)ソケット、新しいクエリを実行する I/O 制御操作ソケットのアドレス ファミリ用のローカル トランスポート アドレスのリスト。

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

 

 




