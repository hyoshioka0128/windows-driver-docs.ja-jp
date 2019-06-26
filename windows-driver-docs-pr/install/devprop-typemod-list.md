---
title: DEVPROP_TYPEMOD_LIST
description: Windows Vista および Windows の以降のバージョンでは、DEVPROP_TYPEMOD_LIST 識別子は DEVPROP_TYPE_STRING および DEVPROP_TYPE_SECURITY_DESCRIPTOR_STRING の基本データ型識別子とのみ組み合わせることができますをプロパティ データ型修飾子を表します。表すデータ型のプロパティの識別子を作成する、 [REG_MULTI_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types) NULL で終わる Unicode 文字列のリスト。
ms.assetid: 0beaa778-55c9-45ac-8163-91d82794a845
keywords:
- DEVPROP_TYPEMOD_LIST デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPROP_TYPEMOD_LIST
api_location:
- Devpropdef.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 4e30190d6f4ed7db63f6c303d8faec4379c6a397
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372736"
---
# <a name="devproptypemodlist"></a>DEVPROP_TYPEMOD_LIST


Windows Vista および Windows の以降のバージョンでは、DEVPROP_TYPEMOD_LIST 識別子とのみ組み合わせることができますをプロパティ データ型修飾子を表します、 [**基本データ型識別子**](https://docs.microsoft.com/previous-versions/ff537793(v=vs.85)) 。 [**DEVPROP_TYPE_STRING** ](devprop-type-string.md)と[ **DEVPROP_TYPE_SECURITY_DESCRIPTOR_STRING** ](devprop-type-security-descriptor-string.md)にプロパティ データ型識別子の作成表す、 [REG_MULTI_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types) NULL で終わる Unicode 文字列のリスト。

<a name="remarks"></a>注釈
-------

組み合わせることはできません DEVPROP_TYPEMOD_LIST [ **DEVPROP_TYPE_EMPTY**](devprop-type-empty.md)、 [ **DEVPROP_TYPE_NULL**](devprop-type-null.md)、 [ **DEVPROP_TYPE_SECURITY_DESCRIPTOR**](devprop-type-security-descriptor.md)、または任意の固定長の基本データ型識別子。

文字列のリストを表すデータ型のプロパティの識別子を作成するには、DEVPROP_TYPEMOD_LIST プロパティ データ型の修飾子と対応する DEVPROP_TYPE_Xxx 識別子の間のビットごとの OR を実行します。 たとえば、指定するため、 [REG_MULTI_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)一連の Unicode 文字列の場合は、次のビットごとの OR を実行します。(DEVPROP_TYPEMOD_LIST | DEVPROP_TYPE_STRING).

サイズ、 [REG_MULTI_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types) NULL で終わる Unicode 文字列の一覧は、最終版を含むリストのサイズ**NULL**リストを終了します。

固定長データ値の配列を表すデータ型のプロパティの識別子を作成する方法については、次を参照してください。 [ **DEVPROP_TYPEMOD_ARRAY**](devprop-typemod-array.md)します。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Devpropdef.h (Devpropdef.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**DEVPROP_TYPEMOD_ARRAY**](devprop-typemod-array.md)

 

 






