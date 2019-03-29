---
title: WSK_RELEASE_SD
description: WSK_RELEASE_SD
ms.assetid: de8cc759-c778-464e-9e19-984ea20c0d29
ms.date: 07/18/2017
keywords:
- WSK_RELEASE_SD ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: e6b760af3a66ce7cf6b4f02c0fb43aa9edc91c43
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582619"
---
# <a name="wskreleasesd"></a>WSK\_リリース\_SD


WSK アプリケーションの使用、WSK\_リリース\_SD のクライアント管理操作を使用して、以前に取得されているセキュリティ記述子のキャッシュされたコピーを解放する、 [ **WSK\_キャッシュ\_SD** ](wsk-cache-sd.md)クライアント管理の操作を使用して取得されたか、 [**ように\_WSK\_セキュリティ**](so-wsk-security.md)ソケット オプション。

セキュリティ記述子のキャッシュされたコピーをリリースする WSK アプリケーションが呼び出す、 [ **WskControlClient** ](https://msdn.microsoft.com/library/windows/hardware/ff571126)関数は次のパラメーター。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>パラメーター</th>
<th>[値]</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>ControlCode</em></p></td>
<td><p>WSK_RELEASE_SD</p></td>
</tr>
<tr class="even">
<td><p><em>InputSize</em></p></td>
<td><p>sizeof(PSECURITY_DESCRIPTOR)</p></td>
</tr>
<tr class="odd">
<td><p><em>InputBuffer</em></p></td>
<td><p>PSECURITY_DESCRIPTOR に型指定された変数へのポインター。 この変数には、リリースされる、キャッシュされたセキュリティ記述子を定義する SECURITY_DESCRIPTOR 構造へのポインターが含まれています。</p></td>
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

セキュリティの詳細については\_記述子構造体をセキュリティのリファレンス ページを参照してください\_Microsoft Windows SDK ドキュメントの記述子。

*Irp*パラメーターである必要があります**NULL**このクライアントのコントロールの操作。

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

 

 




