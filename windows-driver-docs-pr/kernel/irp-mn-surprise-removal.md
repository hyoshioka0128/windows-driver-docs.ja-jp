---
title: IRP_MN_SURPRISE_REMOVAL
description: すべての PnP ドライバーでは、この IRP を処理する必要があります。
ms.date: 08/12/2017
ms.assetid: 19d6847c-6b64-4552-b8b8-fef1d9b13fc7
keywords:
- IRP_MN_SURPRISE_REMOVAL Kernel-Mode Driver Architecture
ms.localizationpriority: medium
ms.openlocfilehash: fb0889a768a4593e713ac9489471c4b6794590fc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556540"
---
# <a name="irpmnsurpriseremoval"></a>IRP\_MN\_SURPRISE\_REMOVAL


すべての PnP ドライバーでは、この IRP を処理する必要があります。

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_PNP** ](irp-mj-pnp.md)送信されるときに
---------

PnP マネージャーでは、この IRP に、デバイスの I/O 操作に使用できるがなくなったことをデバイスのドライバーに通知を送信します。 Windows 2000 以降のシステムだけでは、この IRP が送信されます。

PnP マネージャーは、ユーザー モード アプリケーションやその他のカーネル モード コンポーネントに通知する前に、この IRP を送信します。 この IRP の完了後、PnP マネージャーに通知登録済みのアプリケーションとドライバー デバイスが削除されています。

PnP マネージャーは、この IRP を送信するとき、デバイスは、PnP 状態にできます。

Windows 98/Windows Me で PnP マネージャーでは、この IRP は送信しません。

PnP マネージャー IRQL でこの IRP の送信 = パッシブ\_システム スレッドのコンテキスト内のレベル。

## <a name="input-parameters"></a>入力パラメーター


なし

## <a name="output-parameters"></a>出力パラメーター


なし

## <a name="io-status-block"></a>I/O ステータス ブロック


ドライバーを設定する必要があります**Irp -&gt;IoStatus.Status**ステータス\_成功します。 ドライバーでは、この IRP が失敗する必要があります。

<a name="operation"></a>操作
---------

この IRP では、デバイス スタックの上部にあるドライバーによって最初に処理され、各スタックの下位のドライバーに渡されます。

この IRP の詳細については、次を参照してください。 [IRP の処理\_MN\_突然\_削除要求](https://msdn.microsoft.com/library/windows/hardware/ff546699)します。 デバイスの削除のサポートに関する詳細については、次を参照してください。[デバイスを削除する](https://msdn.microsoft.com/library/windows/hardware/ff561046)します。

**この IRP を送信します。**

システムの使用に予約されています。 ドライバーは、この IRP を送信する必要があります。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Wdm.h (Wdm.h、Ntddk.h、Ntifs.h など)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**IRP\_MN\_REMOVE\_DEVICE**](irp-mn-remove-device.md)

 

 




