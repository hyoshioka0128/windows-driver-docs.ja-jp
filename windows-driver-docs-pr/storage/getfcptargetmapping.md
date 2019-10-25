---
title: GetFcpTargetMapping 関数
description: GetFcpTargetMapping WMI メソッドは、オペレーティングシステムの一連の論理ユニットとこれらの論理ユニットのファイバーチャネルプロトコル (FCP) 識別子を一意に識別する情報間のマッピングを取得します。
ms.assetid: 2e4b3554-31de-4eaa-9228-844639a219d5
keywords:
- GetFcpTargetMapping function Storage デバイス
topic_type:
- apiref
api_name:
- GetFcpTargetMapping
api_location:
- Hbaapi.lib
- Hbaapi.dll
api_type:
- LibDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 66b785938468f928ea430dbaf347ec06d3bb6a06
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837959"
---
# <a name="getfcptargetmapping-function"></a>GetFcpTargetMapping 関数


**GetFcpTargetMapping** WMI メソッドは、オペレーティングシステムの一連の論理ユニットとこれらの論理ユニットのファイバーチャネルプロトコル (FCP) 識別子を一意に識別する情報間のマッピングを取得します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
void GetFcpTargetMapping(
   [in, HBAType("HBA_WWN")] uint8                    HbaPortWWN[8],
   [in] uint32                                       InEntryCount,
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS           HBAStatus,
   [out] uint32                                      TotalEntryCount,
   [out] uint32                                      OutEntryCount,
   [out, WmiSizeIs("OutEntryCount")] HBAFCPScsiEntry Entry[]
);
```

<a name="parameters"></a>parameters
----------

*HbaPortWWN\[8\]*    
マッピングのテーブルを取得するポートの世界規模の名前。 この情報は、構造体の[**GetFcpTargetMapping\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getfcptargetmapping_in)の**HbaPortWWN**メンバーのミニポートドライバーに配信されます。

*Inentrycount*   
WMI プロバイダーが*エントリ*パラメーターで報告できるバインドエントリの数を示します。

*Hbastatus*   
戻ると、操作の状態が格納されます。 許可される値とその説明の一覧については、「 [HBA\_STATUS](hba-status.md)」を参照してください。 ミニポートドライバーは、 [**GetFcpTargetMapping\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getfcptargetmapping_out)構造体の**hbastatus**メンバーにこの情報を返します。

*Totalentrycount*   
HBA に関連付けられている永続的なバインドの合計数を示します。

*Outentrycount*   
**GetFcpTargetMapping**メソッドによって取得されたマッピングの合計数を示します。 この値は*Totalentrycount*以下です。

*エントリ\[\]*    
[**HBAFCPScsiEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_hbafcpscsientry)型の構造体の配列。これは、オペレーティングシステムとファイバーチャネルプロトコル (FCP) の識別子の間の HBA のバインドを記述します。

<a name="return-value"></a>戻り値
------------

WMI メソッドには適用されません。

<a name="remarks"></a>解説
-------

この WMI メソッドは、 [Msfc\_HBAFCPInfo WMI クラス](msfc-hbafcpinfo-wmi-class.md)に属しています。

<a name="requirements"></a>前提条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>ターゲットプラットフォーム</p></td>
<td align="left">デスクトップ</td>
</tr>
<tr class="even">
<td align="left"><p>ヘッダー</p></td>
<td align="left">Hbapiwmi (Hbapiwmi、Hbaapi. h、または Hbaapi .h を含む)</td>
</tr>
<tr class="odd">
<td align="left"><p>ライブラリ</p></td>
<td align="left">Hbaapi .lib</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[HBA\_の状態](hba-status.md)

[**GetFcpTargetMapping\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getfcptargetmapping_in)

[**GetFcpTargetMapping\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getfcptargetmapping_out)

 

 






