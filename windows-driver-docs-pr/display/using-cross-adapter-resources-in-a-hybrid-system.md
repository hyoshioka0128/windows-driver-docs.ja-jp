---
title: ハイブリッド システムでのクロス アダプター リソースの使用
description: Windows Display Driver Model (WDDM) ドライバーは、ハイブリッド システムでは、統合の GPU と独立した GPU の間のクロス アダプターのリソースの共有場所をサポートできます。
ms.assetid: ECBB0AA7-50C2-41C8-9DC6-6EEFC5CEEB15
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ea3970fae802be698797d295a53192fae0c02b3c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373571"
---
# <a name="span-iddisplayusingcross-adapterresourcesinahybridsystemspanusing-cross-adapter-resources-in-a-hybrid-system"></a><span id="display.using_cross-adapter_resources_in_a_hybrid_system"></span>ハイブリッド システムでクロス アダプター リソースの使用


Windows Display Driver Model (WDDM) ドライバーをサポートできる Windows 8.1 以降、*ハイブリッド システム*ここで、*クロス アダプター リソース*統合の GPU と、独立した GPU の間で共有されると、アプリケーションは、アプリケーションのニーズに応じて、いずれかの GPU 上で実行できます。 オペレーティング システムとドライバーをまとめて、GPU でアプリケーションを実行する必要がありますを決定します。

ディスプレイのミニポート ドライバーはクロス アダプター リソースのサポートを設定して express する必要があります、 **CrossAdapterResource**のメンバー、 [ **DXGK\_VIDMMCAPS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_vidmmcaps)構造体。

ドライバーは、割り当ての種類に応じて異なる方法で情報を取得します。 ユーザー モードのディスプレイ ドライバーがプライマリ フラグ、ビデオのネットワーク (VidPN) 存在するソース ID、リフレッシュ レート、および回転など、プライマリの作成時に、通常提供される情報を取得、割り当てが、従来の全画面表示のプライマリの場合は、情報。 ただし、割り当てが、直接に反転するプライマリの場合は、クロス アダプターの割り当ては、プライマリとして使用することがユーザー モードのディスプレイ ドライバーは、プライマリが作成されるときに提供される一般的な情報を得られません。 また、ここでは、個別のユーザー モードのディスプレイ ドライバー プライマリに関する情報を受け取るが検証されない必要があります。 統合されたドライバーは、プライマリであるかを示す情報を受信しません。

これら以降のトピックでは、ハイブリッド システムのドライバーの実装の詳細が得られます。

-   [ハイブリッド システム構成の検証](validating-a-hybrid-system-configuration.md)
-   [クロス アダプターのリソースを使用して、独立した GPU でのレンダリング](rendering-on-a-discrete-gpu-using-cross-adapter-resources.md)
-   [ハイブリッド システム DDI](hybrid-system-ddi.md)

## <a name="span-iddefinitionofahybridsystemspanspan-iddefinitionofahybridsystemspandefinition-and-properties-of-a-hybrid-system"></a><span id="definition_of_a_hybrid_system"></span><span id="DEFINITION_OF_A_HYBRID_SYSTEM"></span>定義とハイブリッド システムのプロパティ:


-   システムには、単一の統合された GPU と 1 つの独立した GPU が含まれています。*GPU を統合*は CPU チップセットと、統合表示パネル LCD パネルなどの出力に統合されています。
    *独立した GPU*は通常 PCI などのバスを介してマザーボード チップセットの north ブリッジに接続するリムーバブル カード。
-   独立した GPU が、統合の GPU よりパフォーマンスが大幅に向上します。
-   不連続の GPU でレンダリング専用デバイスでは、あり表示出力が接続されていません。
-   Gpu が同じハウジングに物理的に囲まれていると、独立した GPU を接続または切断、コンピューターが動作していることはできません。
-   オペレーティング システムは、新しいドライバーがインストールされているときに電源投入時の自己テスト (POST) のルーチンの実行時に、またはディスプレイ アダプターを有効または無効になっているときに、ハイブリッド システムの構成を検出します。

## <a name="span-iddefinitionofacrossadapterresourcespanspan-iddefinitionofacrossadapterresourcespandefinition-and-properties-of-a-cross-adapter-resource"></a><span id="definition_of_a_cross_adapter_resource"></span><span id="DEFINITION_OF_A_CROSS_ADAPTER_RESOURCE"></span>定義とアダプター間のリソースのプロパティ:


-   アダプターが複数のリソースは、以降 Windows 8.1 でのみ使用できます。
-   Aperture GPU メモリ セグメントにのみにページングできます。
-   共有リソースとして割り当てられます。
-   線形の形式で、1 つだけ割り当てがあります。
-   128 バイトの標準的なピッチの配置 (によって定義された、 **D3DKMT\_クロス\_アダプター\_リソース\_ピッチ\_配置**定数)。
-   4 行の高さの標準的な配置が (によって定義された、 **D3DKMT\_クロス\_アダプター\_リソース\_高さ\_配置**定数)。
-   そのメモリの開始アドレスは、1 ページ境界に配置されます。
-   ディスプレイのミニポート ドライバーによってカーネル モードから標準的な割り当てとして作成する場合があり、後で開いて、ユーザー モードのディスプレイ ドライバー。
-   これは、ユーザー モードのディスプレイ ドライバーによって作成されます。

 

 





