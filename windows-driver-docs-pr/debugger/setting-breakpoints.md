---
title: ブレークポイントの設定
description: ブレークポイントの設定
ms.assetid: 9715c35a-0c8c-4e89-be28-2899f21ec964
keywords:
- デバッガーのブレークポイントの設定、エンジンの API
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 494d8a3e8cd043e31c5cd526dda627439f006342
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63381960"
---
# <a name="setting-breakpoints"></a>ブレークポイントの設定


## <span id="ddk_using_breakpoints_dbx"></span><span id="DDK_USING_BREAKPOINTS_DBX"></span>


ブレークポイントが作成されると、 [ **AddBreakpoint** ](https://msdn.microsoft.com/library/windows/hardware/ff537856)メソッド。 このメソッドを作成、 [IDebugBreakpoint](https://msdn.microsoft.com/library/windows/hardware/ff549812)ブレークポイントを表すオブジェクト。 設定も、*ブレークポイント タイプ*(ソフトウェアのブレークポイントまたはプロセッサ ブレークポイント)。 ブレークポイントが作成されたら、その型を変更できません。

ブレークポイントが削除されると、 [ **RemoveBreakpoint** ](https://msdn.microsoft.com/library/windows/hardware/ff554487)メソッド。 これは、削除されますが、 **IDebugBreakpoint**オブジェクト。 このオブジェクトもう一度使用することはできません。

**注**  が**IDebugBreakpoint**実装、 **IUnknown**インターフェイス、メソッド**iunknown::addref**と **:Release**ブレークポイントの有効期間を制御するには使用されません。 これらのメソッドは、ブレークポイントの有効期間に影響を与えるありません。 代わりに、 **IDebugBreakpoint**メソッドの後にオブジェクトが削除される[ **RemoveBreakpoint** ](https://msdn.microsoft.com/library/windows/hardware/ff554487)が呼び出されます。

 

一意な指定はブレークポイントの作成時に*ブレークポイント ID*します。 この識別子は変更されません。 ただし、ブレークポイントが削除されると、その ID は別のブレークポイントの使用可能性があります。 ブレークポイントの削除の通知を受け取る方法の詳細については、次を参照してください。[監視イベント](monitoring-events.md)します。

ブレークポイントの作成時に最初に無効です。つまり、実行を停止するターゲットは発生しません。 メソッドを使用して、このブレークポイントを有効にすることがあります[ **AddFlags** ](https://msdn.microsoft.com/library/windows/hardware/ff537903) 、デバッグを追加する\_ブレークポイント\_ENABLED フラグ。

ブレークポイントが作成されると、0x00000000 に関連付けられているメモリ位置があります。 使用して、場所を変更する[ **SetOffset** ](https://msdn.microsoft.com/library/windows/hardware/ff556741) 、アドレス、またはを使用して[ **SetOffsetExpression** ](https://msdn.microsoft.com/library/windows/hardware/ff556745)シンボリック式. される前に、その初期値から、ブレークポイントの場所を変更する必要があります。

 

 





