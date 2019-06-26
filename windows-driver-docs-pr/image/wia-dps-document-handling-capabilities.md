---
title: WIA\_DPS\_ドキュメント\_処理\_機能
description: WIA\_DPS\_ドキュメント\_処理\_機能プロパティには、スキャナーの機能が含まれています。
ms.assetid: 19c9cbd0-19ef-4d44-85f1-25e71f9a92bc
keywords:
- WIA_DPS_DOCUMENT_HANDLING_CAPABILITIES イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_DPS_DOCUMENT_HANDLING_CAPABILITIES
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 92d5c8a07be5fa414f59bdc3d83400d5f95c5fda
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67393356"
---
# <a name="wiadpsdocumenthandlingcapabilities"></a>WIA\_DPS\_ドキュメント\_処理\_機能


WIA\_DPS\_ドキュメント\_処理\_機能プロパティには、スキャナーの機能が含まれています。

## <span id="ddk_wia_dps_document_handling_capabilities_si"></span><span id="DDK_WIA_DPS_DOCUMENT_HANDLING_CAPABILITIES_SI"></span>


プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_NONE

アクセス権:読み取り専用かどうか

<a name="remarks"></a>注釈
-------

アプリケーションの読み取り、WIA\_DPS\_ドキュメント\_処理\_スキャナーのフラット ベッド ドキュメント フィーダー付き、や両面印刷ユニットがインストールされているかどうかを判断する機能のプロパティ。 さらにインストールされている機能を定義するのに、このプロパティを使用することもできます。 WIA ミニドライバーは、作成し、このプロパティを保持します。

次の表では、だけで Windows 8 では有効な定数について説明します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Value</th>
<th>定義</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>・ インプリント ・</p></td>
<td><p>・ インプリント ・</p></td>
</tr>
<tr class="even">
<td><p>裏書き</p></td>
<td><p>裏書き</p></td>
</tr>
<tr class="odd">
<td><p>BARCODE_READER</p></td>
<td><p>バーコード リーダー</p></td>
</tr>
<tr class="even">
<td><p>PATCH_CODE_READER</p></td>
<td><p>修正プログラム コード リーダー</p></td>
</tr>
<tr class="odd">
<td><p>MICR_READER</p></td>
<td><p>MICR リーダー</p></td>
</tr>
</tbody>
</table>

 

次の表では、だけで Windows 7 で有効な定数について説明します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Value</th>
<th>定義</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>AUTO_SOURCE</p></td>
<td><p>デバイスでサポートする<a href="https://docs.microsoft.com/windows-hardware/drivers/image/auto-configured-scanning" data-raw-source="[auto-configured scanning](https://docs.microsoft.com/windows-hardware/drivers/image/auto-configured-scanning)">スキャンの自動構成</a>します。</p></td>
</tr>
</tbody>
</table>

 

次の表に、Windows 7 と Windows Vista では、有効な定数が、Windows XP ではありません。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Value</th>
<th>定義</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ADVANCED_DUP</p></td>
<td><p>デバイスは、各ドキュメントのサイズに高度な双方向のスキャンの構成を個別にサポートします。</p></td>
</tr>
<tr class="even">
<td><p>DETECT_FILM_TPA</p></td>
<td><p>スキャナーは、透明性またはアダプターをスキャンするフィルムがスキャンする準備ができたときに検出できます。</p></td>
</tr>
<tr class="odd">
<td><p>DETECT_STOR</p></td>
<td><p>内部ストレージでドキュメントがある場合に、スキャナーを検出できます。</p></td>
</tr>
<tr class="even">
<td><p>FILM_TPA</p></td>
<td><p>スキャナーは、透過性またはアダプターをスキャンするフィルムがあります。</p></td>
</tr>
<tr class="odd">
<td><p>STOR</p></td>
<td><p>スキャナーには、内部記憶装置が搭載されています。</p></td>
</tr>
</tbody>
</table>

 

次の表では、Windows 7、Windows Vista、Windows XP と有効な定数について説明します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Value</th>
<th>定義</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>DETECT_FEED</p></td>
<td><p>スキャナーは、フィーダーにドキュメントを検出できます。</p></td>
</tr>
<tr class="even">
<td><p>DETECT_FLAT</p></td>
<td><p>スキャナーは、フラット ベッド プラテン上のドキュメントを検出できます。</p></td>
</tr>
<tr class="odd">
<td><p>DETECT_SCAN</p></td>
<td><p>スキャナーは、スキャンでのみ、フィーダーにドキュメントを検出できます。</p></td>
</tr>
<tr class="even">
<td><p>DUP</p></td>
<td><p>スキャナーが両面印刷ユニットです。</p></td>
</tr>
<tr class="odd">
<td><p>フィード</p></td>
<td><p>スキャナーは、インストールされているドキュメント フィーダーにします。</p></td>
</tr>
<tr class="even">
<td><p>フラット</p></td>
<td><p>スキャナーは、フラット ベッドからプラテン上にします。</p></td>
</tr>
</tbody>
</table>

 

次の表に、のみ; で Windows XP を備えた有効な定数これらのフラグは、Windows 7 および Windows Vista に使用されなくなったし、は使用できません。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Value</th>
<th>定義</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>DETECT_DUP</p></td>
<td><p>スキャナーは、ユーザーからの双方向のスキャン要求を検出できます。</p></td>
</tr>
<tr class="even">
<td><p>DETECT_DUP_AVAIL</p></td>
<td><p>両面印刷ユニットがインストールされている場合、スキャナーを検出できます。</p></td>
</tr>
<tr class="odd">
<td><p>DETECT_FEED_AVAIL</p></td>
<td><p>ドキュメント フィーダー付きのインストール時に、スキャナーを検出できます。</p></td>
</tr>
</tbody>
</table>

 

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Wiadef.h (Wiadef.h を含む)</td>
</tr>
</tbody>
</table>

 

 





