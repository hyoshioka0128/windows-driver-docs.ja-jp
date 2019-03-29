---
title: SM\_GetTargetMapping 関数
description: SM\_GetTargetMapping WMI メソッドは、これらの論理単位の一連のオペレーティング システムの論理ユニットを一意に識別する情報とファイバー チャネルのプロトコル (FCP) 識別子の間のマッピングを取得します。
ms.assetid: db18920c-327d-4349-8821-6d7fb68eccbd
keywords:
- 記憶装置の SM_GetTargetMapping 関数
topic_type:
- apiref
api_name:
- SM_GetTargetMapping
api_location:
- Hbapiwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: d105b8218755279ceb7f442ff63f96c57c7127de
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574680"
---
# <a name="smgettargetmapping-function"></a>SM\_GetTargetMapping 関数


SM\_GetTargetMapping WMI メソッドは、これらの論理単位の一連のオペレーティング システムの論理ユニットを一意に識別する情報とファイバー チャネルのプロトコル (FCP) 識別子の間のマッピングを取得します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
void SM_GetTargetMapping(
   [in, HBAType("HBA_WWN")] uint8                       HbaPortWWN[8],
   [in, HBAType("HBA_WWN")] uint8                       DomainPortWWN[8],
   [in] uint32                                          InEntryCount,
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS              HBAStatus,
   [out] uint32                                         TotalEntryCount,
   [out] uint32                                         OutEntryCount,
   [out, WmiSizeIs("OutEntryCount")] MS_SMHBA_SCSIENTRY Entry[]
);
```

<a name="parameters"></a>パラメーター
----------

*HbaPortWWN*   
ポート マッピングのテーブルが含まれるが取得するには世界中の名 (WWN)。 この情報は、GetTargetMapping の HbaPortWWN メンバーのミニポート ドライバーに配信\_構造体。

*DomainPortWWN*   
世界中のコールバック名 (WWN) ポートは\_任意のポートの最小値を含む識別子\_物理ファイバー チャネル ポートを使用して検出された SMP ポートの識別子。 値が 0 の物理ファイバー チャネル ポートを使用して SMP ポートが検出されない場合があります。

*InEntryCount*   
入力パラメーターで、WMI プロバイダーをレポートできるバインド エントリの数。

*HBAStatus*   
操作の状態。 使用できる値とその説明の一覧は、次を参照してください。、 [HBA\_状態](hba-status.md)構造体。 ミニポート ドライバーでは、この情報を返します、GetFcpTargetMapping の HBAStatus メンバー\_構造体。

*TotalEntryCount*   
HBA に関連付けられている永続的なバインドの合計数。

*OutEntryCount*   
SM によって取得されるマッピングの合計数\_GetTargetMapping メソッド。 この値は、TotalEntryCount 以下になります。

*エントリ*   
MS の種類の構造体の配列\_SMHBA\_SCSIENTRY オペレーティング システムとファイバー チャネルのプロトコル (FCP) 識別子の HBA のバインディングを記述します。

<a name="return-value"></a>戻り値
------------

WMI メソッドには適用されません。

<a name="remarks"></a>コメント
-------

この WMI メソッドは、ミリ秒に属する\_SM\_TargetInformationMethods WMI クラスです。

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
<td align="left">Hbapiwmi.h</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[HBA\_状態](hba-status.md)

[**SM\_GetTargetMapping\_IN**](https://msdn.microsoft.com/library/windows/hardware/ff566256)

[**SM\_GetTargetMapping\_アウト**](https://msdn.microsoft.com/library/windows/hardware/ff566258)

 

 






