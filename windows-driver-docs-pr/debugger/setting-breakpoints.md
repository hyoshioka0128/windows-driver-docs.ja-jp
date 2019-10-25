---
title: ブレークポイントの設定
description: ブレークポイントの設定
ms.assetid: 9715c35a-0c8c-4e89-be28-2899f21ec964
keywords:
- デバッガーエンジン API, ブレークポイントの設定
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 631649233cdaf864191cf58d2cbaef1639683235
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838817"
---
# <a name="setting-breakpoints"></a>ブレークポイントの設定


## <span id="ddk_using_breakpoints_dbx"></span><span id="DDK_USING_BREAKPOINTS_DBX"></span>


ブレークポイントは、 [**Addbreakpoint**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-addbreakpoint)ポイントメソッドを使用して作成されます。 このメソッドは、ブレークポイントを表す[IDebugBreakpoint](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugbreakpoint)オブジェクトを作成します。 また、*ブレークポイントの種類*(ソフトウェアブレークポイントまたはプロセッサのブレークポイント) も設定します。 ブレークポイントが作成されると、その型を変更することはできません。

ブレークポイントは[**Removebreakpoint**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-removebreakpoint)ポイントメソッドを使用して削除されます。 これにより、 **IDebugBreakpoint**オブジェクトも削除されます。このオブジェクトを再度使用することはできません。

**注**   **IDebugBreakpoint**は**iunknown**インターフェイスを実装していますが、 **iunknown:: AddRef**メソッドと**iunknown:: Release**メソッドは、ブレークポイントの有効期間の制御には使用されません。 これらのメソッドは、ブレークポイントの有効期間には影響しません。 代わりに、 **IDebugBreakpoint**オブジェクトは、 [**removebreakpoint ポイント**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-removebreakpoint)が呼び出された後に削除されます。

 

ブレークポイントが作成されると、一意の*ブレークポイント ID*が付与されます。 この識別子は変更されません。 ただし、ブレークポイントが削除された後は、その ID を別のブレークポイントに使用することができます。 ブレークポイントの削除の通知を受信する方法の詳細については、「[イベントの監視](monitoring-events.md)」を参照してください。

ブレークポイントが作成されると、最初は無効になります。これは、ターゲットの実行が停止されないことを意味します。 このブレークポイントは、 [**Addflags**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugbreakpoint2-addflags)メソッドを使用して、デバッグ\_ブレークポイント\_有効フラグを追加することによって有効にすることができます。

最初に作成されたブレークポイントには、メモリ位置0x00000000 が関連付けられています。 場所を変更するには、 [**SetOffset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugbreakpoint2-setoffset)をアドレスと共に使用するか、または[**Setoffsetexpression**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugbreakpoint2-setoffsetexpression)とシンボリック式を使用します。 ブレークポイントの場所は、使用前に初期値から変更する必要があります。

 

 





