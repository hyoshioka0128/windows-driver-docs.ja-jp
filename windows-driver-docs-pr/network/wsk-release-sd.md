---
title: WSK_RELEASE_SD
description: WSK_RELEASE_SD
ms.assetid: de8cc759-c778-464e-9e19-984ea20c0d29
ms.date: 07/18/2017
keywords:
- WSK_RELEASE_SD ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: f76618607d7f9cb48d383a22cb194599e1ce3d41
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844356"
---
# <a name="wsk_release_sd"></a>WSK\_リリース\_SD


Wsk アプリケーションは WSK\_RELEASE\_SD クライアントコントロール操作を使用して、以前に[**wsk\_\_キャッシュ**](wsk-cache-sd.md)を使用して取得されたセキュリティ記述子のキャッシュされたコピーを、sd クライアント制御操作または was を使用して解放します。[ **\_WSK\_セキュリティ**](so-wsk-security.md)ソケットオプションを使用して取得されます。

セキュリティ記述子のキャッシュされたコピーを解放するために、WSK アプリケーションは、次のパラメーターを使用して[**Wskcontrolclient**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_client)関数を呼び出します。

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
<td><p>WSK_RELEASE_SD</p></td>
</tr>
<tr class="even">
<td><p><em>InputSize</em></p></td>
<td><p>sizeof (PSECURITY_DESCRIPTOR)</p></td>
</tr>
<tr class="odd">
<td><p><em>InputBuffer</em></p></td>
<td><p>PSECURITY_DESCRIPTOR で型指定された変数へのポインター。 この変数には、解放されるキャッシュされたセキュリティ記述子を定義する SECURITY_DESCRIPTOR 構造体へのポインターが含まれています。</p></td>
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

セキュリティ\_記述子の構造の詳細については、Microsoft Windows SDK のドキュメントのセキュリティ\_記述子のリファレンスページを参照してください。

このクライアントコントロール操作では、 *Irp*パラメーターは**NULL**である必要があります。

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

 

 




