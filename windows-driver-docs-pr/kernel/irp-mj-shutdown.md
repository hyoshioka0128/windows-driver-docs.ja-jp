---
title: IRP_MJ_SHUTDOWN
description: データの内部キャッシュがある大容量記憶装置のドライバーでは、DispatchShutdown ルーチンでは、この要求を処理する必要があります。
ms.date: 08/12/2017
ms.assetid: af0b01b5-5f81-42da-aa4b-433bd422a51f
keywords:
- IRP_MJ_SHUTDOWN カーネル モード ドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: 20459241f40f4000dc16933a0d3e562424847af8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382253"
---
# <a name="irpmjshutdown"></a>IRP\_MJ\_シャット ダウン


データでこの要求を処理する必要がありますの内部キャッシュがある大容量記憶装置のドライバーを[ *DispatchShutdown* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチン。 大容量記憶装置のドライバーと上層にあるそれらの中間ドライバーを基になるドライバーには、データの内部バッファーが保持している場合この要求処理する必要がありますもします。

<a name="when-sent"></a>送信時
---------

シャット ダウン要求を受信するには、ファイル システム ドライバーが、システムがシャット ダウンされている通知を送信していることを示します。

1 つまたは複数のファイル システム ドライバーまたは送信できます下位レベルのドライバーは、複数のシャット ダウン要求ユーザーがログオフしたときに、システムが何らかの理由でシャット ダウンされています。

## <a name="input-parameters"></a>入力パラメーター


なし

## <a name="output-parameters"></a>出力パラメーター


なし

<a name="operation"></a>操作
---------

ドライバーは、現在、デバイスにキャッシュされているか、シャット ダウン要求を完了する前に、ドライバーの内部バッファーに保持されているすべてのデータの転送を完了する必要があります。

ドライバーは受信しません、 **IRP\_MJ\_シャット ダウン**いずれかに関係するために登録しない限り、デバイス オブジェクトの要求[ **IoRegisterShutdownNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioregistershutdownnotification)または[ **IoRegisterLastChanceShutdownNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioregisterlastchanceshutdownnotification)します。

<a name="requirements"></a>必要条件
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


[*DispatchShutdown*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)

[**IoRegisterLastChanceShutdownNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioregisterlastchanceshutdownnotification)

[**IoRegisterShutdownNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioregistershutdownnotification)

 

 




