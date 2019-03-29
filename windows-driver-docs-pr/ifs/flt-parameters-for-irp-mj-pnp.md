---
title: FLT_PARAMETERS IRP_MJ_PNP 共用体
description: 共用体のコンポーネントで使用されるときに、FLT の MajorFunction フィールド\_IO\_パラメーター\_操作のブロック構造は IRP\_MJ\_PNP します。
ms.assetid: d3ce893b-f113-4c50-8f52-30c7ced25ae0
keywords:
- FLT_PARAMETERS IRP_MJ_PNP 共用体インストール可能なファイル システム ドライバー
- FLT_PARAMETERS union インストール可能なファイル システム ドライバー
- PFLT_PARAMETERS 共用体ポインター インストール可能なファイル システム ドライバー
topic_type:
- apiref
api_name:
- FLT_PARAMETERS
api_location:
- fltkernel.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f41c12635a72139b79a0376bb01282a102ec709d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570669"
---
# <a name="fltparameters-for-irpmjpnp-union"></a>FLT\_IRP のパラメーター\_MJ\_PNP 共用体


共用体のコンポーネントで使用されるときに、 **MajorFunction**のフィールド、 [ **FLT\_IO\_パラメーター\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff544638)用の構造、操作が[ **IRP\_MJ\_PNP**](irp-mj-pnp.md)します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef union _FLT_PARAMETERS {
  ...   ;
  union {
    struct  StartDevice;
    struct  QueryDeviceRelations;
    struct  QueryInterface;
    struct  DeviceCapabilities;
    struct  FilterResourceRequirements;
    struct  ReadWriteConfig;
    struct  SetLock;
    struct  QueryId;
    struct  QueryDeviceText;
    struct  UsageNotification;
  } Pnp;
  ...   ;
} FLT_PARAMETERS, *PFLT_PARAMETERS;
```

<a name="members"></a>メンバー
-------

**Pnp**  
**StartDevice**  
IRP に使用される共用体のコンポーネント\_MN\_開始\_デバイス操作。 この操作のパラメーターの詳細については、参照のエントリを参照してください。 [ **IRP\_MN\_開始\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/ff551749)します。

**QueryDeviceRelations**  
IRP に使用される共用体のコンポーネント\_MN\_クエリ\_デバイス\_リレーション操作。 この操作のパラメーターの詳細については、参照のエントリを参照してください。 [ **IRP\_MN\_クエリ\_デバイス\_リレーション**](https://msdn.microsoft.com/library/windows/hardware/ff551670)します。

**QueryInterface**  
IRP に使用される共用体のコンポーネント\_MN\_クエリ\_インターフェイス操作です。 この操作のパラメーターの詳細については、参照のエントリを参照してください。 [ **IRP\_MN\_クエリ\_インターフェイス**](https://msdn.microsoft.com/library/windows/hardware/ff551687)します。

**DeviceCapabilities**  
IRP に使用される共用体のコンポーネント\_MN\_クエリ\_機能操作。 この操作のパラメーターの詳細については、参照のエントリを参照してください。 [ **IRP\_MN\_クエリ\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff551664)します。

**FilterResourceRequirements**  
IRP に使用される共用体のコンポーネント\_MN\_フィルター\_リソース\_要件操作。 この操作のパラメーターの詳細については、参照のエントリを参照してください[ **IRP\_MN\_フィルター\_リソース\_要件**](https://msdn.microsoft.com/library/windows/hardware/ff550874).

**ReadWriteConfig**  
IRP に使用される共用体のコンポーネント\_MN\_読み取り\_CONFIG および IRP\_MN\_書き込み\_構成操作。 この操作のパラメーターの詳細については、参照のエントリを参照してください[ **IRP\_MN\_読み取り\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/ff551727)と[ 。**IRP\_MN\_書き込み\_CONFIG**](https://msdn.microsoft.com/library/windows/hardware/ff551769)します。

**SetLock**  
IRP に使用される共用体のコンポーネント\_MN\_設定\_ロック操作。 この操作のパラメーターの詳細については、参照のエントリを参照してください。 [ **IRP\_MN\_設定\_ロック**](https://msdn.microsoft.com/library/windows/hardware/ff551742)します。

**QueryId**  
IRP に使用される共用体のコンポーネント\_MN\_クエリ\_操作の ID。 この操作のパラメーターの詳細については、参照のエントリを参照してください。 [ **IRP\_MN\_クエリ\_ID**](https://msdn.microsoft.com/library/windows/hardware/ff551679)します。

**QueryDeviceText**  
IRP に使用される共用体のコンポーネント\_MN\_クエリ\_デバイス\_テキスト操作。 この操作のパラメーターの詳細については、参照のエントリを参照してください。 [ **IRP\_MN\_クエリ\_デバイス\_テキスト**](https://msdn.microsoft.com/library/windows/hardware/ff551674)します。

**UsageNotification**  
IRP に使用される共用体のコンポーネント\_MN\_デバイス\_使用状況\_通知操作。 この操作のパラメーターの詳細については、参照のエントリを参照してください[ **IRP\_MN\_デバイス\_使用状況\_通知**](https://msdn.microsoft.com/library/windows/hardware/ff550841) .

<a name="remarks"></a>コメント
-------

[ **FLT\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff544673)の構造体[ **IRP\_MJ\_PNP** ](irp-mj-pnp.md)操作コールバック データによって表される IRP ベース プラグ アンド プレイ (PnP) 操作のパラメーターが含まれています ([**FLT\_コールバック\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff544620)) 構造体。 含まれている、 [ **FLT\_IO\_パラメーター\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff544638)構造体。

IRP\_MJ\_PNP 操作は IRP ベース操作。

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
<td align="left">Fltkernel.h (Fltkernel.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**FLT\_コールバック\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff544620)

[**FLT\_IO\_PARAMETER\_BLOCK**](https://msdn.microsoft.com/library/windows/hardware/ff544638)

[**FLT\_IS\_FASTIO\_OPERATION**](https://msdn.microsoft.com/library/windows/hardware/ff544645)

[**FLT\_IS\_FS\_FILTER\_OPERATION**](https://msdn.microsoft.com/library/windows/hardware/ff544648)

[**FLT\_IS\_IRP\_OPERATION**](https://msdn.microsoft.com/library/windows/hardware/ff544654)

[**FLT\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/ff544673)

[**IRP\_MJ\_PNP**](irp-mj-pnp.md)

[**IRP\_MJ\_PNP (WDK カーネル モード ドライバーのアーキテクチャのリファレンス)**](https://msdn.microsoft.com/library/windows/hardware/ff550772)

[**IRP\_MN\_デバイス\_使用状況\_通知**](https://msdn.microsoft.com/library/windows/hardware/ff550841)

[**IRP\_MN\_フィルター\_リソース\_要件**](https://msdn.microsoft.com/library/windows/hardware/ff550874)

[**IRP\_MN\_クエリ\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff551664)

[**IRP\_MN\_クエリ\_デバイス\_リレーション**](https://msdn.microsoft.com/library/windows/hardware/ff551670)

[**IRP\_MN\_QUERY\_DEVICE\_TEXT**](https://msdn.microsoft.com/library/windows/hardware/ff551674)

[**IRP\_MN\_QUERY\_ID**](https://msdn.microsoft.com/library/windows/hardware/ff551679)

[**IRP\_MN\_クエリ\_インターフェイス**](https://msdn.microsoft.com/library/windows/hardware/ff551687)

[**IRP\_MN\_READ\_CONFIG**](https://msdn.microsoft.com/library/windows/hardware/ff551727)

[**IRP\_MN\_SET\_LOCK**](https://msdn.microsoft.com/library/windows/hardware/ff551742)

[**IRP\_MN\_START\_DEVICE**](https://msdn.microsoft.com/library/windows/hardware/ff551749)

[**IRP\_MN\_WRITE\_CONFIG**](https://msdn.microsoft.com/library/windows/hardware/ff551769)

 

 






