---
title: シェーダーのコード形式
description: シェーダーのコード形式
ms.assetid: 62377d19-8e45-4d0c-b974-0c0417d1a948
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: a5dc4eb7da4c092f541874c0f70e574b125a7073
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829461"
---
# <a name="shader-code-format"></a>シェーダーのコード形式


## <span id="ddk_shader_code_format_gg"></span><span id="DDK_SHADER_CODE_FORMAT_GG"></span>


ピクセルシェーダーまたは頂点シェーダーを作成するコマンドは、シェーダーコードのグループで構成されます。 これらのコードは、シェーダーの作成方法をドライバーに指示します。 各シェーダーコード内のトークンの形式によって、一意性が決まります。 [シェーダーコードトークン](shader-code-tokens.md)は、特定の形式の DWORD です。

DirectX3D ランタイムは、コードをドライバーに渡す前にシェーダーコードを検証します。 シェーダーコードがドライバーに到着すると、コードの形式が有効であるため、ドライバーはコードを解釈できます。 ドライバーは、コードを解釈するためにシェーダーコードのトークンを読み取ります。

個々のシェーダーコードは、一般的なトークンレイアウトで書式設定されます。 最初のトークンは[バージョントークン](version-token.md)である必要があります。 バージョントークンは、コードのバージョン番号を提供します。また、コードがピクセルシェーダーと頂点シェーダーのどちらであるかを判断します。 シェーダーコンテンツは、バージョントークンに従い、さまざまな[命令トークン](instruction-token.md)で構成されます。これは、多くの場合、[コメントトークン](comment-token.md)と空白と混在しています。 命令トークンによって指定される正確な操作に応じて、[ラベル](label-token.md)、[宛先パラメーター](destination-parameter-token.md)、および[ソースパラメータートークン](source-parameter-token.md)もシェーダーの内容の一部にすることができ、命令トークンに従うことができます。 たとえば、命令トークンで[ADD 命令](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d9types/ne-d3d9types-_d3dshader_instruction_opcode_type)が指定されている場合、ドライバーは、1つの変換先と2つのソースパラメータートークンが命令トークンに従うことを決定します。 [終了トークン](end-token.md)がシェーダーコードを完了します。

セットアップ手順 (たとえば、D3DSIO\_DCL と D3DSIO\_DEF) には、一意に書式設定されたトークンが含まれています。

各シェーダー命令には、特定のトークン形式が含まれています。 「[シェーダー操作コード](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d9types/ne-d3d9types-_d3dshader_instruction_opcode_type)」セクションでは、各シェーダー命令のトークン形式について説明します。

シェーダー命令は、最初の命令で始まり、D3DSIO\_RET または D3DSIO\_の終了命令で終了します。 サブルーチンは、D3DSIO\_RET 命令に従います。

命令トークンで指定できる操作の詳細については、最新の DirectX SDK ドキュメントの「ピクセルシェーダーの参照と頂点シェーダーのリファレンス」を参照してください。

## <a name="span-idrequirementsspanspan-idrequirementsspanspan-idrequirementsspanrequirements"></a><span id="Requirements"></span><span id="requirements"></span><span id="REQUIREMENTS"></span>要件


Windows Vista 以降のバージョンの Windows オペレーティングシステムで使用できます。

 

 





