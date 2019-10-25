---
title: WdbgExts のターゲット情報
description: WdbgExts のターゲット情報
ms.assetid: 70b26047-2f3a-4d35-861f-a9ca17d1d5f9
keywords:
- WdbgExts 拡張機能、ターゲット
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: eae7908748b84fec52256707293aae253e72aaa3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834171"
---
# <a name="wdbgexts-target-information"></a>WdbgExts のターゲット情報


ターゲットがメモリアドレスに32ビットまたは64ビットのポインターを使用しているかどうかを判断するには、 [**IsPtr64**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-isptr64)関数を使用します。

ターゲットのオペレーティングシステムの詳細については、「[**カーネル\_の\_のバージョンを取得\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_dbgkd_get_version64)には、 [**Ioctl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nc-wdbgexts-pwindbg_ioctl_routine)操作 IG を使用します。 ターゲット上のプロセッサの合計数を取得し、現在のプロセッサを検出するには、関数[**GetKdContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-getkdcontext)を使用します。

[**Getdebugger data**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-getdebuggerdata)関数は、KDDEBUGGER\_DATA64 または KDDEBUGGER\_DATA32 構造体を返します。この構造には、現在のセッション中に[デバッガーエンジン](introduction.md#debugger-engine)によってクエリまたは特定されたターゲットに関する情報が含まれています。 この情報には、特定のキーターゲットの場所と特定の状態の値が含まれます。

デバッガーは、ターゲットから取得した情報をキャッシュします。 関数[**Getデバッガ cachesize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-getdebuggercachesize)は、このキャッシュのサイズを返します。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

より強力なターゲット API については、このドキュメントの「[デバッガーエンジン API の使用](using-the-debugger-engine-api.md)」セクションの「[ターゲット情報](target-information.md)」を参照してください。

 

 





