---
title: WDI_TLV_ADAPTER_RESUME_REQUIRED
description: WDI_TLV_ADAPTER_RESUME_REQUIRED では、アダプターの再開が必要なかどうかを指定する TLV です。
ms.assetid: 341B871A-F789-447E-A74C-3274B6B8B14A
ms.date: 07/18/2017
keywords:
- WDI_TLV_ADAPTER_RESUME_REQUIRED ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: b2f8d2cb5ca268dcc02732dc7913dea6bc9b16bc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380566"
---
# <a name="wditlvadapterresumerequired"></a>WDI\_TLV\_アダプター\_再開\_必要な作業


WDI\_TLV\_アダプター\_再開\_必要な作業は、アダプターの再開が必要なかどうかを指定する TLV します。

## <a name="tlv-type"></a>TLV 型


0xB7

## <a name="length"></a>長さ


UINT8 のサイズをバイト単位で。

## <a name="values"></a>値


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>型</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>UINT8</td>
<td>アダプターの再開が必要なかどうかを指定します。
<p>有効な値は 0 (不要) および 1 (必須です)。 かどうか 1 に設定、ファームウェア サポートが必要 OS をそのコンテキストを再開します。</p></td>
</tr>
</tbody>
</table>

 

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>サポートされている最小のクライアント</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>サポートされている最小のサーバー</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>Header</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 




