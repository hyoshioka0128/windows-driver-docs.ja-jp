---
title: 非ローカルの表示メモリでのテクスチャの並べ替え
description: 非ローカルの表示メモリでのテクスチャの並べ替え
ms.assetid: b4b4c478-7034-4ff9-8cb2-f86baffd89f7
keywords:
- 表示メモリ WDK DirectDraw、テクスチャの並べ替え
- 非ローカルの表示メモリ WDK DirectDraw、テクスチャの並べ替え
- AGP WDK DirectDraw、テクスチャの並べ替え
- 描画 AGP WDK DirectDraw、テクスチャの並べ替えのサポート
- DirectDraw AGP サポート WDK Windows 2000 の表示、テクスチャの並べ替え
- メモリ WDK DirectDraw AGP、テクスチャの並べ替え
- WDK DirectDraw のテクスチャの並べ替え
- DDCAPS2_SYSTONONLOCAL_AS_SYSTOLOCAL
- WDK DirectDraw、テクスチャの並べ替え
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2aa00b6d62d35b903117d0420a3cb49fbb329cd5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376129"
---
# <a name="reordering-textures-in-nonlocal-display-memory"></a>非ローカルの表示メモリでのテクスチャの並べ替え


## <span id="ddk_reordering_textures_in_nonlocal_display_memory_gg"></span><span id="DDK_REORDERING_TEXTURES_IN_NONLOCAL_DISPLAY_MEMORY_GG"></span>


ドライバー開発者可能性がありますをより効率的なテクスチャの管理を許可する AGP メモリにテクスチャを並べ替えるには必要な特別な場合があります。 DDCAPS2\_SYSTONONLOCAL\_AS\_SYSTOLOCAL フラグは、ドライバーがすべて同じに対して指定されている上限を使用して、非ローカルのビデオ メモリをサーフェス (サーフェスのシステム メモリのコピー) をバックアップから blt をサポートできることを通知ローカルのビデオ メモリ blt 表面のメモリにバックアップします。

DDCAPS2\_SYSTONONLOCAL\_AS\_SYSTOLOCAL フラグが有効な場合にのみ、DDCAPS2\_NONLOCALVIDMEMCAPS フラグを設定します。 場合 DDCAPS2\_SYSTONONLOCAL\_AS\_SYSTOLOCAL が、セット、DDCAPS\_ドライバーによって CANBLTSYSMEM フラグを設定する必要があり、すべての関連するバッキング サーフェス blt 上限は適切である必要があります。 DDCAPS2\_SYSTONONLOCAL\_AS\_SYSTOLOCAL ことを示す、バッキング画面ビデオ メモリの DDCAPS blt キャップは表面にビデオ メモリの非ローカル blt バックアップにも適用されます。 たとえば、 **dwSVBCaps**、 **dwSVBCKeyCaps**、 **dwSVBFXCaps**、および**dwSVBRops**のメンバー、 [ **DDCORECAPS** ](https://docs.microsoft.com/windows/desktop/api/ddrawi/ns-ddrawi-_ddcorecaps)構造が正しく入力すると見なされます。 これらの caps ビットと一致する非ローカル メモリにバッキング画面から、blt は、ドライバーに渡されます。

**注**  自体のテクスチャの効率的な並べ替えを行うドライバーを有効にするこの機能が対象としています。 これは*いない*AGP メモリにハードウェアを記述できることを意味するものです。 ハードウェア AGP メモリに直接書き込むことは現在サポートされていません。

 

 

 





