---
title: 複数ヘッド メモリの管理
description: 複数ヘッド メモリの管理
ms.assetid: 37cda124-0c3b-4af4-92b8-329440dd3221
keywords:
- 複数ヘッド ハードウェア WDK DirectX 9.0、メモリ管理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 94d2aec2bdc0b50e048b4bcfc038b44cde400241
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579672"
---
# <a name="managing-multiple-head-memory"></a>複数ヘッド メモリの管理


## <span id="ddk_managing_multiple_head_memory_gg"></span><span id="DDK_MANAGING_MULTIPLE_HEAD_MEMORY_GG"></span>


設定、DDSCAPS2\_ADDITIONALPRIMARY 機能ビット、 **dwCaps2**のメンバー、 [ **DDSCAPS2** ](https://msdn.microsoft.com/library/windows/hardware/ff550292)それぞれの面では従属要素の構造ヘッドは、そのようなサーフェイスがその先頭に割り当てられているビデオ メモリから割り当てられている最後のサーフェスをヘッドを通知します。 下位の head が保証されるため受信しなかったこと以降、下位の head は master head ビデオ メモリの割り当ての制御を放棄しする必要があります[ *DdCreateSurface* ](https://msdn.microsoft.com/library/windows/hardware/ff549263)、アプリケーションの有効期間を呼び出します。

ドライバーでは、master head が下位ヘッドに関連付けられているメモリを割り当てることができませんでことを確認する必要があります。

共通言語ランタイムは、ドライバーの[ *DdDestroySurface* ](https://msdn.microsoft.com/library/windows/hardware/ff549281)を下位の頭のサーフェスを破棄する関数、DDSCAPS2\_ADDITIONALPRIMARY 機能ビットが設定、ドライバー下位の先頭が、もう一度は、ビデオ メモリ管理の管理に通知されます。

ほとんどの場合、ビデオ メモリは既存の DirectDraw プロセスに固有の head この選択を所有します。 具体的には、次のとおりです。

-   ランタイムを保証する以降の割り当てを要求せずに下位の後にヘッドが行われる*DdCreateSurface* 、DDSCAPS2 を使用して呼び出しが行われる\_ADDITIONALPRIMARY ビット。 そのため、ドライバーでは、いつでも独自のビデオ メモリ プールから割り当てを制限する必要はありません。

-   アプリケーションが終了するか最小限に抑える、すべてのサーフェイスが破棄されます。 そのため、下位の頭のプールからの master head によって作成されたすべてのテクスチャがクリーンアップされます。

-   場合、DDSCAPS2\_下位ヘッドは、上のサーフェス ADDITIONALPRIMARY ビットが設定されていない後はこれらのヘッドを続ける場合スタンドアロンのヘッドと同様に、ビデオ メモリを割り当てられません。 実際には、このような下位ヘッドは、その他のアダプターの複数のモニター機能と同じです。

-   ドライバーは、master head が下位ヘッドのプールから特定のリソースを割り当てられることができる場合に関する決定をなど、下位の頭のプールからメモリを割り当てます実装を提供する必要があります。 Master head 複数ヘッド シナリオに関与しているかどうかに関する情報自体にないことに注意してください。 マスターで使用できるプールがかどうかこれらヘッドのいずれかを判断するには、そのグループ内の下位のすべてのヘッドを走査する必要があります、独自のビデオ メモリ不足、master head を実行すると (つまり、下位の頭のいずれかを判断する受信*DdCreateSurface* 、DDSCAPS2 で呼び出しを\_ADDITIONALPRIMARY ビットが設定)。

-   最後に、ランタイムは、グループ内のすべてのヘッドが複数ヘッドのシナリオに含めることが保証されますに注意してください。 したがって、ドライバーは、複数ヘッド モードで現在があるかどうかを示す状態の 1 つのビットをのみ維持する必要があります。

 

 





