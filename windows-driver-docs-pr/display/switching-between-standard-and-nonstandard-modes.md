---
title: 標準および非標準モードの切り替え
description: 標準および非標準モードの切り替え
ms.assetid: 15939910-b325-47ff-b4ed-bbaeec4149bd
keywords:
- 非標準の表示モード WDK DirectX 9.0、標準および非標準モードの切り替え
- WDK DirectX 9.0 の標準および非標準モードの切り替え
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bd007ce8d8298fe85907c80bb7005e1147e26681
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553710"
---
# <a name="switching-between-standard-and-nonstandard-modes"></a>標準および非標準モードの切り替え


## <span id="ddk_switching_between_standard_and_nonstandard_modes_gg"></span><span id="DDK_SWITCHING_BETWEEN_STANDARD_AND_NONSTANDARD_MODES_GG"></span>


DirectX 9.0 ドライバーは、標準の表示モードの標準のプライマリ画面と標準モードのダミーのプライマリ画面を作成するため、ランタイムは、必要な場合に、モードを切り替えることができます。 両方のサーフェスに表示されているさまざまな形式を除く、同じビデオ メモリを表します。 次の順序で示すように、ドライバーを切り替えますときに、ページ フリップは、標準および非標準のモードが要求されます。

1.  アプリケーションでは、モードの切り替えを要求します。

    アプリケーションを呼び出す、 **ChangeDisplaySettings**に対応するビット深度画像モードを変更する関数。 10:10:10:2 モードの場合は、ビット深さは、ピクセルあたり 32 ビットをします。 詳細については**ChangeDisplaySettings**、Microsoft Windows SDK のドキュメントを参照してください。

2.  ドライバーは、標準のプライマリ画面を作成します。

    ランタイムが呼び出す、ドライバーの[ *DdCreateSurface* ](https://msdn.microsoft.com/library/windows/hardware/ff549263)プライマリ画面の作成を要求する関数。 このプライマリ画面には、標準の表示形式が使用されます (D3DFMT など\_A8B8G8R8) をバック バッファーを持ちません。

3.  ドライバーは、ダミーのプライマリ画面チェーンを作成します。

    ランタイムが呼び出す、ドライバーの*DdCreateSurface*ダミーのプライマリ画面の作成を要求する関数。 ランタイムの指定、DDSCAPS2\_ビット EXTENDEDFORMATPRIMARY (0x40000000) 機能、 **dwCaps2**のメンバー、 [ **DDSCAPS2** ](https://msdn.microsoft.com/library/windows/hardware/ff550292)用の構造サーフェスが非表示モードを使用するように指定するには、この画面 (たとえば、D3DFMT\_A2R10G10B10)。 ランタイムも指定して、DDSCAPS\_OFFSCREENPLAIN 機能ビット、 **dwCaps**画面に、明示的なピクセル形式を示す DDSCAPS2 のメンバー。

    この画面は、既存のプライマリ画面のもう 1 つの名前にするとしているため、ドライバーがメモリを割り当てられませんさらにビデオを画面に。

    この画面のランタイムも指定します、DDSCAPS\_反転、DDSCAPS\_で複雑な機能がビット**dwCaps**と接続されているランタイムは、標準のプライマリを設定する方法と同様に、バック バッファーのセット画面のチェーンを反転します。 ドライバーはビデオ メモリを割り当てる必要がありますので、これらのバック バッファーのドライバーのないそれ以降の呼び出し*DdCreateSurface*関数は、これらのバック バッファーに対して行われる; は、ランタイムはのみの 1 つ以上の画面オブジェクトを作成します、。標準プライマリです。

4.  ドライバーは、非標準形式に画面を反転します。

    ディスプレイ デバイスは、標準の形式を出力、中に、アプリケーションは、これらのバック バッファーのいずれかで非標準のイメージを作成します。 このイメージは、すぐに表示できるが、ランタイムを指定します、非標準のサーフェスのいずれかのドライバーの呼び出しでターゲットとして[ *DdFlip* ](https://msdn.microsoft.com/library/windows/hardware/ff549306)関数。 ドライバーでは、ディスプレイ デバイスを非標準の形式を出力し、reprograms します。

5.  アプリケーションを実行します。

    アプリケーションがドライバーのそれ以降の呼び出しを生成*DdFlip*非標準のバッファーとドライバーの間の関数は、非標準の形式を表示します。 アプリケーションでは、ドライバーへの呼び出しを生成できますも[ **D3dDrawPrimitives2** ](https://msdn.microsoft.com/library/windows/hardware/ff544704) 、D3DDP2OP を使用して機能\_フロント バッファーが、これらの呼び出しにバック バッファーをコピーする BLT 操作コード常に、2 つの非標準のサーフェス オブジェクト間で行われます。 ドライバーは、ウィンドウ表示モードで非標準の形式をサポートする場合を除き、ドライバーでは非標準と標準のサーフェス形式の間の blt は処理されません。 詳細については、ウィンドウ表示モードの場合は、次を参照してください。 [Two-Dimensional 操作のサポート](supporting-two-dimensional-operations.md)します。

6.  ドライバーは、標準の形式に surface の背面を反転します。

    ランタイムが、ドライバーへの呼び出しで、変換先として、標準形式のプライマリ画面を指定します、アプリケーションが終了するか最小限に抑える*DdFlip*関数。 ドライバーでは、標準の形式を出力する、ディスプレイ デバイスし reprograms します。

7.  ドライバーは、ダミーのサーフェスを破棄します。

    ドライバーが、ダミーの画面を破棄するとき、ディスプレイ デバイスの標準書式指定を行ったり、確認してください。

 

 





