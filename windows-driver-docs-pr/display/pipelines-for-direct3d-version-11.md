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
ms.openlocfilehash: 788c3c5ee9f1ad42fc9855044ca71bb4fb497c60
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579120"
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

[**CalcPrivateShaderSize**](https://msdn.microsoft.com/library/windows/hardware/ff538315)

[**CalcPrivateTessellationShaderSize**](https://msdn.microsoft.com/library/windows/hardware/ff538318)

[*CreateHullShader*](https://msdn.microsoft.com/library/windows/hardware/ff540655)

[**DestroyShader**](https://msdn.microsoft.com/library/windows/hardware/ff552805)

[**HsSetShaderResources**](https://msdn.microsoft.com/library/windows/hardware/ff567300)

[**HsSetShader**](https://msdn.microsoft.com/library/windows/hardware/ff567294)

[**HsSetSamplers**](https://msdn.microsoft.com/library/windows/hardware/ff567290)

[**HsSetConstantBuffers**](https://msdn.microsoft.com/library/windows/hardware/ff567286)

[**HsSetShaderWithIfaces**](https://msdn.microsoft.com/library/windows/hardware/ff567306)

### <a name="span-idtessellatorspanspan-idtessellatorspantessellator"></a><span id="tessellator"></span><span id="TESSELLATOR"></span>テッセレータ

テッセレータは、ある操作が、ハル シェーダー内の宣言によって定義されている固定機能単位です。 テッセレータは、ハル シェーダーによって出力が更新プログラムごとに動作します。 ハル シェーダー tess 要因は、テセレーションにどの程度、テッセレータを通知する数字が生成されます (geometry と接続の生成)、修正プログラムのドメイン。

Direct3D ランタイムが呼び出す、ドライバーの[ **CalcPrivateTessellationShaderSize** ](https://msdn.microsoft.com/library/windows/hardware/ff538318)包またはドメイン シェーダーのメモリ領域のサイズを計算する関数。

### <a name="span-iddomainshaderspanspan-iddomainshaderspandomain-shader"></a><span id="domain_shader"></span><span id="DOMAIN_SHADER"></span>ドメイン シェーダー

ドメイン シェーダーは、テッセレータによって生成される、頂点ごと 1 回呼び出されます。 各呼び出しは、汎用的なドメインでは、その座標によって識別されます。 ドメイン シェーダーの役割は、3-D 空間内のポイント) (など、具体的なものには、その座標を有効にするドメイン シェーダーのストリームを使用します。 修正プログラムで、各ドメイン シェーダーの呼び出しでは、ハル シェーダーのすべての出力を (など、出力の制御点) の入力を共有にもアクセスします。

Direct3D のランタイムは、設定を作成する次のドライバー関数を呼び出すし、ドメイン シェーダーを破棄します。

[**CalcPrivateTessellationShaderSize**](https://msdn.microsoft.com/library/windows/hardware/ff538318)

[*CreateDomainShader*](https://msdn.microsoft.com/library/windows/hardware/ff540637)

[**DestroyShader**](https://msdn.microsoft.com/library/windows/hardware/ff552805)

[**DsSetShaderResources**](https://msdn.microsoft.com/library/windows/hardware/ff557306)

[**DsSetShader**](https://msdn.microsoft.com/library/windows/hardware/ff557305)

[**DsSetSamplers**](https://msdn.microsoft.com/library/windows/hardware/ff557298)

[**DsSetConstantBuffers**](https://msdn.microsoft.com/library/windows/hardware/ff557289)

[**DsSetShaderWithIfaces**](https://msdn.microsoft.com/library/windows/hardware/ff557316)

### <a name="span-idcomputeshaderspanspan-idcomputeshaderspancompute-shader"></a><span id="compute_shader"></span><span id="COMPUTE_SHADER"></span>計算シェーダー

計算シェーダーは、GPU が描画パイプラインからのすべてのグラフィックス懸案事項なしのデータを並列プロセッサの一般的なグリッドと見なすことができます。 計算シェーダーが高速に明示的なアクセス権をシェーダーの呼び出しのグループ間の通信を容易にメモリを共有します。 計算シェーダーも分散読み込みを実行する権限を持ち、メモリに書き込みます。 アトミック操作の可用性には、共有メモリ アドレスに一意のアクセスができます。 計算シェーダーは描画パイプラインの一部ではありません。 計算シェーダーは、独自に存在します。 ただし、計算シェーダーは、その他のすべてのシェーダー ステージと同じデバイスに存在します。 Direct3D ランタイムが呼び出す、ドライバーの*DispatchXxx*ドライバーのではなく関数*DrawXxx*計算シェーダーを呼び出す関数。

Direct3D のランタイムは、設定を作成する次のドライバー関数を呼び出すし、計算シェーダーを破棄します。

[*CreateComputeShader*](https://msdn.microsoft.com/library/windows/hardware/ff540606)

[**DestroyShader**](https://msdn.microsoft.com/library/windows/hardware/ff552805)

[**CsSetShaderResources**](https://msdn.microsoft.com/library/windows/hardware/ff540802)

[**CsSetShader**](https://msdn.microsoft.com/library/windows/hardware/ff540799)

[**CsSetSamplers**](https://msdn.microsoft.com/library/windows/hardware/ff540795)

[**CsSetConstantBuffers**](https://msdn.microsoft.com/library/windows/hardware/ff540794)

[**CsSetShaderWithIfaces**](https://msdn.microsoft.com/library/windows/hardware/ff540805)

[**CsSetUnorderedAccessViews**](https://msdn.microsoft.com/library/windows/hardware/ff540808)

[**ディスパッチ**](https://msdn.microsoft.com/library/windows/hardware/ff553896)

[**DispatchIndirect**](https://msdn.microsoft.com/library/windows/hardware/ff553899)

### <a name="span-idunorderedaccessresourceviewsspanspan-idunorderedaccessresourceviewsspanunordered-access-resource-views"></a><span id="unordered_access_resource_views"></span><span id="UNORDERED_ACCESS_RESOURCE_VIEWS"></span>順序付けられていないアクセス リソース ビュー

順序付けられていないアクセス リソース ビューは、計算シェーダーまたはピクセル シェーダーにバインドできる読み取り/書き込みリソースです。 順序付けられていないアクセス リソース ビューのバインドは、任意のシェーダー ステージのシェーダー リソース ビューは読み取り専用のリソースのバインド方法に似ています。

Direct3D のランタイムは、設定を作成する次のドライバー関数を呼び出すし、順序付けられていないアクセス リソース ビューを破棄します。

[**CalcPrivateUnorderedAccessViewSize**](https://msdn.microsoft.com/library/windows/hardware/ff538320)

[**CreateUnorderedAccessView**](https://msdn.microsoft.com/library/windows/hardware/ff540711)

[**DestroyUnorderedAccessView**](https://msdn.microsoft.com/library/windows/hardware/ff552812)

[**ClearUnorderedAccessViewFLOAT**](https://msdn.microsoft.com/library/windows/hardware/ff539412)

[**ClearUnorderedAccessViewUINT**](https://msdn.microsoft.com/library/windows/hardware/ff539414)

[**CopyStructureCount**](https://msdn.microsoft.com/library/windows/hardware/ff540544)

[**SetRenderTargets(D3D11)**](https://msdn.microsoft.com/library/windows/hardware/ff569554)

 

 





