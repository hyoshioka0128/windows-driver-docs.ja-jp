---
title: IRP_MN_SURPRISE_REMOVAL
description: すべての PnP ドライバーは、この IRP を処理する必要があります。
ms.date: 08/12/2017
ms.assetid: 19d6847c-6b64-4552-b8b8-fef1d9b13fc7
keywords:
- IRP_MN_SURPRISE_REMOVAL カーネルモードドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: 29406ccc147c510639ebc87943a31eec165013e4
ms.sourcegitcommit: 7681ac46c42782602bd3449d61f7ed4870ef3ba7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82922553"
---
# <a name="irp_mn_surprise_removal"></a>IRP\_の\_突然\_の削除


すべての PnP ドライバーは、この IRP を処理する必要があります。

## <a name="value"></a>値

0x17

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_PNP**](irp-mj-pnp.md)

<a name="when-sent"></a>送信時
---------

PnP マネージャーは、デバイスが i/o 操作に使用できなくなったことをデバイスに通知するために、この IRP を送信します。 この IRP は、Windows 2000 以降のシステムでのみ送信されます。

PnP マネージャーは、ユーザーモードアプリケーションやその他のカーネルモードコンポーネントに通知する前に、この IRP を送信します。 この IRP が完了すると、デバイスが削除されたことを示す登録済みアプリケーションとドライバーが PnP マネージャーに通知されます。

PnP マネージャーがこの IRP を送信すると、デバイスは任意の PnP 状態になることがあります。

Windows 98/Windows Me では、PnP マネージャーはこの IRP を送信しません。

PnP マネージャーは、システムスレッドのコンテキストでこの\_IRP を IRQL = パッシブレベルで送信します。

## <a name="input-parameters"></a>入力パラメーター


None

## <a name="output-parameters"></a>出力パラメーター


None

## <a name="io-status-block"></a>I/O ステータス ブロック


ドライバーでは、 **Irp-&gt;iostatus**を設定する必要\_があります。状態は SUCCESS に設定されます。 ドライバーは、この IRP を失敗させることはできません。

<a name="operation"></a>Operation
---------

この IRP は、デバイススタックの一番上にあるドライバーによって最初に処理され、スタック内の下位の各ドライバーに渡されます。

この IRP の詳細については、「 [irp\_の\_突然\_の削除要求の処理](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-an-irp-mn-surprise-removal-request)」を参照してください。 デバイスの削除のサポートの詳細については、「[デバイスの削除](https://docs.microsoft.com/windows-hardware/drivers/kernel/removing-a-device)」を参照してください。

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


[**IRP\_の\_すべて\_のデバイスの削除**](irp-mn-remove-device.md)

 

 




