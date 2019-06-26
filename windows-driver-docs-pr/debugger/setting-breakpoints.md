---
title: ブレークポイントの設定
description: ブレークポイントの設定
ms.assetid: 9715c35a-0c8c-4e89-be28-2899f21ec964
keywords:
- デバッガーのブレークポイントの設定、エンジンの API
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 348b921af971f02cb4ab56d40dc9aaeb807ceb29
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366394"
---
# <a name="setting-breakpoints"></a>ブレークポイントの設定


## <span id="ddk_using_breakpoints_dbx"></span><span id="DDK_USING_BREAKPOINTS_DBX"></span>


ブレークポイントが作成されると、 [ **AddBreakpoint** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-addbreakpoint)メソッド。 このメソッドを作成、 [IDebugBreakpoint](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nn-dbgeng-idebugbreakpoint)ブレークポイントを表すオブジェクト。 設定も、*ブレークポイント タイプ*(ソフトウェアのブレークポイントまたはプロセッサ ブレークポイント)。 ブレークポイントが作成されたら、その型を変更できません。

ブレークポイントが削除されると、 [ **RemoveBreakpoint** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-removebreakpoint)メソッド。 これは、削除されますが、 **IDebugBreakpoint**オブジェクト。 このオブジェクトもう一度使用することはできません。

**注**  が**IDebugBreakpoint**実装、 **IUnknown**インターフェイス、メソッド**iunknown::addref**と **:Release**ブレークポイントの有効期間を制御するには使用されません。 これらのメソッドは、ブレークポイントの有効期間に影響を与えるありません。 代わりに、 **IDebugBreakpoint**メソッドの後にオブジェクトが削除される[ **RemoveBreakpoint** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-removebreakpoint)が呼び出されます。

 

一意な指定はブレークポイントの作成時に*ブレークポイント ID*します。 この識別子は変更されません。 ただし、ブレークポイントが削除されると、その ID は別のブレークポイントの使用可能性があります。 ブレークポイントの削除の通知を受け取る方法の詳細については、次を参照してください。[監視イベント](monitoring-events.md)します。

ブレークポイントの作成時に最初に無効です。つまり、実行を停止するターゲットは発生しません。 メソッドを使用して、このブレークポイントを有効にすることがあります[ **AddFlags** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugbreakpoint2-addflags) 、デバッグを追加する\_ブレークポイント\_ENABLED フラグ。

ブレークポイントが作成されると、0x00000000 に関連付けられているメモリ位置があります。 使用して、場所を変更する[ **SetOffset** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugbreakpoint2-setoffset) 、アドレス、またはを使用して[ **SetOffsetExpression** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugbreakpoint2-setoffsetexpression)シンボリック式. される前に、その初期値から、ブレークポイントの場所を変更する必要があります。

 

 





