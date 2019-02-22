---
title: バグ チェック 0x164 WIN32K_CRITICAL_FAILURE
description: WIN32K_CRITICAL_FAILURE のバグ チェックでは、0x00000164 の値を持ちます。 これは、Win32k の重大なエラーが発生したことを示します。
ms.assetid: 6274C852-53DA-4E01-B2A6-D7485501BE50
keywords:
- バグ チェック 0x164 WIN32K_CRITICAL_FAILURE
- WIN32K_CRITICAL_FAILURE
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- WIN32K_CRITICAL_FAILURE
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 829cbca4f2db3534eafcb6466e1c945a1d3760ac
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559680"
---
# <a name="bug-check-0x164-win32kcriticalfailure"></a>バグ チェック 0x164 の。WIN32K\_重大\_エラー


WIN32K\_重大\_エラーのバグ チェックが 0x00000164 の値を持ちます。 これは、Win32k の重大なエラーが発生したことを示します。

**重要な**プログラマ向けのトピックです。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。

## <a name="win32kcriticalfailure-parameters"></a>WIN32K\_重大\_エラー パラメーター


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">1</td>
<td align="left"><p>1 - エラーの種類。</p>
0x1:REGION_VALIDATION_FAILURE リージョンが画面の範囲外です。
<p>2 - DC へのポインター</p>
<p>3 - 画面へのポインター</p>
<p>4 - リージョンへのポインター</p>
0x2:OPERATOR_NEW_USED - 演算子&quot;新しい&quot;メモリを割り当てるために使用します。
<p>2-予約されています</p>
<p>3-予約されています</p>
<p>4-予約されています</p>
<p></p>
0x3:CRITICAL_APISET_EXTENSIONS_MISSING - 重要な拡張機能 APISET API がありません。
<p>2-wchar_t * に不足している関数の名前</p>
<p>3-予約されています</p>
<p>4-予約されています</p>
0x4:GDI_SPRITE_SURFACE_INVALID_DELETE - GDI スプライト&#39;s 図形は、スプライトを削除することがなく削除中です。
<p>2 - 画面に処理します。</p>
<p>3 - 画面に参照カウント</p>
<p>4 - サーフェスの所有者の PID</p>
0x5。POINTER_DEVICE_EXCLUSIVE_OPEN_FAILED - デバイスを開けませんでした。
<p></p>
<p>2 - デバイスの UNICODE_STRING</p>
<p>3-予約されています</p>
<p>4-予約されています</p>
0x8:PUBLIC_DC_INVALID_PRIVATE_MEMBER - パブリック DC が、特定のプロセスが所有するオブジェクトへのポインターです。
<p>2 - DC へのポインター</p>
<p>3 - オブジェクトを所有するプロセス id</p>
<p>4-予約されています</p>
0 xa:TTFD_INVOKE_ILLEGAL_ID - 無効な関数のテーブルのインデックスは、TTFD で使用されています。
<p>2-予約されています</p>
<p>3-予約されています</p>
<p>4-予約されています</p>
0 xb:OTFD_INVOKE_ILLEGAL_ID - 無効な関数のテーブルのインデックスは、ATMFD で使用されています。
<p>2-予約されています</p>
<p>3-予約されています</p>
<p>4-予約されています</p>
0 xc:GFPE_INVOKE_ILLEGAL_ID - 無効な関数のテーブルのインデックスは、パレットで使用されています。
<p>2 - パレットへのポインター</p>
<p>3-無効なインデックス</p>
<p>4-最大の有効なインデックス + 1</p>
0x10:USER_SAS_REGISTRATION_FAILED - SAS キーの登録に失敗しました。
<p>2-vkey</p>
<p>3-修飾子</p>
<p>4-フラグ</p></td>
</tr>
<tr class="even">
<td align="left">2</td>
<td align="left">パラメーター 1 を参照してください。</td>
</tr>
<tr class="odd">
<td align="left">3</td>
<td align="left">パラメーター 1 を参照してください。</td>
</tr>
<tr class="even">
<td align="left">4</td>
<td align="left">パラメーター 1 を参照してください。</td>
</tr>
</tbody>
</table>

 

 

 




