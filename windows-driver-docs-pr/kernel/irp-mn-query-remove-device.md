---
title: IRP_MN_QUERY_REMOVE_DEVICE
description: すべての PnP ドライバーは、この IRP を処理する必要があります。
ms.date: 08/12/2017
ms.assetid: 95ec9ed8-014f-4d01-bed7-3aeb29cd9e73
keywords:
- IRP_MN_QUERY_REMOVE_DEVICE カーネルモードドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: 60ee3539877e440b40533b3a97fe0510bbeedaaa
ms.sourcegitcommit: 7681ac46c42782602bd3449d61f7ed4870ef3ba7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82922599"
---
# <a name="irp_mn_query_remove_device"></a>IRP\_を\_実行\_する\_クエリデバイスの削除


すべての PnP ドライバーは、この IRP を処理する必要があります。

## <a name="value"></a>値

0x01

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_PNP**](irp-mj-pnp.md)

<a name="when-sent"></a>送信時
---------

PnP マネージャーは、この IRP を送信して、デバイスがコンピューターから削除されようとしていること、およびコンピューターを中断せずにデバイスを削除できるかどうかを問い合わせます。 また、この IRP は、ユーザーがデバイスのドライバーを更新するように要求した場合にも送信されます。

PnP マネージャーは、システムスレッドのコンテキストで\_この IRP を IRQL パッシブレベルで送信します。

## <a name="input-parameters"></a>入力パラメーター


None

## <a name="output-parameters"></a>出力パラメーター


None

## <a name="io-status-block"></a>I/O ステータス ブロック


ドライバーは、 **Irp-&gt;iostatus**を、status が\_SUCCESS に設定されているか、状態\_が "失敗" などの適切なエラー状態に設定されています。

<a name="operation"></a>Operation
---------

この IRP は、デバイススタックの一番上にあるドライバーによって最初に処理され、スタック内の下位の各ドライバーに渡されます。

この IRP に応答して、ドライバーは、コンピューターを邪魔せずにデバイスを削除できるかどうかを示します。

この IRP の処理の詳細については、次を参照してください。 [irp\_を処理する\_クエリ\_を処理するデバイス要求を削除\_](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-an-irp-mn-query-remove-device-request)します。 デバイスの削除に関する一般的な情報については、「[デバイスの削除](https://docs.microsoft.com/windows-hardware/drivers/kernel/removing-a-device)」を参照してください。

**この IRP を送信しています**

システムで使用するために予約されています。 ドライバーは、この IRP を送信することはできません。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>ヘッダー</p></td>
<td>Wdm.h (Wdm.h、Ntddk.h、Ntifs.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**\_IRP\_を終了\_する\_デバイスの削除**](irp-mn-cancel-remove-device.md)

[**IRP\_\_デバイス\_使用量\_の通知**](irp-mn-device-usage-notification.md)

[**IRP\_の\_すべて\_のデバイスの削除**](irp-mn-remove-device.md)

 

 




