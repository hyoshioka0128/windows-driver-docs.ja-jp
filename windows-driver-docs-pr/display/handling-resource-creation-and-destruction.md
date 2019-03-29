---
title: リソースの作成および破棄の処理
description: リソースの作成および破棄の処理
ms.assetid: d443bdc3-1c5a-4372-9e6a-b8a4d21499b9
keywords:
- WDK の表示のリソースの作成
- リソースの破棄 WDK の表示
- WDK を表示するリソースを破棄します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 356f66e7754a4529630fd121903e67788dadaefd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579231"
---
# <a name="handling-resource-creation-and-destruction"></a>リソースの作成および破棄の処理


Microsoft DirectX のグラフィックスを有効にするには、カーネル サブシステム リソースの有効期間を適切に追跡し、メモリのディスプレイ ドライバーをオペレーティング システム、ユーザー モードでのリークを防ぐためが正しく作成し、リソースを破棄する必要があります。

マイクロソフトの Direct3D ランタイムは、次のユーザー モード ユーザー モードのリソースを作成する、ディスプレイ ドライバー関数を呼び出します。

-   [**CreateResource** ](https://msdn.microsoft.com/library/windows/hardware/ff540688)新しい共有または共有リソースを作成します。

-   [**OpenResource** ](https://msdn.microsoft.com/library/windows/hardware/ff568611)既存の共有リソースへのビューが開きます。

両方の呼び出しでは、Direct3D ランタイム渡します一意*ユーザー モードのランタイム リソース ハンドル*ユーザー モードのディスプレイ ドライバーが、ランタイムにコールバックを使用します。 ときに*CreateResource*または*OpenResource*ユーザー モードのディスプレイ ドライバーは、リソースを表す一意のユーザー モードのハンドルを返しますが正常に返されます。 このハンドルは、*ユーザー モード ドライバー リソース ハンドル*します。 ランタイムは、ドライバーの後続の呼び出しで、ユーザー モード ドライバー リソース ハンドルを使用します。

ユーザー モードのランタイム リソース ハンドルと、ユーザー モード ドライバー リソース ハンドルの間に一対一の対応が存在します。 Direct3D ランタイムとユーザー モード ドライバーの exchange を介して処理するユーザー モードのランタイムとドライバーのリソースを表示、 **hResource**のメンバー、 [ **D3DDDIARG\_CREATERESOURCE** ](https://msdn.microsoft.com/library/windows/hardware/ff542963)と[ **D3DDDIARG\_OPENRESOURCE** ](https://msdn.microsoft.com/library/windows/hardware/ff543232)構造体。

ユーザー モードのディスプレイ ドライバーが Direct3D のランタイムを呼び出すときに[ **pfnAllocateCb** ](https://msdn.microsoft.com/library/windows/hardware/ff568893)ユーザー モード リソースの割り当てを作成する関数をドライバーは、ユーザー モードのランタイム リソースを指定する必要があります処理、 **hResource**のメンバー、 [ **D3DDDICB\_ALLOCATE** ](https://msdn.microsoft.com/library/windows/hardware/ff544137)構造体、 *pData*パラメーターを指します。 Direct3D ランタイムがリソースを識別する一意のカーネル モードのハンドルを生成し、ユーザー モードに渡すことでドライバーを表示する、 **hKMResource** D3DDDICB のメンバー\_割り当て。 ユーザー モードのディスプレイ ドライバーは、後で使用するディスプレイのミニポート ドライバーのコマンドのストリーム内で、カーネル モードのリソース ハンドルを挿入できます。

**注**  ユーザー モード リソース ハンドルは、各ユーザー モード リソースの作成に固有では常に、カーネル モードのリソース ハンドルが常に一意でないです。 Direct3D のランタイムがユーザー モードのディスプレイ ドライバーを呼び出すときに[ **OpenResource** ](https://msdn.microsoft.com/library/windows/hardware/ff568611)関数を既存のビューを開くには共有リソース、ランタイムは、でリソースのカーネルモードのハンドルを渡します**hKMResource**のメンバー、 [ **D3DDDIARG\_OPENRESOURCE** ](https://msdn.microsoft.com/library/windows/hardware/ff543232)構造体、 *pResource*パラメーターポインター。 ランタイムが以前、ランタイムがユーザー モードのディスプレイ ドライバーの呼び出された後にこのカーネル モードのハンドルが作成[ **CreateResource** ](https://msdn.microsoft.com/library/windows/hardware/ff540688)関数。

 

ユーザー モード リソースを破棄する*CreateResource*または*OpenResource* Direct3D ランタイムを作成では、ユーザー モード ドライバー リソース ハンドルを渡します、 *hResource*ユーザー モードのディスプレイ ドライバーの呼び出しでパラメーター [ **DestroyResource** ](https://msdn.microsoft.com/library/windows/hardware/ff552795)関数。 ユーザー モードのディスプレイ ドライバーがユーザー モードのランタイム リソース ハンドルを渡す、カーネル モードのリソース ハンドルとそのすべてのユーザー モード リソースに関連付けられている割り当てを解放する、 **hResource** のメンバー[**D3DDDICB\_DEALLOCATE** ](https://msdn.microsoft.com/library/windows/hardware/ff544161)構造体、 *pData*への呼び出しでパラメーターが指す、 [ *pfnDeallocateCb*](https://msdn.microsoft.com/library/windows/hardware/ff568898)関数。

ユーザー モードのディスプレイ ドライバーが作成し、リソースを破棄するときは、次の項目を考慮してください。

-   共有リソースへの応答でユーザー モードのディスプレイ ドライバーを作成する割り当て (への応答は、 [ **CreateResource** ](https://msdn.microsoft.com/library/windows/hardware/ff540688)を呼び出し、 **SharedResource**ビット フィールドのフラグ設定、**フラグ**のメンバー [ **D3DDDIARG\_CREATERESOURCE**](https://msdn.microsoft.com/library/windows/hardware/ff542963))、ドライバーを割り当てる必要があります以外**NULL**値を**hResource**のメンバー [ **D3DDDICB\_ALLOCATE**](https://msdn.microsoft.com/library/windows/hardware/ff544137)します。

-   非共有リソースへの応答でユーザー モードのディスプレイ ドライバーを作成する割り当て、ドライバーは必要ありませんを割り当てる以外に**NULL**値を**hResource** D3DDDICB のメンバー\_割り当て。 場合、ドライバーを割り当てる**NULL**に**hResource**割り当ては、デバイスとしない、特定のリソース (およびカーネル モードのリソース ハンドル) に関連付けられました。 ただし、この割り当ては本当に、リソースに関係する場合、ドライバーはそのリソースを割り当てを関連付ける必要があります。
    **注**  ユーザー モード ドライバーのセットを表示する場合にのみ、カーネル モードのリソース ハンドルが作成された、 **hResource** D3DDDICB のメンバー\_ユーザー モードのランタイムのリソースへの配賦を処理する、ドライバーから受信した、 **hResource**のメンバー、 [ **D3DDDIARG\_CREATERESOURCE** ](https://msdn.microsoft.com/library/windows/hardware/ff542963)構造体への呼び出しで[ **CreateResource**](https://msdn.microsoft.com/library/windows/hardware/ff540688)します。

     

-   ときに[ **DestroyResource** ](https://msdn.microsoft.com/library/windows/hardware/ff552795)と呼ばれる、ユーザー モードを非共有リソースを破棄するには、ユーザー モードのディスプレイ ドライバーが呼び出すことができます[ *pfnDeallocateCb* ](https://msdn.microsoft.com/library/windows/hardware/ff568898)で、 **hResource**のメンバー [ **D3DDDICB\_DEALLOCATE** ](https://msdn.microsoft.com/library/windows/hardware/ff544161)設定**NULL**場合にのみ、ドライバーでは、リソースに割り当てを関連付けられていることはありません。 ドライバーを呼び出す必要がある場合は、ユーザー モードのディスプレイ ドライバーには、リソースに割り当てが関連付けられている、 **pfnDeallocateCb**で、 **hResource** D3DDDICB のメンバー\_DEALLOCATE 非-に設定**NULL**値。 それ以外の場合、メモリ リークが発生します。

 

 





