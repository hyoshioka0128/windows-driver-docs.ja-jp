---
title: SM\_SetPersistentBinding 関数
description: SM\_SetPersistentBinding メソッドは、OS 固有の LUN の情報を論理ユニットのファイバー チャネルのプロトコル (FCP) 識別子にマップする HBA ミニポート ドライバーで使用されるバインドを設定します。
ms.assetid: 722f7216-9ff4-4f12-a4fe-e1f8f9e594e1
keywords:
- 記憶装置の SM_SetPersistentBinding 関数
topic_type:
- apiref
api_name:
- SM_SetPersistentBinding
api_location:
- Hbapiwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: e6fa74b90d0e3dbbf720487ef3f8b57dcd2ac383
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549577"
---
# <a name="smsetpersistentbinding-function"></a>SM\_SetPersistentBinding 関数


SM\_SetPersistentBinding メソッドは、OS 固有の LUN の情報を論理ユニットのファイバー チャネルのプロトコル (FCP) 識別子にマップする HBA ミニポート ドライバーで使用されるバインドを設定します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
void SM_SetPersistentBinding(
   [in, HBAType("HBA_WWN")] uint8                        HbaPortWWN[8],
   [in, HBAType("HBA_WWN")] uint8                        DomainPortWWN[8],
   [in] uint32                                           InEntryCount,
   [in, WmiSizeIs("InEntryCount")] MS_SMHBA_BINDINGENTRY Entry[],
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS               HBAStatus,
   [out] uint32                                          OutStatusCount,
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS               EntryStatus
);
```

<a name="parameters"></a>パラメーター
----------

*HbaPortWWN*   
永続的なバインドが設定するポートの世界中の名前 (WWN)。

*DomainPortWWN*   
世界中のコールバック名 (WWN) ポートは\_を任意のポートの最小値を持つ識別子\_物理ファイバー チャネル ポートを使用して検出された SMP ポートの識別子。 値が 0 の物理ファイバー チャネル ポートを使用して SMP ポートが検出されない場合があります。

*InEntryCount*   
入力パラメーターで、WMI プロバイダーをレポートできるバインド エントリの数。

*エントリ*   
SMHBA 型の構造体の配列\_SCSIENTRY をオペレーティング システムと SAS の識別子の HBA のバインディングについて説明します。

*HBAStatus*   
操作の状態。 使用できる値とその説明の一覧は、次を参照してください。 [HBA\_状態](hba-status.md)します。 ミニポート ドライバーでは、この情報を返します、GetPersistentBinding の HBAStatus メンバー\_構造体。

*OutStatusCount*   
SM によって取得される永続的なバインドの合計数\_GetPersistentBinding メソッド。 この値は、TotalEntryCount 以下になります。

*EntryStatus*   
操作の状態。 使用できる値とその説明の一覧は、次を参照してください。 [HBA\_状態](hba-status.md)します。 ミニポート ドライバーでは、この情報を返します、GetPersistentBinding の HBAStatus メンバー\_構造体。

<a name="return-value"></a>戻り値
------------

WMI メソッドには適用されません。

<a name="remarks"></a>注釈
-------

この WMI メソッドは、ミリ秒に属する\_SM\_TargetInformationMethods WMI クラスです。

<a name="requirements"></a>要件
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
<td align="left">Hbapiwmi.h</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[HBA\_状態](hba-status.md)

[**SM\_SetPersistentBinding\_IN**](https://msdn.microsoft.com/library/windows/hardware/ff566334)

[**SM\_SetPersistentBinding\_アウト**](https://msdn.microsoft.com/library/windows/hardware/ff566335)

 

 






