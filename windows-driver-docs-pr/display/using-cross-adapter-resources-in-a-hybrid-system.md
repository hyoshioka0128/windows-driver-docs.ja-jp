---
title: ハイブリッド システムでのクロス アダプター リソースの使用
description: Windows Display Driver Model (WDDM) ドライバーは、クロスアダプターリソースが統合 GPU と別個の GPU の間で共有されるハイブリッドシステムをサポートできます。
ms.assetid: ECBB0AA7-50C2-41C8-9DC6-6EEFC5CEEB15
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f828150a97a283d8238b6f3c3dbea69828df42b7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829277"
---
# <a name="span-iddisplayusing_cross-adapter_resources_in_a_hybrid_systemspanusing-cross-adapter-resources-in-a-hybrid-system"></a><span id="display.using_cross-adapter_resources_in_a_hybrid_system"></span>ハイブリッドシステムでのクロスアダプターリソースの使用


Windows 8.1 以降では、Windows Display Driver Model (WDDM) ドライバーは、*クロスアダプターリソース*が統合 gpu と別個の gpu の間で共有される*ハイブリッドシステム*をサポートできます。また、アプリケーションは、アプリケーションのニーズ。 オペレーティングシステムとドライバーの組み合わせによって、アプリケーションを実行する必要がある GPU が決まります。

ディスプレイミニポートドライバーは、 [**DXGK\_VIDMMCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_vidmmcaps)構造体のクロス**adapterresource**メンバーを設定することによって、クロスアダプターリソースのサポートを表す必要があります。

ドライバーは、割り当ての種類に応じて、さまざまな方法で情報を取得します。 割り当てが従来の全画面のプライマリである場合、プライマリフラグ、ビデオの存在するネットワーク (VidPN) ソース ID、リフレッシュレート、およびローテーションなど、プライマリの作成時に通常提供される情報がユーザーモード表示ドライバーによって取得されます。参照. ただし、割り当てが直接フリッププライマリである場合、アダプター間の割り当てはプライマリとして使用できますが、ユーザーモードの表示ドライバーは、プライマリの作成時に提供される通常の情報を取得しません。 また、この場合、個別のユーザーモード表示ドライバーはプライマリに関する情報を受け取りますが、検証する必要はありません。 統合ドライバーは、それがプライマリであることを示す情報を受信しません。

次のトピックでは、ハイブリッドシステムのドライバー実装の詳細について説明します。

-   [ハイブリッドシステム構成の検証](validating-a-hybrid-system-configuration.md)
-   [クロスアダプターリソースを使用した個別の GPU でのレンダリング](rendering-on-a-discrete-gpu-using-cross-adapter-resources.md)
-   [ハイブリッドシステム DDI](hybrid-system-ddi.md)

## <a name="span-iddefinition_of_a_hybrid_systemspanspan-iddefinition_of_a_hybrid_systemspandefinition-and-properties-of-a-hybrid-system"></a><span id="definition_of_a_hybrid_system"></span><span id="DEFINITION_OF_A_HYBRID_SYSTEM"></span>ハイブリッドシステムの定義とプロパティ:


-   システムには1つの統合 GPU と1つの独立した GPU が含まれています。*統合 gpu*は CPU チップセットに統合され、LCD パネルなどの統合されたディスプレイパネルに出力されます。
    *個々の GPU*は通常、PCI などのバスを介してマザーボードチップセットの北ブリッジに接続するリムーバブルカードです。
-   離散 GPU は、統合 GPU よりも大幅に高いパフォーマンスを備えています。
-   個別の GPU はレンダリング専用のデバイスであり、表示出力は接続されていません。
-   両方の Gpu が物理的に同じハウジングに入っており、コンピューターの実行中に個別の GPU が接続または切断されることはありません。
-   オペレーティングシステムは、新しいドライバーがインストールされたとき、またはディスプレイアダプターが有効または無効になっているときに、電源オン自己テスト (POST) ルーチンを実行すると、ハイブリッドシステムの構成を検出します。

## <a name="span-iddefinition_of_a_cross_adapter_resourcespanspan-iddefinition_of_a_cross_adapter_resourcespandefinition-and-properties-of-a-cross-adapter-resource"></a><span id="definition_of_a_cross_adapter_resource"></span><span id="DEFINITION_OF_A_CROSS_ADAPTER_RESOURCE"></span>クロスアダプターリソースの定義とプロパティ:


-   クロスアダプタリソースは Windows 8.1 からのみ使用できます。
-   これは、絞り GPU メモリセグメントにのみページングされます。
-   共有リソースとして割り当てられます。
-   線形形式の割り当ては1つだけです。
-   これには、128バイトの標準ピッチアラインメントがあります ( **D3DKMT\_クロス\_アダプター\_リソース\_ピッチ\_アラインメント**定数)。
-   これには、4行の標準の高さアラインメントが用意されています ( **D3DKMT\_クロス\_アダプター\_リソース\_高さ\_アラインメント**定数)。
-   メモリの開始アドレスは、1ページの境界に合わせて調整されます。
-   これは、ディスプレイミニポートドライバーによってカーネルモードから標準の割り当てとして作成され、後でユーザーモードのディスプレイドライバーによって開かれる場合があります。
-   これは、ユーザーモードの表示ドライバーによって作成される場合があります。

 

 





