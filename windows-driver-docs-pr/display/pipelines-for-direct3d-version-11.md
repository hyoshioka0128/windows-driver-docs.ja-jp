---
title: Direct3D バージョン 11 のパイプライン
description: Direct3D バージョン 11 のパイプライン
ms.assetid: 7d724751-761e-409c-8398-d1b5d58c057c
keywords:
- Direct3D のバージョン 11 WDK Windows 7 の表示、パイプラインします。
- Direct3D のバージョン 11 WDK Windows Server 2008 R2 を表示するためのパイプライン
- パイプラインを Direct3D のバージョンの WDK Windows 7 の 11 の表示
- Direct3D のバージョン 11 WDK Windows Server 2008 R2 の表示用のパイプライン
- ハル シェーダー WDK Windows 7 の表示
- ハル シェーダー WDK Windows Server 2008 R2 の表示
- テッセレータ WDK Windows 7 の表示
- テッセレータ WDK Windows Server 2008 R2 の表示
- ドメイン シェーダー WDK Windows 7 の表示
- ドメイン シェーダー WDK Windows Server 2008 R2 の表示
- 計算シェーダー WDK Windows 7 の表示
- 計算シェーダー WDK Windows Server 2008 R2 の表示
- 順序付けられていないアクセス リソース ビュー WDK Windows 7 を表示します。
- 順序付けられていないアクセス リソース ビューの WDK Windows Server 2008 R2 の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c2597e2e73e3330a2109e731fabc9bb6b2877107
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385573"
---
# <a name="pipelines-for-direct3d-version-11"></a>Direct3D バージョン 11 のパイプライン


このセクションでは、Windows 7 以降および Windows Server 2008 R2 以降のバージョンの Windows オペレーティング システムにのみ適用されます。

Direct3D のバージョン 11 のグラフィックのレンダリング パイプラインから展開されますが、[バージョン 10 で Direct3D グラフィックスのレンダリング パイプライン](rendering-pipeline.md)します。 Direct3D のバージョン 11、プログラミング可能なシェーダーが共有コア、Direct3D のバージョン 10 がサポートされているだけでもサポートしていますハル、ドメイン、および計算シェーダーのコア。

Direct3D のバージョン 11 が実際には 2 つの異なるパイプラインをサポートしています: 描画パイプライン (グラフィックス レンダリング パイプライン) とディスパッチ パイプライン (計算シェーダー パイプライン)。 描画とディスパッチのパイプラインは、技術的には両方のパイプラインで同時に、作成するためのバインドまたはバインドされた 1 つのパイプラインを作成するため、および他のパイプラインでの読み取り用に同じ subresource ができないという意味で接続疎されます。

次の図は、Direct3D のバージョン 11 の描画パイプラインの機能ブロックを示します。

![描画パイプラインの機能ブロックを示す図](images/pipeline-dx11.png)

次の図は、Direct3D のバージョン 11 のディスパッチ パイプラインの機能ブロックを示します。

![ディスパッチのパイプラインの機能ブロックを示す図](images/pipeline-compute.png)

次のセクションでは、上記の図に示すような Direct3D の新しい 11 要素について説明します。

### <a name="span-idhullshaderspanspan-idhullshaderspanhull-shader"></a><span id="hull_shader"></span><span id="HULL_SHADER"></span>ハル シェーダー

ハル シェーダーは、修正プログラムあたり 1 回は動作します。 ハル シェーダーを使用するには、入力アセンブラーから修正プログラムを適用します。 ハル シェーダーは出力制御点に修正プログラムを構成する入力の制御点を変換できます。 ハル シェーダーは、固定関数テッセレータ ステージの他のセットアップを実行できます。 たとえば、ハル シェーダーは tess 要因は、テセレーションする量を示す数値を出力できます。

Direct3D のランタイムは、設定を作成する次のドライバー関数を呼び出すし、ハル シェーダーを破棄します。

[**CalcPrivateShaderSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_calcprivateshadersize)

[**CalcPrivateTessellationShaderSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_calcprivatetessellationshadersize)

[*CreateHullShader*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createhullshader)

[**DestroyShader**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_destroyshader)

[**HsSetShaderResources**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setshaderresources)

[**HsSetShader**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setshader)

[**HsSetSamplers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setsamplers)

[**HsSetConstantBuffers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setconstantbuffers)

[**HsSetShaderWithIfaces**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_setshader_with_ifaces)

### <a name="span-idtessellatorspanspan-idtessellatorspantessellator"></a><span id="tessellator"></span><span id="TESSELLATOR"></span>テッセレータ

