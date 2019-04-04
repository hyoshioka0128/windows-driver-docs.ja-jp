---
title: SIO_WSK_REGISTER_EXTENSION
description: SIO_WSK_REGISTER_EXTENSION
ms.assetid: e7fd6d68-85e8-4c5f-b67f-2193d200130d
ms.date: 07/18/2017
keywords:
- SIO_WSK_REGISTER_EXTENSION ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 722f69616475e59f1a343f5895a9afd513b5fefd
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349023"
---
# <a name="siowskregisterextension"></a>SIO\_WSK\_登録\_拡張機能


SIO\_WSK\_登録\_ソケット I/O 制御操作の拡張機能を使用すると、WSK サブシステムによってサポートされている拡張機能インターフェイスを登録する WSK アプリケーション。 このソケット I/O 制御操作は、すべての種類のソケットに適用されます。

拡張機能インターフェイスを登録する WSK アプリケーションを呼び出す、 [ **WskControlSocket** ](https://msdn.microsoft.com/library/windows/hardware/ff571127)関数は次のパラメーター。

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
<td><p><em>RequestType</em></p></td>
<td><p><strong>WskIoctl</strong></p></td>
</tr>
<tr class="even">
<td><p><em>ControlCode</em></p></td>
<td><p>SIO_WSK_REGISTER_EXTENSION</p></td>
</tr>
<tr class="odd">
<td><p><em>レベル</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><em>InputSize</em></p></td>
<td><p>sizeof(WSK_EXTENSION_CONTROL_IN)</p></td>
</tr>
<tr class="odd">
<td><p><em>InputBuffer</em></p></td>
<td><p>ポインターを<a href="https://msdn.microsoft.com/library/windows/hardware/ff571167" data-raw-source="[&lt;strong&gt;WSK_EXTENSION_CONTROL_IN&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff571167)"> <strong>WSK_EXTENSION_CONTROL_IN</strong> </a>構造体。 この構造体にはへのポインターが含まれています、<a href="https://msdn.microsoft.com/library/windows/hardware/ff568373" data-raw-source="[Network Programming Interface (NPI)](https://msdn.microsoft.com/library/windows/hardware/ff568373)">ネットワーク プログラミング インターフェイス (NPI)</a>拡張機能インターフェイスやディスパッチ テーブルと拡張機能の WSK アプリケーションの実装のコンテキストへのポインターの識別子インターフェイスです。</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSize</em></p></td>
<td><p>sizeof(WSK_EXTENSION_CONTROL_OUT)</p></td>
</tr>
<tr class="odd">
<td><p><em>OutputBuffer</em></p></td>
<td><p>ポインターを<a href="https://msdn.microsoft.com/library/windows/hardware/ff571168" data-raw-source="[&lt;strong&gt;WSK_EXTENSION_CONTROL_OUT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff571168)"> <strong>WSK_EXTENSION_CONTROL_OUT</strong> </a>構造体。 この構造体は、ディスパッチ テーブルへのポインターと、拡張機能インターフェイスの実装の WSK サブシステムのためのコンテキストへのポインターを受け取ります。</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p>NULL</p></td>
</tr>
</tbody>
</table>


呼び出すときに、WSK アプリケーションが IRP へのポインターを指定しない、 **WskControlSocket**拡張機能インターフェイスを登録する関数。

ディスパッチ テーブル構造体の内容は、拡張機能インターフェイスに固有です。

拡張機能インターフェイスを登録の詳細については、[拡張機能インターフェイスを登録する](https://msdn.microsoft.com/library/windows/hardware/ff570461)を参照してください。

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

 

 




