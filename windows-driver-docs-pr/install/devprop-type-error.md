---
title: DEVPROP_TYPE_ERROR
description: DEVPROP_TYPE_ERROR 識別子は、WINERROR で定義されている Microsoft Win32 エラー コード値の基本データ型識別子を表します。H.
ms.assetid: fe8fa3de-a984-4c6f-902f-5eda24402a65
keywords:
- DEVPROP_TYPE_ERROR デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPROP_TYPE_ERROR
api_location:
- Devpropdef.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 6a6be27334e5fefe69b4a5772ea516a9a2632094
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381722"
---
# <a name="devproptypeerror"></a>DEVPROP_TYPE_ERROR


DEVPROP_TYPE_ERROR 識別子は、WINERROR で定義されている Microsoft Win32 エラー コード値の基本データ型識別子を表します。H.

<a name="remarks"></a>注釈
-------

Windows Vista および Windows での以降のバージョンで、[統一されたデバイス プロパティのモデル](https://docs.microsoft.com/windows-hardware/drivers/install/unified-device-property-model--windows-vista-and-later-)も定義、 [ **DEVPROP_TYPE_NTSTATUS** ](devprop-type-ntstatus.md) NTSTATUS の基本データ型識別子エラー コード値。

のみ DEVPROP_TYPE_ERROR を組み合わせることができます、 [ **DEVPROP_TYPEMOD_ARRAY** ](devprop-typemod-array.md)プロパティ データ型の修飾子。

### <a name="setting-a-property-of-this-type"></a>この型のプロパティを設定

基本データ型は DEVPROP_TYPE_ERROR プロパティを設定するに対応する SetupDiSet を呼び出す*Xxx*プロパティ関数と set 関数は、次のようにパラメーターを入力します。

-   設定、 *PropertyType* DEVPROP_TYPE_ERROR パラメーター。

-   設定、 *PropertyBuffer*パラメーターを少なくとも 1 つの Win32 エラー コード値を含むことのできるバッファーへのポインター。

-   設定、 *PropertyBufferSize*パラメーター`sizeof(ULONG)`します。

-   プロパティを設定する適切な関数の残りのパラメーターを設定します。

### <a name="retrieving-the-descriptive-text-for-a-win32-error-code-value"></a>Win32 エラー コード値の説明テキストを取得します。

Win32 エラー コードに関連付けられている説明テキストを取得する、 [ **FormatMessage** ](https://docs.microsoft.com/windows/desktop/api/winbase/nf-winbase-formatmessage)関数 (Windows SDK に記載されている) 時に、次のようにします。

-   値で FORMAT_MESSAGE_FROM_SYSTEM フラグが含まれて、 *dwflags*パラメーター。

-   設定、 *dwMessageID*パラメーターをエラー コード値。

-   わかりやすいテキストを取得する、必要に応じて、他のオプションとパラメーターを設定します。

<a name="requirements"></a>必要条件
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


[**DEVPROP_TYPE_NTSTATUS**](devprop-type-ntstatus.md)

[**DEVPROP_TYPEMOD_ARRAY**](devprop-typemod-array.md)

 

 