テッセレータは、ある操作が、ハル シェーダー内の宣言によって定義されている固定機能単位です。 テッセレータは、ハル シェーダーによって出力が更新プログラムごとに動作します。 ハル シェーダー tess 要因は、テセレーションにどの程度、テッセレータを通知する数字が生成されます (geometry と接続の生成)、修正プログラムのドメイン。

Direct3D ランタイムが呼び出す、ドライバーの[ **CalcPrivateTessellationShaderSize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_calcprivatetessellationshadersize)包またはドメイン シェーダーのメモリ領域のサイズを計算する関数。

### <a name="span-iddomainshaderspanspan-iddomainshaderspandomain-shader"></a><span id="domain_shader"></span><span id="DOMAIN_SHADER"></span>ドメイン シェーダー

ドメイン シェーダーは、テッセレータによって生成される、頂点ごと 1 回呼び出されます。 各呼び出しは、汎用的なドメインでは、その座標によって識別されます。 ドメイン シェーダーの役割は、3-D 空間内のポイント) (など、具体的なものには、その座標を有効にするドメイン シェーダーのストリームを使用します。 修正プログラムで、各ドメイン シェーダーの呼び出しでは、ハル シェーダーのすべての出力を (など、出力の制御点) の入力を共有にもアクセスします。

Direct3D のランタイムは、設定を作成する次のドライバー関数を呼び出すし、ドメイン シェーダーを破棄します。

[**CalcPrivateTessellationShaderSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_calcprivatetessellationshadersize)

[*CreateDomainShader*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createdomainshader)

[**DestroyShader**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_destroyshader)

[**DsSetShaderResources**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setshaderresources)

[**DsSetShader**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setshader)

[**DsSetSamplers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setsamplers)

[**DsSetConstantBuffers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setconstantbuffers)

[**DsSetShaderWithIfaces**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_setshader_with_ifaces)

### <a name="span-idcomputeshaderspanspan-idcomputeshaderspancompute-shader"></a><span id="compute_shader"></span><span id="COMPUTE_SHADER"></span>計算シェーダー

計算シェーダーは、GPU が描画パイプラインからのすべてのグラフィックス懸案事項なしのデータを並列プロセッサの一般的なグリッドと見なすことができます。 計算シェーダーが高速に明示的なアクセス権をシェーダーの呼び出しのグループ間の通信を容易にメモリを共有します。 計算シェーダーも分散読み込みを実行する権限を持ち、メモリに書き込みます。 アトミック操作の可用性には、共有メモリ アドレスに一意のアクセスができます。 計算シェーダーは描画パイプラインの一部ではありません。 計算シェーダーは、独自に存在します。 ただし、計算シェーダーは、その他のすべてのシェーダー ステージと同じデバイスに存在します。 Direct3D ランタイムが呼び出す、ドライバーの*DispatchXxx*ドライバーのではなく関数*DrawXxx*計算シェーダーを呼び出す関数。

Direct3D のランタイムは、設定を作成する次のドライバー関数を呼び出すし、計算シェーダーを破棄します。

[*CreateComputeShader*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createcomputeshader)

[**DestroyShader**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_destroyshader)

[**CsSetShaderResources**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setshaderresources)

[**CsSetShader**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setshader)

[**CsSetSamplers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setsamplers)

[**CsSetConstantBuffers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setconstantbuffers)

[**CsSetShaderWithIfaces**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_setshader_with_ifaces)

[**CsSetUnorderedAccessViews**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_setunorderedaccessviews)

[**Dispatch**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_dispatch)

[**DispatchIndirect**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_dispatchindirect)

### <a name="span-idunorderedaccessresourceviewsspanspan-idunorderedaccessresourceviewsspanunordered-access-resource-views"></a><span id="unordered_access_resource_views"></span><span id="UNORDERED_ACCESS_RESOURCE_VIEWS"></span>順序付けられていないアクセス リソース ビュー

順序付けられていないアクセス リソース ビューは、計算シェーダーまたはピクセル シェーダーにバインドできる読み取り/書き込みリソースです。 順序付けられていないアクセス リソース ビューのバインドは、任意のシェーダー ステージのシェーダー リソース ビューは読み取り専用のリソースのバインド方法に似ています。

Direct3D のランタイムは、設定を作成する次のドライバー関数を呼び出すし、順序付けられていないアクセス リソース ビューを破棄します。

[**CalcPrivateUnorderedAccessViewSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_calcprivateunorderedaccessviewsize)

[**CreateUnorderedAccessView**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createunorderedaccessview)

[**DestroyUnorderedAccessView**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_destroyunorderedaccessview)

[**ClearUnorderedAccessViewFLOAT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_clearunorderedaccessviewfloat)

[**ClearUnorderedAccessViewUINT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_clearunorderedaccessviewuint)

[**CopyStructureCount**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_copystructurecount)

[**SetRenderTargets(D3D11)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_setrendertargets)

 

 





