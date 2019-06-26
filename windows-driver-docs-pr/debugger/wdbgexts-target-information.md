---
title: WdbgExts のターゲット情報
description: WdbgExts のターゲット情報
ms.assetid: 70b26047-2f3a-4d35-861f-a9ca17d1d5f9
keywords:
- WdbgExts 拡張機能します。
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6bfddb923f583615f4f929a042ab0d752cd6caa6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369424"
---
# <a name="wdbgexts-target-information"></a>WdbgExts のターゲット情報


ターゲットがメモリ アドレスの 32 ビットまたは 64 ビットのポインターを使用するかどうかを判断する関数を使用して[ **IsPtr64**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nf-wdbgexts-isptr64)します。

については、ターゲットのオペレーティング システムを使用、 [ **Ioctl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nc-wdbgexts-pwindbg_ioctl_routine)操作[ **IG\_取得\_カーネル\_バージョン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/ns-wdbgexts-_dbgkd_get_version64). 現在のプロセッサは、どれをご確認ください、ターゲットでプロセッサの合計数を取得する、関数を使用して[ **GetKdContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nf-wdbgexts-getkdcontext)します。

[ **GetDebuggerData** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nf-wdbgexts-getdebuggerdata)返します、KDDEBUGGER\_DATA64 または KDDEBUGGER\_ターゲットに関する情報を含む DATA32 構造体を[デバッガー エンジン](introduction.md#debugger-engine)がクエリを実行したり、現在のセッション時に決定されます。 この情報には、特定のキーのターゲットの場所と特定の状態の値が含まれています。

デバッガーでは、ターゲットから取得したいくつかの情報をキャッシュします。 関数は、 [ **GetDebuggerCacheSize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nf-wdbgexts-getdebuggercachesize)はこのキャッシュのサイズを返します。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

強力なターゲット API を参照してください。[ターゲット情報](target-information.md)で、[デバッガー エンジン API を使用して](using-the-debugger-engine-api.md)このドキュメントの「します。

 

 





