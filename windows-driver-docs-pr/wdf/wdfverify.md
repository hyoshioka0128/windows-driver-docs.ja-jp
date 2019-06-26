---
title: WDFVERIFY マクロ
description: WDFVERIFY マクロでは、論理式をテストし、式が FALSE に評価される場合は、カーネル デバッガーを中断します。
ms.assetid: 9dc19299-7eda-42fb-811e-ba8dc5c1cdb5
keywords:
- WDFVERIFY マクロ
ms.date: 08/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: eec94b8472a09f64dba592a46cc7768a72149cbd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354431"
---
# <a name="wdfverify-macro"></a>WDFVERIFY マクロ


\[KMDF にのみ適用されます。\]

**WDFVERIFY**マクロ論理式をテストして、式の評価が**FALSE**、カーネル デバッガーを中断します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
VOID WDFVERIFY(
    exp
);
```

<a name="parameters"></a>パラメーター
----------

*exp 関数*   
WDFVERIFY をテストする論理式。

<a name="return-value"></a>戻り値
------------

なし

<a name="remarks"></a>注釈
-------

コードを**WDFVERIFY**リリース構成またはデバッグ構成で、ドライバーをビルドするときに、ドライバーのバイナリにマクロが含まれます。 場合は、ドライバーのバイナリが含まれています。 **WDFVERIFY**コード、コードはチェック ビルドまたは Microsoft Windows オペレーティング システムのビルドでは、ドライバーが実行される場合に実行されます。

**WDFVERIFY**場合のみカーネル デバッガーにコードでは、 **VerifyOn**レジストリの値を設定します。 ドライバーをデバッグする際のレジストリ エントリの詳細については、次を参照してください。 [Debugging Framework-Based ドライバーのレジストリ エントリ](https://docs.microsoft.com/windows-hardware/drivers/wdf/registry-values-for-debugging-kmdf-drivers)します。

ドライバーのデバッグの詳細については、次を参照してください。 [KMDF ドライバーをデバッグ](https://docs.microsoft.com/windows-hardware/drivers/wdf/debugging-a-wdf-driver)します。

<a name="examples"></a>例
--------

次のコード例は、要求オブジェクトを再利用失敗した場合、デバッガーを中断します。

```cpp
status = WdfRequestReuse(Request, &params);
WDFVERIFY(NT_SUCCESS(status));
```

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>対象プラットフォーム</p></td>
<td><a href="https://go.microsoft.com/fwlink/p/?linkid=531356" data-raw-source="[Universal](https://go.microsoft.com/fwlink/p/?linkid=531356)">ユニバーサル</a></td>
</tr>
<tr class="even">
<td><p>最小 KMDF バージョン</p></td>
<td><p>1.0</p></td>
</tr>
<tr class="odd">
<td><p>Header</p></td>
<td>Wdfassert.h (Wdf.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**VERIFY_IS_IRQL_PASSIVE_LEVEL**](verify-is-irql-passive-level.md)

 

 






