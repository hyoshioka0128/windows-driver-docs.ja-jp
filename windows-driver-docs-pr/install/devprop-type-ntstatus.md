---
title: DEVPROP_TYPE_NTSTATUS
description: DEVPROP_TYPE_NTSTATUS 識別子は Ntstatus.h に定義されている NTSTATUS ステータス コードの値の基本データ型識別子を表します。
ms.assetid: 7593d24d-8e89-409e-9047-0c14268b8e62
keywords:
- DEVPROP_TYPE_NTSTATUS デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPROP_TYPE_NTSTATUS
api_location:
- Devpropdef.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: cf8ded26b336b57c798ec9085c97824a77244f00
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557099"
---
# <a name="devproptypentstatus"></a>DEVPROP_TYPE_NTSTATUS


DEVPROP_TYPE_NTSTATUS 識別子は Ntstatus.h に定義されている NTSTATUS ステータス コードの値の基本データ型識別子を表します。

<a name="remarks"></a>注釈
-------

Windows Vista および Windows での以降のバージョンで、[統一されたデバイス プロパティのモデル](https://msdn.microsoft.com/library/windows/hardware/ff553515)も定義、 [ **DEVPROP_TYPE_ERROR** ](devprop-type-error.md) Microsoft の基本データ型識別子Win32 エラー コード値。

のみ DEVPROP_TYPE_NTSTATUS を組み合わせることができます、 [ **DEVPROP_TYPEMOD_ARRAY** ](devprop-typemod-array.md)プロパティ データ型の修飾子。

### <a name="setting-a-property-of-this-type"></a>この型のプロパティを設定

基本データ型は DEVPROP_TYPE_NTSTATUS プロパティを設定する呼び出し、対応する **SetupDiSet * * * Xxx*プロパティ関数と set 関数は、次のようにパラメーターを入力します。

- 設定、 *PropertyType* DEVPROP_TYPE_NTSTATUS パラメーター。

- 設定、 *PropertyBuffer*パラメーターを少なくとも 1 つの NTSTATUS 値を含むことのできるバッファーへのポインター。

- 設定、 *PropertyBufferSize*パラメーターを<strong>sizeof (</strong>NTSTATUS<strong>)</strong>します。

- プロパティを設定する適切な関数の残りのパラメーターを設定します。

### <a name="retrieving-the-descriptive-text-for-a-ntstatus-error-code-value"></a>NTSTATUS のエラー コード値の説明テキストを取得します。

NTSTATUS エラー コード値に関連付けられている説明テキストを取得する、 **FormatMessage**関数 (Windows SDK に記載されている) 時に、次のようにします。

-   値に FORMAT_MESSAGE_FROM_SYSTEM フラグと FORMAT_MESSAGE_FROM_HMODULE フラグのビットごとの OR を含める、 *dwflags*パラメーター。

-   設定、 *lpSource*パラメーターを識別するハンドルを*NtDLL.dll*モジュールにはわかりやすいテキストのソースです。

-   設定、 *dwMessageID*パラメーターをエラー コード値。

-   わかりやすいテキストを取得する、必要に応じて、他のオプションとパラメーターを設定します。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>バージョン</p></td>
<td align="left"><p>Windows Vista と Windows の以降のバージョン。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Devpropdef.h (Devpropdef.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**DEVPROP_TYPE_ERROR**](devprop-type-error.md)

[**DEVPROP_TYPEMOD_ARRAY**](devprop-typemod-array.md)

 

 






