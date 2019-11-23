---
title: フィルター コマンドの非ブロック化
description: フィルター コマンドの非ブロック化
ms.assetid: 9f20c6fa-c515-43b8-a947-f6290d15bd35
keywords:
- マクロは WDK DirectX VA、deblocking filter コマンドをブロックします
- フィルターコマンドをブロックしない場合は、WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e0d505f6ea91b98045aac12e0279c16a73e3beeb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839763"
---
# <a name="deblocking-filter-commands"></a>フィルター コマンドの非ブロック化


## <span id="ddk_deblocking_filter_commands_gg"></span><span id="DDK_DEBLOCKING_FILTER_COMMANDS_GG"></span>


マクロブロックの deblocking filter コマンドでは、現在のマクロブロックの中で再構築されたサンプルの値を読み取るためにアクセラレータが必要になる場合があります。 読み込まれる再構築された値は、現在のマクロブロックの上にあるサンプルの2つの行、現在のマクロブロックの左側にあるサンプルの2つの列、および現在のマクロブロック内のサンプルです。 Deblocking filter コマンドを実行すると、現在のマクロブロックの上にある1行のサンプルと、現在のマクロブロックの左上にあるサンプルの1つの列が変更される可能性があります。また、現在のマクロブロック内のサンプルの最大3行と3列にも変更が加えられます。 このため、特定のマクロブロックに対する deblocking フィルター処理では、他の2つのマクロブロックの前の再構築が必要になる場合があります。

Deblocking フィルターコマンドバッファーには、次の2種類があります。

-   現在の deblocking フィルターコマンドバッファーの外部にあるマクロブロックの再構築されたサンプルの値のアクセスと変更を必要とするバッファー ( [**DXVA\_ピクチャパラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_pictureparameters)構造体が**0 の場合**)。

-   現在の deblocking フィルターコマンドバッファーの外部にあるマクロブロックの再構築されたサンプルの値のアクセスと変更を必要としないバッファー ( **B絵文字 Deblock限定**が1の場合)。

最初の種類の deblocking コマンドバッファーを処理するには、現在のバッファーで制御されるマクロブロックの左または上にあるマクロブロックに影響するすべてのバッファーに対して、マクロブロックの再構築が完了している必要があります。 これは、現在のバッファー内の deblocking コマンドを処理する前に行う必要があります。

2番目の種類の deblocking コマンドバッファーを処理するために、アクセラレータは、現在のバッファー内の以前の再構築値のみを使用します。

Deblocking フィルター操作は、次の2つの方法のいずれかでアクセラレータで実行できます。

-   バッファーまたはフレーム全体のモーション予測と残差データを最初に処理した後、いくつかのサンプルの値を読み戻し、deblocking フィルター操作の結果として変更します。

-   残余差データバッファーを使用して、deblocking コマンドバッファーを調整して処理します。 この場合、deblocking コマンドバッファーは、再構築された出力値をコピー先の画像サーフェイスに書き込む前に処理されます。

ブロックされていない画像の目的の画像の表面は、deblocked の前に再構築された画像とは異なる場合がある**ことに注意**してください  。 これにより、次の図の予測に使用されるサンプル値に影響を与えない postdecoding プロセスとして、"ループの外側" の deblocking がサポートされるようになります。

 

 

 





