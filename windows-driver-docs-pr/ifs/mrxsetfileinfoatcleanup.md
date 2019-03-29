---
title: MRxSetFileInfoAtCleanup ルーチン
description: MRxSetFileInfoAtCleanup ルーチンは、ネットワークのミニ リダイレクターがクリーンアップでファイル システム オブジェクトでファイルの情報を設定することを要求する RDBSS によって呼び出されます。
ms.assetid: 099244ee-cc66-4500-9fee-a10238aaa66c
keywords:
- MRxSetFileInfoAtCleanup ルーチン インストール可能なファイル システム ドライバー
- PMRX_CALLDOWN
topic_type:
- apiref
api_name:
- MRxSetFileInfoAtCleanup
api_location:
- mrx.h
api_type:
- UserDefined
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c4fdd8d5637ad3796f6f27357ee934ceec746694
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571377"
---
# <a name="mrxsetfileinfoatcleanup-routine"></a>MRxSetFileInfoAtCleanup ルーチン


*MRxSetFileInfoAtCleanup*ルーチンを呼び出して[RDBSS](https://msdn.microsoft.com/library/windows/hardware/ff556810)ネットワーク ミニ リダイレクターがクリーンアップでファイル システム オブジェクトでファイルの情報を設定することを要求します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
PMRX_CALLDOWN MRxSetFileInfoAtCleanup;

NTSTATUS MRxSetFileInfoAtCleanup(
  _Inout_ PRX_CONTEXT RxContext
)
{ ... }
```

<a name="parameters"></a>パラメーター
----------

*RxContext* \[入力、出力\]  
RX へのポインター\_CONTEXT 構造体。 このパラメーターには、操作を要求している IRP が含まれています。

<a name="return-value"></a>戻り値
------------

*MRxSetFileInfoAtCleanup*ステータスを返します\_成功または適切な NTSTATUS 値に成功しました。

<a name="remarks"></a>コメント
-------

RDBSS への呼び出しを発行する*MRxSetFileInfoAtCleanup*ファイル オブジェクトへの最後のハンドルが閉じられたときのクリーンアップ中にします。 これは、ファイル オブジェクトへの最後の参照が削除されたときに呼び出される、閉じる操作よりも異なります。

*MRxSetFileInfoAtCleanup*ファイルまたはファイルのサイズのタイムスタンプが変更された場合、RDBSS によって呼び出されます。 呼び出し*MRxSetFileInfoAtCleanup* RDBSS でが行われるとは別にこれらの変更の各します。 ファイルのサイズと、タイムスタンプの両方が変更されているかどうかは、により、2 つの呼び出しを RDBSS *MRxSetFileInfoAtCleanup*します。

呼び出しの前に*MRxSetFileInfoAtCleanup*、RDBSS、RX では、次のメンバーを変更します\_によって示される CONTEXT 構造体、 *RxContext*ファイルのタイムスタンプがある場合は、パラメーター変更されました。

**Info.FileInformationClass**メンバーのセットをファイルに\_情報\_FileBasicInformation のクラスの値。

**Info.Buffer**メンバーのセットをファイルに\_BASIC\_スタックに割り当てられている情報の構造体。

**Info.Length**メンバーは、ファイル、sizeof に設定\_BASIC\_情報構造体。

呼び出しの前に*MRxSetFileInfoAtCleanup*、RDBSS、RX では、次のメンバーを変更します\_によって示される CONTEXT 構造体、 *RxContext*パラメーター ファイルのサイズが変更された場合。

**Info.FileInformationClass**メンバーのセットをファイルに\_情報\_FileEndOfFileInformation のクラスの値。

**Info.Buffer**メンバーのセットをファイルに\_エンド\_の\_ファイル\_スタックに割り当てられている情報の構造体。

**Info.Length**に設定されているメンバー <strong>sizeof (</strong>ファイル\_エンド\_の\_ファイル\_情報<strong>)</strong>します。

戻り値を無視する RDBSS *MRxSetFileInfoAtCleanup*します。

このルーチンで何もしないリターン状態を選択できますネットワーク ミニリダイレクター\_成功します。 ファイルのサイズやタイムスタンプを変更するは、クリーンアップ操作中に処理されます。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>対象プラットフォーム</p></td>
<td align="left">Desktop</td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Mrx.h (Mrx.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**MRxIsValidDirectory**](https://msdn.microsoft.com/library/windows/hardware/ff550696)

[**MRxQueryDirectory**](mrxquerydirectory.md)

[**MRxQueryEaInfo**](mrxqueryeainfo.md)

[**MRxQueryFileInfo**](mrxqueryfileinfo.md)

[**MRxQueryQuotaInfo**](mrxqueryquotainfo.md)

[**MRxQuerySdInfo**](mrxquerysdinfo.md)

[**MRxQueryVolumeInfo**](mrxqueryvolumeinfo.md)

[**MRxSetEaInfo**](mrxseteainfo.md)

[**MRxSetFileInfo**](mrxsetfileinfo.md)

[**MRxSetQuotaInfo**](mrxsetquotainfo.md)

[**MRxSetSdInfo**](mrxsetsdinfo.md)

[**MRxSetVolumeInfo**](mrxsetvolumeinfo.md)

 

 






