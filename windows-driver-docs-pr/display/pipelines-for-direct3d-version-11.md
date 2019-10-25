---
title: Direct3D バージョン 11 のパイプライン
description: Direct3D バージョン 11 のパイプライン
ms.assetid: 7d724751-761e-409c-8398-d1b5d58c057c
keywords:
- Direct3D バージョン 11 WDK Windows 7 display、パイプライン
- Direct3D バージョン 11 WDK Windows Server 2008 R2 の表示、パイプライン
- Direct3D version 11 WDK Windows 7 ディスプレイのパイプライン
- Direct3D バージョン 11 WDK Windows Server 2008 R2 のパイプラインの表示
- ハル shader WDK Windows 7 ディスプレイ
- ハル shader WDK Windows Server 2008 R2 ディスプレイ
- テッセレータ WDK Windows 7 ディスプレイ
- テッセレータ WDK Windows Server 2008 R2 ディスプレイ
- ドメインシェーダー WDK Windows 7 ディスプレイ
- ドメインシェーダー WDK Windows Server 2008 R2 ディスプレイ
- コンピューティングシェーダー WDK Windows 7 ディスプレイ
- コンピューティングシェーダー WDK Windows Server 2008 R2 ディスプレイ
- 順序付けられていないアクセスリソースビュー WDK Windows 7 ディスプレイ
- 順序付けられていないアクセスリソースビュー WDK Windows Server 2008 R2 ディスプレイ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d659bbfd55d0db3b99f5b44ae6925846851e7a9b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829810"
---
# <a name="pipelines-for-direct3d-version-11"></a>Direct3D バージョン 11 のパイプライン


このセクションは、windows 7 以降、および windows Server 2008 R2 以降のバージョンの Windows オペレーティングシステムにのみ適用されます。

Direct3D バージョン11用のグラフィックスレンダリングパイプラインは、 [direct3d バージョン10用のグラフィックスレンダリングパイプライン](rendering-pipeline.md)から展開されています。 Direct3d バージョン10でサポートされている共有のプログラミング可能なシェーダーコアに加えて、Direct3D バージョン11では、ハル、ドメイン、およびコンピューティングシェーダーコアもサポートされています。

Direct3D バージョン11では、描画パイプライン (グラフィックスレンダリングパイプライン) とディスパッチパイプライン (計算シェーダーパイプライン) という2つの異なるパイプラインが実際にサポートされています。 描画とディスパッチのパイプラインは、両方のパイプラインで同時に書き込みを行うために同じサブリソースをバインドすることも、1つのパイプラインで書き込みを行うためにバインドすることも、もう一方のパイプラインで読み取ることもできないという点で、技術的には緩やかに接続されています。

次の図は、Direct3D バージョン11用の描画パイプラインの機能ブロックを示しています。

![描画パイプラインの機能ブロックを示す図](images/pipeline-dx11.png)

次の図は、Direct3D バージョン11のディスパッチパイプラインの機能ブロックを示しています。

![ディスパッチパイプラインの機能ブロックを示す図](images/pipeline-compute.png)

以下のセクションでは、前の図に示されている新しい Direct3D 11 ブロックについて説明します。

### <a name="span-idhull_shaderspanspan-idhull_shaderspanhull-shader"></a><span id="hull_shader"></span><span id="HULL_SHADER"></span>ハルシェーダー

ハルシェーダーは、修正プログラムごとに1回動作します。 ハルシェーダーは、入力アセンブラーの修正プログラムと共に使用できます。 ハルシェーダーは、修正プログラムを構成する入力コントロールポイントを出力制御ポイントに変換できます。 ハルシェーダーは、固定関数テッセレータステージに対して他の設定を実行できます。 たとえば、ハルシェーダーは、テセレーションを示す数値である tess 要因を出力できます。

Direct3D ランタイムは、次のドライバー関数を呼び出して、ハルシェーダーを作成、設定、および破棄します。

[**CalcPrivateShaderSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_calcprivateshadersize)

[**CalcPrivateTessellationShaderSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_calcprivatetessellationshadersize)

[*CreateHullShader*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createhullshader)

[**DestroyShader**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_destroyshader)

[**HsSetShaderResources**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setshaderresources)

[**HsSetShader**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setshader)

[**HsSetSamplers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setsamplers)

[**HsSetConstantBuffers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setconstantbuffers)

[**HsSetShaderWithIfaces**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_setshader_with_ifaces)

### <a name="span-idtessellatorspanspan-idtessellatorspantessellator"></a><span id="tessellator"></span><span id="TESSELLATOR"></span>テッセレータ

テッセレータは、ハルシェーダー内の宣言によって操作が定義されている固定関数単位です。 テッセレータは、ハルシェーダーによって出力される修正プログラムごとに1回動作します。 ハルシェーダーは tess 要因を生成します。これは、修正プログラムのドメインでテセレーション (geometry と接続の生成) の量をテッセレータに通知する数値です。

