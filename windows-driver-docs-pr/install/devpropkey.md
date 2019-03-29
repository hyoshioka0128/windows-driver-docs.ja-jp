---
title: DEVPROPKEY 構造体
description: Windows Vista および Windows の以降のバージョンでは、DEVPROPKEY 構造体は、統一されたデバイス プロパティのモデル内のデバイス プロパティのデバイス プロパティのキーを表します。
ms.assetid: 98986d43-84c0-44e6-83f9-08e872ea5e6d
keywords:
- DEVPROPKEY 構造デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPROPKEY
api_location:
- devpropdef.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 4ba0806bd159e35cb6e7f9af3bc25eafd339a0a8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573170"
---
# <a name="devpropkey-structure"></a>DEVPROPKEY 構造体


Windows Vista および以降のバージョンの Windows では、DEVPROPKEY 構造が内のデバイス プロパティのデバイス プロパティのキーを表します、[統一されたデバイス プロパティのモデル](https://msdn.microsoft.com/library/windows/hardware/ff553515)します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
struct DEVPROPKEY {
  DEVPROPGUID fmtid;
  DEVPROPID   pid;
};
```

<a name="members"></a>メンバー
-------

**fmtid**  
プロパティのカテゴリを示す DEVPROPGUID に型指定された値。

DEVPROPGUID のデータ型は、として定義されます。

```cpp
typedef GUID  DEVPROPGUID, *PDEVPROPGUID;
```

**pid**  
プロパティのカテゴリ内のプロパティを一意に識別する DEVPROPID に型指定された値。 内部システム上の理由から、プロパティの識別子が 2 つ以上である必要があります。

DEVPROPID のデータ型は、として定義されます。

```cpp
typedef ULONG DEVPROPID, *PDEVPROPID;
```

<a name="remarks"></a>コメント
-------

DEVPROPKEY 構造がの一部、[統一されたデバイス プロパティのモデル](https://msdn.microsoft.com/library/windows/hardware/ff553515)します。

システム提供のデバイス プロパティのキーの基本セットが定義されている*Devpkey.h*します。

[**定義\_DEVPROPKEY** ](https://msdn.microsoft.com/library/windows/hardware/ff541072)マクロは、デバイス プロパティのキーを表す DEVPROPKEY 構造体のインスタンスを作成します。

<a name="requirements"></a>必要条件
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


[**DEFINE\_DEVPROPKEY**](https://msdn.microsoft.com/library/windows/hardware/ff541072)

 

 






