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
ms.openlocfilehash: 00435311f4ee55af17d7a5d7c6f342d9c72796b5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372734"
---
# <a name="devpropkey-structure"></a>DEVPROPKEY 構造体


Windows Vista および以降のバージョンの Windows では、DEVPROPKEY 構造が内のデバイス プロパティのデバイス プロパティのキーを表します、[統一されたデバイス プロパティのモデル](https://docs.microsoft.com/windows-hardware/drivers/install/unified-device-property-model--windows-vista-and-later-)します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
struct DEVPROPKEY {
  DEVPROPGUID fmtid;
  DEVPROPID   pid;
};
```

<a name="members"></a>Members
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

<a name="remarks"></a>注釈
-------

DEVPROPKEY 構造がの一部、[統一されたデバイス プロパティのモデル](https://docs.microsoft.com/windows-hardware/drivers/install/unified-device-property-model--windows-vista-and-later-)します。

システム提供のデバイス プロパティのキーの基本セットが定義されている*Devpkey.h*します。

[**定義\_DEVPROPKEY** ](https://docs.microsoft.com/windows-hardware/drivers/install/define-devpropkey)マクロは、デバイス プロパティのキーを表す DEVPROPKEY 構造体のインスタンスを作成します。

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


[**DEFINE\_DEVPROPKEY**](https://docs.microsoft.com/windows-hardware/drivers/install/define-devpropkey)

 

 






