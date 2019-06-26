---
title: VERIFY_IS_IRQL_PASSIVE_LEVEL マクロ
description: VERIFY_IS_IRQL_PASSIVE_LEVEL マクロは、IRQL PASSIVE_LEVEL では、ドライバーが実行されていない場合、カーネル デバッガーを中断します。
ms.assetid: 7f1e25af-df66-46a2-8d27-7924677e4d5d
keywords:
- VERIFY_IS_IRQL_PASSIVE_LEVEL マクロ
ms.date: 08/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0c8e51cd166ee5c3156c52cdede3d6cac60bcb33
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372145"
---
# <a name="verifyisirqlpassivelevel-macro"></a>VERIFY_IS_IRQL_PASSIVE_LEVEL マクロ


[KMDF にのみ適用されます]

**VERIFY_IS_IRQL_PASSIVE_LEVEL** IRQL では、ドライバーが実行されていない場合に、マクロがカーネル デバッガーを中断 PASSIVE_LEVEL を = です。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
VOID VERIFY_IS_IRQL_PASSIVE_LEVEL(void);
```

<a name="parameters"></a>パラメーター
----------

このマクロには、パラメーターがありません。

<a name="return-value"></a>戻り値
------------

なし

<a name="remarks"></a>注釈
-------

コードを**VERIFY_IS_IRQL_PASSIVE_LEVEL**リリース構成またはデバッグ構成で、ドライバーをビルドするときに、ドライバーのバイナリにマクロが含まれます。 場合は、ドライバーのバイナリが含まれています。 **VERIFY_IS_IRQL_PASSIVE_LEVEL**コード、コードはチェック ビルドまたは Microsoft Windows オペレーティング システムのビルドでは、ドライバーが実行される場合に実行されます。

**VERIFY_IS_IRQL_PASSIVE_LEVEL**コードにカーネル デバッガーでは、次のいずれかが true の場合。

-   **DbgBreakOnError**レジストリに 0 以外の値に設定されます。
-   **VerifierOn** 0 以外の値に設定されていると**DbgBreakOnError**が設定されていません。
-   ドライバーの検証が有効になっている、ドライバーは、フレームワーク バージョン 1.9 以降でビルドされたあり**VerifierOn**も**DbgBreakOnError**設定されます。

ドライバーをデバッグする際のレジストリ エントリの詳細については、次を参照してください。 [Debugging Framework-Based ドライバーのレジストリ エントリ](https://docs.microsoft.com/windows-hardware/drivers/wdf/registry-values-for-debugging-kmdf-drivers)します。

ドライバーのデバッグの詳細については、次を参照してください。 [KMDF ドライバーをデバッグ](https://docs.microsoft.com/windows-hardware/drivers/wdf/debugging-a-wdf-driver)します。

<a name="examples"></a>例
--------

次のコード例は、IRQL では、ドライバーが実行されていない場合は、カーネル デバッガーを中断 PASSIVE_LEVEL を = です。

```cpp
VERIFY_IS_IRQL_PASSIVE_LEVEL();
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


[**WDFVERIFY**](wdfverify.md)