Direct3D ランタイムは、ドライバーの[**CalcPrivateTessellationShaderSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_calcprivatetessellationshadersize)関数を呼び出して、ハルまたはドメインシェーダーのメモリ領域のサイズを計算します。

### <a name="span-iddomain_shaderspanspan-iddomain_shaderspandomain-shader"></a><span id="domain_shader"></span><span id="DOMAIN_SHADER"></span>ドメインシェーダー

ドメインシェーダーは、テッセレータによって生成される頂点ごとに1回呼び出されます。 各呼び出しは、一般的なドメインの座標によって識別されます。 ドメインシェーダーの役割は、ドメインシェーダーの下位ストリームを使用するために、その座標を (3 次元空間のポイントなどの) 明確なものにすることです。 パッチの各ドメインシェーダー呼び出しも、すべてのハル shader 出力 (出力制御ポイントなど) の共有入力にアクセスします。

Direct3D ランタイムは、次のドライバー関数を呼び出して、ドメインシェーダーを作成、設定、および破棄します。

[**CalcPrivateTessellationShaderSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_calcprivatetessellationshadersize)

[*CreateDomainShader*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createdomainshader)

[**DestroyShader**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_destroyshader)

[**DsSetShaderResources**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setshaderresources)

[**DsSetShader**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setshader)

[**DsSetSamplers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setsamplers)

[**DsSetConstantBuffers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setconstantbuffers)

[**DsSetShaderWithIfaces**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_setshader_with_ifaces)

### <a name="span-idcompute_shaderspanspan-idcompute_shaderspancompute-shader"></a><span id="compute_shader"></span><span id="COMPUTE_SHADER"></span>計算シェーダー

コンピューティングシェーダーを使用すると、GPU をデータ並列プロセッサの汎用グリッドとして表示できます。描画パイプラインからのグラフィックスの障害は発生しません。 コンピューティングシェーダーは、高速共有メモリに明示的にアクセスして、シェーダー呼び出しのグループ間の通信を容易にします。 コンピューティングシェーダーでは、メモリに対して散在する読み取りと書き込みを実行する機能も備えています。 アトミック操作の可用性は、共有メモリアドレスへの一意のアクセスを可能にします。 コンピューティングシェーダーは、描画パイプラインの一部ではありません。 コンピューティングシェーダーは、それ自体に存在します。 ただし、コンピューティングシェーダーは、他のすべてのシェーダーステージと同じデバイスに存在します。 Direct3D ランタイムは、ドライバーの*Drawxxx*関数ではなく、ドライバーの*DispatchXxx*関数を呼び出して、コンピューティングシェーダーを呼び出します。

Direct3D ランタイムは、次のドライバー関数を呼び出して、コンピューティングシェーダーを作成、設定、および破棄します。

[*CreateComputeShader*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createcomputeshader)

[**DestroyShader**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_destroyshader)

[**CsSetShaderResources**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setshaderresources)

[**CsSetShader**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setshader)

[**CsSetSamplers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setsamplers)

[**CsSetConstantBuffers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setconstantbuffers)

[**CsSetShaderWithIfaces**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_setshader_with_ifaces)

[**CsSetUnorderedAccessViews**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_setunorderedaccessviews)

[**Dispatch**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_dispatch)

[**DispatchIndirect**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_dispatchindirect)

### <a name="span-idunordered_access_resource_viewsspanspan-idunordered_access_resource_viewsspanunordered-access-resource-views"></a><span id="unordered_access_resource_views"></span><span id="UNORDERED_ACCESS_RESOURCE_VIEWS"></span>順序付けられていないアクセスのリソースビュー

順序付けられていないアクセスリソースビューは、コンピューティングシェーダーまたはピクセルシェーダーにバインドできる読み取り/書き込みリソースです。 順序付けられていないアクセスリソースビューのバインドは、読み取り専用のリソースであるシェーダーのリソースビューを任意のシェーダーステージにバインドする方法に似ています。

Direct3D ランタイムは、次のドライバー関数を呼び出して、順序付けられていないアクセスリソースビューを作成、設定、および破棄します。

[**CalcPrivateUnorderedAccessViewSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_calcprivateunorderedaccessviewsize)

[**CreateUnorderedAccessView**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createunorderedaccessview)

[**DestroyUnorderedAccessView**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_destroyunorderedaccessview)

[**ClearUnorderedAccessViewFLOAT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_clearunorderedaccessviewfloat)

[**ClearUnorderedAccessViewUINT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_clearunorderedaccessviewuint)

[**CopyStructureCount**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_copystructurecount)

[**SetRenderTargets (D3D11)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_setrendertargets)

 

 





