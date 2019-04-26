---
title: SM\_GetPersistentBinding 関数
description: SM\_GetPersistentBinding メソッドは、HBA のミニポート ドライバーが使用するバインドを取得します。 これらのバインドは、論理ユニットを OS 固有の LUN の情報をファイバー チャネルのプロトコル (FCP) 識別子にマップします。
ms.assetid: 74a67e91-c3b3-462a-8810-a9eae64e02a7
keywords:
- 記憶装置の SM_GetPersistentBinding 関数
topic_type:
- apiref
api_name:
- SM_GetPersistentBinding
api_location:
- Hbapiwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 2e1e83efd3f45efcae3d3185f210cb60635ead03
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351668"
---
# <a name="smgetpersistentbinding-function"></a>SM\_GetPersistentBinding 関数


SM\_GetPersistentBinding メソッドは、HBA のミニポート ドライバーが使用するバインドを取得します。 これらのバインドは、論理ユニットを OS 固有の LUN の情報をファイバー チャネルのプロトコル (FCP) 識別子にマップします。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
void SM_GetPersistentBinding(
   [in, HBAType("HBA_WWN")] uint8                          HbaPortWWN[8],
   [in, HBAType("HBA_WWN")] uint8                          DomainPortWWN[8],
   [in] uint32                                             InEntryCount,
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS                 HBAStatus,
   [out] uint32                                            TotalEntryCount,
   [out] uint32                                            OutEntryCount,
   [out, WmiSizeIs("OutEntryCount")] MS_SMHBA_BINDINGENTRY Bindings[]
);
```

<a name="parameters"></a>パラメーター
----------

*HbaPortWWN*   
永続的なバインドを取得するポートの世界中の名 (WWN)。

*DomainPortWWN*   
世界中のコールバック名 (WWN) ポートは\_を任意のポートの最小値を持つ識別子\_物理ファイバー チャネル ポートを使用して検出された SMP ポートの識別子。 値が 0 の物理ファイバー チャネル ポートを使用して SMP ポートが検出されない場合があります。

*InEntryCount*   
入力パラメーターで、WMI プロバイダーをレポートできるバインド エントリの数。

*HBAStatus*   
操作の状態。 使用できる値とその説明の一覧は、次を参照してください。、 [HBA\_状態](hba-status.md)構造体。 ミニポート ドライバーでは、この情報を返します、GetPersistentBinding の HBAStatus メンバー\_構造体。

*TotalEntryCount*   
HBA に関連付けられている永続的なバインドの合計数。

*OutEntryCount*   
SM によって取得される永続的なバインドの合計数\_GetPersistentBinding メソッド。 この値は、TotalEntryCount 以下になります。

*バインド*   
MS の種類の構造体の配列\_SMHBA\_BINDINGENTRY オペレーティング システムとファイバー チャネルのプロトコル (FCP) 識別子の HBA のバインディングを記述します。

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

[**SM\_GetPersistentBinding\_IN**](https://msdn.microsoft.com/library/windows/hardware/ff566246)

[**SM\_GetPersistentBinding\_アウト**](https://msdn.microsoft.com/library/windows/hardware/ff566248)

 

 






