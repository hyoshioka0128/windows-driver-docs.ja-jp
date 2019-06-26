---
title: フィルター コマンドの非ブロック化
description: フィルター コマンドの非ブロック化
ms.assetid: 9f20c6fa-c515-43b8-a947-f6290d15bd35
keywords:
- マクロ ブロック WDK DirectX va なので、フィルター コマンドが非ブロック化
- 非ブロック化フィルター コマンド WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1663b1c9814bc5c8b7b9193960c3d7c2a668f2c8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358652"
---
# <a name="deblocking-filter-commands"></a>フィルター コマンドの非ブロック化


## <span id="ddk_deblocking_filter_commands_gg"></span><span id="DDK_DEBLOCKING_FILTER_COMMANDS_GG"></span>


マクロ ブロックの deblocking filter コマンドは、アクセス キーの値は、サンプルを再構築の読み取り専用にし、次へ を現在のマクロ ブロック必要があります。 読み取られた再構築された値は、現在のマクロ ブロックでは、上記のサンプル、現在のマクロ ブロックの左側と現在のマクロ ブロック内のサンプルの 2 つの列の 2 つの行です。 Deblocking フィルタ コマンドの現在のマクロ ブロックの上のサンプルの 1 つの行と最大 3 つの行だけでなく、現在のマクロ ブロックの残りのサンプルの 1 つの列と 3 つの列の現在のマクロ ブロック内のサンプルの変更可能性があります。 デバッグ情報を非ブロック化、特定のマクロ ブロックのプロセスをフィルター処理、他の 2 つのマクロ ブロックの前の再構築できますが、そのため、必要があります。

フィルター コマンド バッファーを非ブロック化の 2 つのさまざまな種類は次のとおりです。

-   アクセスとの値の変更が必要なバッファーの現在のフィルター deblocking コマンド バッファー外のマクロ ブロック用のサンプルを再構築 (ときに、 **bPicDeblockConfined**のメンバー、 [ **DXVA\_PictureParameters** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_pictureparameters)構造体は 0 です)。

-   アクセスおよびの値の変更が不要なバッファーの現在のフィルター deblocking コマンド バッファー外のマクロ ブロック用のサンプルを再構築 (と**bPicDeblockConfined**は 1)。

コマンド バッファーを非ブロック化の最初のタイプを処理するには、アクセラレータはマクロ ブロックを左または現在のバッファーで制御するマクロ ブロックの上に影響を与えるすべてのバッファーのマクロ ブロックの再構築が完了したことを確認する必要があります。 これは、現在のバッファーに deblocking コマンドを処理する前に実行する必要があります。

コマンド バッファーを非ブロック化の 2 番目の型を処理するには、アクセラレータは、現在のバッファー内の以前の再構築値のみを使用します。

Deblocking フィルター操作は、2 つの方法のいずれかで、アクセラレータで実行できます。

-   サンプルの一部の値に読み取り、deblocking のフィルター操作の結果の変更によってバッファー全体またはフレームのモーション予測および残余違いのデータが最初に、後に処理します。

-   残存の違いのデータ バッファーと共に連携のとれた方法で deblocking コマンド バッファーを処理します。 この場合、deblocking コマンド バッファーは、転送先の画像のサーフェイスに再構築された出力値を書き込む前に処理されます。

**注**   deblocked 画像の転送先の画像サーフェスが非ブロック化する前に再構築された画像のと異なる可能性があります。 次の図の予測に使用するサンプルの値によって影響されなかった postdecoding プロセスとして非ブロック化""ループの外側これが、サポートされます。

 

 

 





