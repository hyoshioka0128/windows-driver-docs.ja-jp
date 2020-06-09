---
title: バグチェック 0xD4 SYSTEM_SCAN_AT_RAISED_IRQL_CAUGHT_IMPROPER_DRIVER_UNLOAD
description: SYSTEM_SCAN_AT_RAISED_IRQL_CAUGHT_IMPROPER_DRIVER_UNLOAD バグチェックの値は0x000000D4 です。 これは、ドライバーがアンロード前に保留中の操作をキャンセルしなかったことを示します。
ms.assetid: 4c0e69d1-737c-4dd7-b52a-4cd5eeadcbb9
keywords:
- バグチェック 0xD4 SYSTEM_SCAN_AT_RAISED_IRQL_CAUGHT_IMPROPER_DRIVER_UNLOAD
- SYSTEM_SCAN_AT_RAISED_IRQL_CAUGHT_IMPROPER_DRIVER_UNLOAD
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- SYSTEM_SCAN_AT_RAISED_IRQL_CAUGHT_IMPROPER_DRIVER_UNLOAD
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 80f123048cf7401d5631084a5c9a7822b8cff495
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534567"
---
# <a name="bug-check-0xd4-system_scan_at_raised_irql_caught_improper_driver_unload"></a>バグチェック 0xD4: 発生した \_ \_ IRQL のシステムスキャンで、不適切な \_ ドライバーの \_ \_ \_ \_ \_ アンロードが検出されました


\_ \_ \_ \_ \_ \_ 不適切 \_ \_ なドライバーのアンロードのバグチェックでシステムスキャンが発生したときに、0x000000D4 の値が指定されています。 これは、ドライバーがアンロード前に保留中の操作をキャンセルしなかったことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。


## <a name="system_scan_at_raised_irql_caught_improper_driver_unload-parameters"></a>発生した \_ \_ IRQL のシステムスキャンで、不適切な \_ ドライバーの \_ \_ \_ \_ \_ アンロードパラメーターが検出されました


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>参照されるメモリ</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>参照時の IRQL</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p><strong>0:</strong>込ん</p>
<p><strong>1:</strong>企画</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>参照されたメモリのアドレス</p></td>
</tr>
</tbody>
</table>

 

エラーの原因となっているドライバーを識別できる場合は、その名前が青色の画面に出力され、メモリ内の場所 (PUNICODE \_ 文字列) **KiBugCheckDriver**に格納されます。

<a name="cause"></a>原因
-----

このドライバーは、アンロードの前に、ルックアサイドリスト、Dpc、ワーカースレッド、またはその他の項目をキャンセルできませんでした。 その後、システムは、発生した IRQL でドライバーの以前の場所にアクセスしようとしました。

<a name="resolution"></a>解像度
----------

デバッグを開始するには、カーネルデバッガーを使用してスタックトレースを取得します。この拡張機能で[**は、バグ**](-analyze.md)チェックに関する情報を表示し、根本原因を特定し、 [**Kb (スタックバックトレースの表示)**](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)コマンドを使用してスタックトレースを取得します。 エラーの原因となったドライバーが特定されている場合は、ドライバー検証ツールをアクティブ化し、このバグのレプリケートを試みます。

[ドライバーの検証](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)機能の詳細については、「Windows driver Kit」を参照してください。

 

 




