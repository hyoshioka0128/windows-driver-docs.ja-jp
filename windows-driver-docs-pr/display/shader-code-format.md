---
title: シェーダーのコード形式
description: シェーダーのコード形式
ms.assetid: 62377d19-8e45-4d0c-b974-0c0417d1a948
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 506c7be066efb38ef8ef473c6194ad1dd1c5e27a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348324"
---
# <a name="shader-code-format"></a>シェーダーのコード形式


## <span id="ddk_shader_code_format_gg"></span><span id="DDK_SHADER_CODE_FORMAT_GG"></span>


ピクセルまたは頂点シェーダーを作成するコマンドは、シェーダー コードのグループで構成されます。 これらのコードは、シェーダーを作成する方法のドライバーに指示します。 各シェーダー コード内のトークンの形式は、その一意性を決定します。 A[シェーダー コード トークン](shader-code-tokens.md)は、特定の形式を持つ DWORD。

DirectX3D ランタイムは、ドライバーのコードに渡す前に、シェーダー コードを検証します。 ドライバーでシェーダー コードが到着すると、ドライバーは、コードの形式が有効であるため、コードを解釈できます。 ドライバーは、シェーダー コードを解釈するコードのトークンを読み取ります。

各個々 のシェーダー コードには、一般的なトークンのレイアウトが表示されます。 最初のトークンである必要があります、[バージョン トークン](version-token.md)します。 バージョン トークンは、コードのバージョン番号を示しもピクセルまたは頂点シェーダーのコードは、かどうかを決定します。 シェーダー コンテンツが依存して、バージョン トークンと、さまざまなで構成されます[命令トークン](instruction-token.md)でおそらく、混在した状態で、[コメント トークン](comment-token.md)および空白です。 命令のトークンを指定する正確な動作によって[ラベル](label-token.md)、 [destination パラメーター](destination-parameter-token.md)、および[パラメーター トークンをソース](source-parameter-token.md)シェーダーの一部にすることもできますコンテンツは、命令、トークンに従ってください。 たとえば、次の命令のトークンを指定します、 [ADD 命令](https://msdn.microsoft.com/library/windows/hardware/ff538212)ドライバーは、1 つの送信先と 2 つのソース パラメーター トークンが命令のトークンを従うことを決定します。 [トークンの終了](end-token.md)シェーダー コードが完了するとします。

セットアップ手順 (D3DSIO など\_DCL と D3DSIO\_DEF) 一意に書式設定されたトークンを含めることができます。

各シェーダーの命令には、特定のトークン形式が含まれています。 [シェーダー オペレーション コード](https://msdn.microsoft.com/library/windows/hardware/ff569706)セクションには、各シェーダーの命令のトークンの形式がについて説明します。

シェーダー命令がプライマリの命令の先頭し、末尾を D3DSIO 使用\_RET または D3DSIO\_END 命令。 次のサブルーチン、D3DSIO\_RET 命令。

命令のトークンで指定できる操作の詳細については、最新の DirectX SDK ドキュメントでは、ピクセル シェーダーの参照と頂点シェーダーのリファレンスを参照してください。

## <a name="span-idrequirementsspanspan-idrequirementsspanspan-idrequirementsspanrequirements"></a><span id="Requirements"></span><span id="requirements"></span><span id="REQUIREMENTS"></span>要件


Windows Vista および Windows オペレーティング システムの以降のバージョンで使用できます。

 

 





