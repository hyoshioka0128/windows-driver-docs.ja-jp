---
title: SM\_RemovePersistentBinding 関数
description: SM\_RemovePersistentBinding メソッド バインドを解除する 1 つまたは複数永続的な SCSI Id を指定する、指定したアダプターのポート。
ms.assetid: 475c2f5f-4a1c-48b4-9a43-81d03b1b737d
keywords:
- 記憶装置の SM_RemovePersistentBinding 関数
topic_type:
- apiref
api_name:
- SM_RemovePersistentBinding
api_location:
- Hbapiwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: ba4d03f231c468663f124c6e780a99076f429634
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532433"
---
# <a name="smremovepersistentbinding-function"></a>SM\_RemovePersistentBinding 関数


SM\_RemovePersistentBinding メソッド バインドを解除する 1 つまたは複数永続的な SCSI Id を指定する、指定したアダプターのポート。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
void SM_RemovePersistentBinding(
   [in, HBAType("HBA_WWN")] uint8                      HbaPortWWN[8],
   [in, HBAType("HBA_WWN")] uint8                      DomainPortWWN[8],
   [in] uint32                                         EntryCount,
   [in, WmiSizeIs("EntryCount")] MS_SMHBA_BINDINGENTRY Entry[],
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS             HBAStatus
);
```

<a name="parameters"></a>パラメーター
----------

*HbaPortWWN*   
永続的なバインドを削除予定のポートの世界中の名前 (WWN)。

*DomainPortWWN*   
世界中のコールバック名 (WWN) ポートは\_を任意のポートの最小値を持つ識別子\_物理ファイバー チャネル ポートを使用して検出された SMP ポートの識別子。 値が 0 の物理ファイバー チャネル ポートを使用して SMP ポートが検出されない場合があります。

*EntryCount*   
入力パラメーターで、WMI プロバイダーをレポートできるバインド エントリの数。

*エントリ*   
一連の MS\_SMHBA\_BINDINGENTRY 型永続的なバインディング。

*HBAStatus*   
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

[**SM\_RemovePersistentBinding\_IN**](https://msdn.microsoft.com/library/windows/hardware/ff566269)

[**SM\_RemovePersistentBinding\_アウト**](https://msdn.microsoft.com/library/windows/hardware/ff566271)

 

 






